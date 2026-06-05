# ✋ magic-hands — Gesture-Controlled 3D Web App

A **single self-contained HTML file** (`hand-3d.html`) that runs a gesture-controlled 3D experience in your browser.  
No npm, no build step, no install — every library loads from a CDN.  
Works on **phone and laptop**, over `https` or `http://localhost`.

---

## Live demo (GitHub Pages)

Open on your phone — camera and motion sensors work over `https`:

**https://rai515515.github.io/magic-hands/hand-3d.html**

Allow the camera prompt when it appears. On iOS, also allow Motion & Orientation when switching to Scan mode.

---

## How to run locally

### Laptop
```bash
python3 -m http.server 8000
# then open: http://localhost:8000/hand-3d.html
```

### Phone (same Wi-Fi as laptop)
```bash
# Find your laptop's IP:
# Mac:     ipconfig getifaddr en0
# Windows: ipconfig  (look for IPv4 under Wi-Fi)
# Linux:   hostname -I
# Then open on your phone: http://192.168.x.x:8000/hand-3d.html
```

---

## Features — all 41

### Place mode (3D model library)

| # | Feature | Notes |
|---|---------|-------|
| 1 | Live camera feed, full-screen | `object-fit: cover`, no stretching |
| 2 | Auto-selects camera | Rear camera on phones, webcam on laptops |
| 3 | Flip Camera button | Switches front/rear at any time |
| 4 | Real-time hand tracking | Google MediaPipe Hands, one hand |
| 5 | Skeleton overlay | 21 landmark dots + connection lines, aligned to cropped video |
| 6 | 3D model floating over camera | Three.js on a transparent canvas |
| 7 | Pinch to grab and move | Thumb + index tip distance, with hysteresis |
| 8 | Pinch-gap to resize | Open/close fingers scales the model smoothly |
| 9 | Auto-spin when released | Gentle idle rotation on X and Y |
| 10 | Drag-to-rotate | One-finger touch or mouse drag rotates on any axis |
| 11 | On-screen help text | Updates per mode |
| 12 | Live FPS counter | Smoothed, always visible top-right |
| 13 | Responsive layout | Portrait + landscape, phone + laptop, safe areas |
| 14 | Model menu | Scrollable button row; active model highlighted |
| 15 | Built-in cube | Always available, wireframe hologram style |
| 16 | URL-based model slots | Heart / Skull / Brain — paste any .glb URL to activate |
| 17 | GLTFLoader from CDN | Loads .glb / .gltf files; Three.js r128 |
| 18 | Loading overlay | Shown while a model downloads |
| 19 | Load error + fallback | Friendly 5-second message; reverts to cube automatically |
| 20 | Upload model button | Opens OS file picker, .glb / .gltf only |
| 21 | Local file loading | URL.createObjectURL — fully offline, no CORS |
| 22 | "My model" in menu | Uploaded model persists in menu for the session |
| 23 | Auto-fit on load | Bounding-box scale + recentre — any size .glb fits correctly |
| 24 | modelGroup container | All gestures work identically on any loaded model |

### Scan mode (capture photos of a real object)

| # | Feature | Notes |
|---|---------|-------|
| 25 | Mode toggle button | Place / Scan; purple tint in Scan mode |
| 26 | Pinch once to start capture | Rising-edge detection, no flicker |
| 27 | Pinch again to stop | Manual stop at any time |
| 28 | Timed auto-capture | One photo every 0.5 s, up to 30 frames |
| 29 | Thumbnail strip | Scrollable, auto-scrolls to newest |
| 30 | Download as ZIP | JSZip; files named frame_001.jpg and so on |
| 31 | README inside ZIP | Explains how to feed frames into Luma AI / Polycam / Nerfstudio |
| 32 | Honest on-screen notes | Browser cannot do live photogrammetry — says so clearly |
| 33 | 12-segment coverage ring | Clock-face SVG; fills as you orbit the object |
| 34 | Real compass heading | DeviceOrientation / webkitCompassHeading; permission requested on iOS |
| 35 | Coverage ring fallback | Fills next empty slot if sensor is unavailable |
| 36 | "Good coverage" message | Shown when all 12 segments are green |
| 37 | Blur detection | Laplacian-variance sharpness check on 128 px grayscale frame |
| 38 | Skip blurry frames | Rejected frames not saved; quick retry on next tick |
| 39 | Live steadiness meter | Green = sharp enough; orange = hold steadier |
| 40 | Auto-stop | Stops automatically when ring is full AND 20+ sharp frames saved |
| 41 | Scan complete + upload note | Pulses Download button; tells you to drag ZIP into Luma/Polycam |

---

## Adding anatomy models

1. Find a free `.glb` on [Sketchfab](https://sketchfab.com) (filter: Downloadable + Free) or [Z-Anatomy](https://www.z-anatomy.com).
2. Open `hand-3d.html` in any text editor.
3. Find the `MODEL_LIBRARY` array near the top of the `<script>`.
4. Paste the direct `.glb` URL into the matching `url: ''` slot.
5. Save and reload — tap the button in the model menu.

**CORS note:** if the URL loads with an error, use the Upload model button instead — it loads from your local device and always works.

---

## Libraries used (all CDN, no install)

| Library | Version | Purpose |
|---------|---------|---------|
| Three.js | r128 | 3D rendering |
| Three.js GLTFLoader | r128 | Load .glb / .gltf models |
| MediaPipe Hands | 0.4 | Real-time hand tracking |
| MediaPipe Camera Utils | 0.3 | Feed camera frames to MediaPipe |
| JSZip | 3.10 | Build the scan ZIP in-browser |

---

## Commit history

| Commit | What was added |
|--------|---------------|
| `571ff5f` | Base app: camera, hand tracking, 3D cube, pinch gestures, FPS |
| `90e51b8` | Scan mode: capture, thumbnails, ZIP download, README.txt |
| `ffc20a3` | Coverage ring (motion sensor), blur detection, steadiness meter |
| `3d3dac7` | Auto-stop on full sharp coverage, Scan complete message |
| `e7be7d7` | 3D model library, file upload, auto-fit, drag-to-rotate |
