# Tilt‑Pen AR Webapp

This repository contains a mobile‑first web app that lets you use your smartphone like a pen on any flat surface. By tilting the phone and moving it like a pen, the app records the device’s orientation to draw strokes on a canvas overlay. It’s ideal for quick notes, signatures and scribbles without touching the screen.

## How it works

The app listens for `DeviceOrientation` events when you press **Start**. If the phone is tilted forward beyond a threshold, it is treated as “pen down” and the change in orientation angles (`beta` and `gamma`) is mapped to movements on a canvas. The canvas sits on top of a live camera feed from the rear camera to create an augmented‑reality effect. Press **Stop** to halt recording or **Clear** to erase the canvas.

### Architecture

At a high level, the app follows these steps:

1. **Tilt Detection** – Determine if the device is pitched forward far enough to simulate a pen touching the table.
2. **Orientation Mapping** – Convert small changes in pitch (`beta`) and roll (`gamma`) into 2D deltas for drawing.
3. **Canvas Rendering** – Draw lines between successive points while the pen is down.
4. **Controls & Video** – Display a rear‑camera preview underneath the canvas and provide Start/Stop/Clear controls.

## Running locally

You can run the app locally with any static file server. For example, with Python:

```
bash
python3 -m http.server 8000
```

Then open `http://localhost:8000/index.html` on a mobile device. Grant camera permission, press **Start** and tilt the phone forward like a pen to begin drawing. Lift the phone to stop drawing.

## Limitations & future improvements

This project is a prototype. It infers pen motion purely from orientation, which means lines can drift and accuracy is limited. There is no true spatial tracking or depth sensing. Browser support varies; modern mobile Chrome and Firefox work best, whereas iOS Safari may require experimental flags. Future work could include calibration settings and integration with WebXR anchors or AR markers for better precision.

## Confidence

The current implementation meets the basic requirements and demonstrates the concept, but it lacks precise tracking and robust AR features. I estimate about **70 % confidence** that this approach will satisfy your initial objective. Feedback and testing will help refine thresholds, sensitivity and UI.

## License

This project is provided under the MIT License.
