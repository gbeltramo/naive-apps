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
```
