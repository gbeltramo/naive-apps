# Earth and Solar System Prompt

```text
You are an autonomous coding agent working inside the Zed editor with file and terminal tools. Build the whole app yourself without asking me any questions. Make reasonable decisions and finish.

GOAL
Create ONE file, `index.html`, in this directory root: an interactive 3D visualisation of the Earth and the Solar System using three.js. It must work by opening the file or running `python3 -m http.server` and visiting it in a browser. No build step, no npm.

TECH CONSTRAINTS
- Single HTML file with inline <style> and <script type="module">.
- Load three.js through an import map pinned to a specific version, for example:
  "three": "https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js"
  "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.160.0/examples/jsm/"
- Use OrbitControls from three/addons.
- Do NOT depend on external image/texture files. Generate all textures procedurally (canvas 2D or GLSL noise). A missing texture must never break the app.

QUALITY BAR
- Runs at a smooth frame rate. Use reasonable sphere segment counts.
- No console errors or warnings.
- Clean, commented code organised in clear sections.

WORKFLOW (follow strictly)
1. Do not write a long plan. Write the complete file in one go with your file-creation tool.
2. Start `python3 -m http.server 8000` in the background with the terminal tool, if available, and sanity check that the file is served. Re-read your code once and fix syntax errors, typos in three.js API names, and import map mistakes.
3. If anything is wrong, edit the file and fix it. Repeat at most 3 times.
4. Finish with a 5-line summary: how to run it, controls, and known limitations.

Begin now.
```
