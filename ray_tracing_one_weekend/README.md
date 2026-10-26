# [Ray Tracing in One Weekend](https://raytracing.github.io/books/RayTracingInOneWeekend.html)

```text
You are an autonomous coding agent working inside the Zed editor with file and terminal tools. Build the whole app yourself without asking me any questions. Make reasonable decisions and finish.

GOAL
Create ONE file, `index.html`, in the project root: a from-scratch port of the book "Ray Tracing in One Weekend" (https://raytracing.github.io/books/RayTracingInOneWeekend.html) to pure JavaScript, running in the browser and rendering the book's final scene to a <canvas>. Use NO libraries at all (no three.js, no WebGL, no WASM): just plain JS and the 2D canvas for displaying pixels.

TECH CONSTRAINTS
- Single HTML file with inline <style> and <script>.
- No external requests of any kind.
- The renderer must not freeze the page: run the render in a Web Worker created from a Blob URL (or render in time-sliced chunks with requestAnimationFrame / setTimeout). Progressive display: update the canvas as rows or tiles complete, and show a progress bar and elapsed time. Prefer multiple workers (navigator.hardwareConcurrency, capped at 8), each rendering interleaved scanlines or tiles, if you can do it reliably; a single worker is acceptable.
- Use a seeded PRNG (e.g. mulberry32) so renders are deterministic.

IMPLEMENT THE BOOK'S ARCHITECTURE
Mirror the book chapter by chapter, as small clear classes/functions with comments referencing the chapter:
- Vec3 (add, sub, mul, div, dot, cross, length, unit, nearZero, reflect, refract, random helpers, randomUnitVector, randomInUnitDisk). Aliases for Point3 and Color are fine. Avoid excessive allocation in the hot loop where easy, but clarity matters more.
- Ray (origin, direction, at(t)).
- Interval and HitRecord (point, normal, t, frontFace, material, setFaceNormal).
- Sphere with the quadratic hit test (use the half-b optimisation as in the book).
- HittableList.
- Camera: image width and aspect ratio, vfov, lookfrom, lookat, vup, defocus angle (depth of field), focus distance, samples per pixel, max depth. Include antialiasing with random sampling inside the pixel.
- Materials: Lambertian (with scatter direction degenerate-case handling), Metal (with fuzz), Dielectric (refraction, total internal reflection, Schlick reflectance).
- Gamma correction (gamma 2), color clamping, and background sky gradient.
- Ray color computed iteratively or recursively with a max depth.

FINAL SCENE (the book's cover image)
- A large ground sphere (radius 1000, at y=-1000) with a gray lambertian material.
- A grid of small spheres for a, b from -11 to 10: random material choice (about 80% lambertian with random albedo squared, 15% metal with random albedo in [0.5,1] and fuzz in [0,0.5], 5% glass with index 1.5), radius 0.2, centered at (a+0.9*rand, 0.2, b+0.9*rand), skipping those within 0.9 of (4, 0.2, 0).
- Three large spheres of radius 1: glass at (0,1,0), lambertian (0.4,0.2,0.1) at (-4,1,0), metal (0.7,0.6,0.5) fuzz 0 at (4,1,0).
- Camera: vfov 20, lookfrom (13,2,3), lookat (0,0,0), vup (0,1,0), defocus angle 0.6, focus distance 10.

UI
- Controls: image width (default 400, choices 200/400/600/800/1200), samples per pixel (default 50; presets 10/50/100/500), max depth (default 50), "Render" and "Stop" buttons, and a preset dropdown: "Quick preview" (200px, 10 spp), "Balanced" (400px, 50 spp), "Final quality" (800px, 200 spp).
- A secondary scene dropdown showing the book's earlier milestones as simple scenes rendered with the same code: "Ch.6 normals sphere", "Ch.9 diffuse", "Ch.11 metal/glass trio", and "Final scene".
- A "Download PNG" button.
- Show: progress %, elapsed time, rays/second estimate.
- Render automatically a Quick preview of the final scene on page load.

QUALITY BAR
- No console errors. The page stays responsive during rendering.
- Correct-looking result: soft shadows-free diffuse spheres with light bounce, fuzzy metals, hollow-looking glass with refraction, and blurred foreground/background from the defocus blur.
- Clean, commented code, with sections matching the book's chapters.

WORKFLOW (follow strictly)
1. Do not write a long plan. Write the complete file in one go with your file-creation tool.
2. Start `python3 -m http.server 8000` in the background, if a terminal tool is available. Re-read your code once, checking: the worker code string is self-contained (the worker cannot access main-thread classes, so the full ray tracer must live inside the worker source), messages are passed correctly, pixel buffers are transferred properly, and the gamma and image orientation are right (y not flipped).
3. Fix problems by editing the file. Repeat at most 3 times.
4. Finish with a 5-line summary: how to run it, controls, expected render times, and known limitations.

Begin now.
```
