# Tree Model Prompt

```text
You are an autonomous coding agent working inside the Zed editor with file and terminal tools. Build the whole app yourself without asking me any questions. Make reasonable decisions and finish.

GOAL
Create ONE file, `index.html`, in the project root: a procedural 3D tree generator with animated leaves, wind, and real-time shadows, using three.js. It must work by opening the file or via `python3 -m http.server`. No build step, no npm.

TECH CONSTRAINTS
- Single HTML file, inline <style> and <script type="module">.
- three.js via import map pinned to a specific version, for example:
  "three": "https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js"
  "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.160.0/examples/jsm/"
- OrbitControls from three/addons.
- No external image files. Generate bark and leaf textures with canvas 2D.
- Build the UI with plain HTML inputs (no GUI library).

FEATURES
1. Procedural tree: generate the branching recursively (or with a simple L-system) from a seeded random number generator. Parameters: seed, trunk height, trunk radius, branching depth (3 to 7), branch angle, length decay, radius decay, and gravity droop. Build branches as tapered cylinders merged into one BufferGeometry (or an InstancedMesh) for performance. Use a procedural bark texture with normal-like variation.
2. Leaves: use InstancedMesh with thousands of quad leaves (2000 to 20000, adjustable) attached to the terminal branches, each with random orientation, size, and color variation (green to yellow-green; optional autumn palette toggle). Use a canvas-generated leaf texture with alpha and `alphaTest`, and DoubleSide.
3. Wind: implement it in the vertex shader by patching the materials with `onBeforeCompile`, so the CPU does no per-vertex work.
   - Branches sway with a low-frequency motion whose amplitude grows with height and distance from the trunk axis.
   - Leaves flutter with a higher-frequency motion plus a per-instance phase.
   - Uniforms: time, wind strength, wind direction (angle), gust frequency. A smooth gust effect (sum of sines/noise) is required.
4. Lighting and shadows: one DirectionalLight with PCFSoftShadowMap, shadow camera tightly fitted to the tree, a hemisphere light for ambient fill, and a ground plane that receives shadows. IMPORTANT: leaves and branches must cast shadows that match the wind animation, so provide a custom `customDepthMaterial` (MeshDepthMaterial patched with the same wind vertex code) for both the leaves and branches. Without this, shadows would not move.
5. Environment: sky gradient background (or a Sky shader), light fog, and a grass-colored ground with subtle procedural texture.
6. UI panel with sliders: seed + "Regenerate" button, depth, leaf count, wind strength, wind direction, gust frequency, sun elevation and azimuth, and toggles for shadows and autumn colors. Rebuilding the tree on change must be fast and must dispose of old geometries and materials to avoid leaks.
7. Responsive canvas, devicePixelRatio capped at 2, and FPS counter in a corner.

QUALITY BAR
- No console errors or warnings.
- Smooth frame rate with the default settings.
- Clean, commented code split into sections: setup, textures, tree generation, wind shader patch, UI, loop.

WORKFLOW (follow strictly)
1. Do not write a long plan. Write the complete file in one go with your file-creation tool.
2. Start `python3 -m http.server 8000` in the background, if a terminal tool is available. Re-read your code once, checking: import map, API names, shader injection strings actually match the chunk names (`#include <begin_vertex>`), the instance matrix is applied correctly in the wind code, and depth materials are assigned.
3. Fix problems by editing the file. Repeat at most 3 times.
4. Finish with a 5-line summary: how to run it, controls, and known limitations.

Begin now.
```
