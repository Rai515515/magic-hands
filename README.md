# Magic Hands ✋🧊

A gesture-controlled 3D web app that runs in your browser — on phone or laptop — using your camera and your hands. Place 3D models (including anatomy models) into your live camera view and manipulate them with hand gestures, or capture photos of a real object to turn into a 3D model with external tools.

Everything is in **one file** (`hand-3d.html`), uses only CDN libraries, and needs no build step or install.

---

## What it does

**Place mode** — Drop a 3D model into your live camera feed and control it with your hand:

- **Pinch** thumb + index → grab and move the model
- **Pinch gap** (open/close fingers) → scale it bigger/smaller
- **Release** → model auto-spins on its own
- **Rotate slider / gesture** → study it from any fixed angle
- **Model library** → switch between built-in models (Cube, Heart, Skull, Brain)
- **Upload model** → load your own `.glb`/`.gltf` straight from your device (auto-fit and recentered)

**Scan mode** — Capture an ordered set of photos of a real object to feed into 3D reconstruction tools:

- **Pinch** to start/stop capture (auto-snaps a frame every ~½ second)
- **Coverage ring** — a 12-segment clock face lights up green as you orbit the object, so you know you've covered every angle
- **Blur detection** — shaky/blurry frames are skipped automatically; only sharp photos are saved
- **Steadiness meter** — live indicator of whether the camera is steady enough
- **Auto-stop** — capture finishes on its own once all 12 segments are green and ≥20 sharp frames are saved
- **Download ZIP** — saves all photos (named in order) plus a README of capture tips

---

## How to run it

The camera only works over `https://` or `localhost` — not from a double-clicked file.

### Easiest (phone or laptop, no setup): GitHub Pages

Open the hosted URL directly in any browser:

```
https://rai515515.github.io/magic-hands/hand-3d.html
```

Tap **Start Camera** → **Allow**. If a Motion & Orientation prompt appears, tap **Allow**.

### Local on a laptop

```bash
python3 -m http.server 8000
```

Then open: `http://localhost:8000/hand-3d.html`

### Local over Wi-Fi (laptop serves, phone opens)

Run the command above on your laptop, find your laptop's local IP, then on your phone open:

```
http://<your-laptop-ip>:8000/hand-3d.html
```

---

## How to use it

### Place mode (3D models)

1. Tap **Start Camera** and allow access.
1. Make sure the mode button reads **🧩 Mode: Place**.
1. Pick a model from the menu, or tap **📁 Upload model** to load your own `.glb`.
1. **Pinch** to grab and move it. **Change the pinch gap** to scale. **Release** to auto-spin. Use the **rotate slider/gesture** to study angles.

### Scan mode (capture a real object)

1. Tap **Mode** until it reads **📷 Mode: Scan** (use the rear camera — **🔄 Flip** if needed).
1. Aim at a solid, textured, well-lit object. Wait for the steadiness meter to go green.
1. **Pinch** once to start. Slowly walk around the object, pausing at each angle.
1. Fill all 12 ring segments green until **Scan complete ✓** appears (or pinch again to stop early).
1. Tap **⬇ Download photos (ZIP)**.

---

## Adding your own 3D models

The app loads standard **`.glb`** / **`.gltf`** files. Free anatomy and other models:

- **[Sketchfab](https://sketchfab.com)** — search e.g. "heart anatomy", filter to **Downloadable + Free**, download the `.glb`.
- **[Z-Anatomy](https://www.z-anatomy.com)** — free, open-source full human anatomy.
- **[NIH 3D](https://3d.nih.gov)** — free medical/anatomical models from the US National Institutes of Health.

Then tap **📁 Upload model** and pick the file — nothing is uploaded to any server; it loads locally in your browser.

---

## Turning a scan into a real 3D model

The browser captures photos; the actual photoreal 3D model is built by a dedicated tool. Unzip your downloaded photos and feed them into one of these:

- **[Luma AI](https://lumalabs.ai)** *(try first)* — easiest, great results from phone photos.
- **[Polycam](https://poly.cam)** — beginner-friendly web uploader; good backup.
- **[Nerfstudio](https://docs.nerf.studio)** — advanced, runs on your own GPU; full control.

**For best results:** keep the object still, move slowly all the way around, light it well, and grab high/low/side angles. Shiny, transparent, or featureless objects (glass, mirrors, blank white surfaces) don't reconstruct well.

---

## Honest limitations

- **No live 3D reconstruction in-browser.** Photoreal scanning needs heavy GPU work a browser tab can't do live — hence the capture-then-reconstruct workflow above.
- **Hand tracking is heavy.** On older phones the framerate may drop. Start with single-organ models, not full skeletons.
- **Coverage ring uses the phone's motion sensor.** It reliably tells directions apart but exact compass north can drift — treat it as a "have I been all the way around?" guide. If sensor access is blocked, it falls back to a simple progress count.
- **Model load speed** depends on file size — large `.glb` files load slowly on phones.

---

## Tech

- **[MediaPipe Hands](https://developers.google.com/mediapipe)** — real-time hand tracking
- **[Three.js](https://threejs.org)** — 3D rendering + `GLTFLoader`
- **[JSZip](https://stuk.github.io/jszip/)** — packaging captured frames
- **DeviceOrientation / DeviceMotion API** — coverage ring direction
- All loaded from CDN. Single file. No build step.

---

## License

MIT
