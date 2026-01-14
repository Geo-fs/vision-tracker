# Vision Tracker (Hand & Face AI)

A modular, real-time computer vision system that tracks **hands and faces** from a webcam, counts fingers per hand, and classifies gestures. Built with **Python + OpenCV + MediaPipe**, designed for easy expansion into ML, automation, and interactive control.

This project is intentionally structured as a **base architecture**, not a finished product.

---

## Features

- Real-time hand and face landmark tracking  
- Per-hand **finger counting** (thumb included, with sanity checks)  
- Gesture classification:
  - **Fist**
  - **Open Palm**
  - **Pinch**
  - **Point**
  - **Partially Open (N fingers)**
- Handedness detection (**Left / Right**)
- Live **AI View** (picture-in-picture) showing what the system detects
- Modular file structure built for extension and refactoring

---

## Requirements

- **Windows / macOS / Linux**
- **Python 3.10 – 3.11**  
  > MediaPipe is *not* compatible with Python 3.14 (yes, it’s annoying).
- A working webcam

---

## Setup (From ZIP Download)

### 1) Download and extract

1. Go to the GitHub repo’s **Releases**
2. Download the `.zip` for the latest release (example: `v1.01.04`)
3. Extract it to a folder on your computer

Example path:
C:\Users\yourname\vision_tracker

---

### 2) Create a virtual environment (recommended)

Open **PowerShell** or a terminal inside the extracted folder:

```bash
cd path/to/vision_tracker
python -m venv visionenv
```

Activate it:

**Windows:**

```bash
visionenv\Scripts\activate
```

**macOS / Linux**

```bash
source visionenv/bin/activate
```

*You should now see (visionenv) in your terminal.*

3) Install dependencies
With the virtual environment active:

```bash
pip install -r requirements.txt
```

**This installs:**

- opencv-python

- mediapipe (pinned for compatibility)

- numpy

### 4) Run the app
**From the project root:**

```bash
python main.py
```

### Expected behavior:

- Webcam feed opens

- Hand + face overlays appear

**Each hand shows:**

- Left/Right handedness

- Finger count

- Gesture label

- A small AI View PiP appears showing what the tracker “sees”

*Press ESC to exit whenever you want!*

### Project Structure
vision_tracker/
├── main.py                 # Main application loop
├── config.py               # App configuration and toggles
├── requirements.txt
└── pipeline/
    ├── camera.py           # Webcam handling
    ├── detectors.py        # MediaPipe detectors
    ├── render.py           # Drawing & overlays
    ├── face.py             # Face-specific rendering logic
    ├── gestures.py         # Finger counting & gesture logic
    ├── features.py         # Landmark utilities
    └── utils.py            # Shared helpers
    
**This separation is intentional: you can upgrade one part (like gestures) without rewriting the whole app.**

### Configuration
**Edit settings in config.py, including:**

- webcam index (if you have multiple cameras)

- whether the image is mirrored

- detection confidence thresholds

- whether the AI PiP is shown and its size

### Modifying the AI
**This is the whole point. Common places to extend:**

- Finger counting + gesture logic
- pipeline/gestures.py
- tune thresholds
- add new gestures
- replace rules with a trained ML classifier
- Visual overlays
- pipeline/render.py
- pipeline/face.py
- Detection pipeline
- pipeline/detectors.py
- add pose tracking
- add multi-face support
- enable/disable landmark refinements

### Troubleshooting
- Webcam doesn’t open
  Try changing the camera index in config.py:
  
  0 → 1 or 2

- MediaPipe errors / missing modules
  Confirm you’re using Python 3.10 or 3.11
  
  Confirm your virtual environment is activated:
  
  Windows: (visionenv) should appear in the terminal

- Console warnings
  MediaPipe/TFLite can be noisy. Warnings are usually safe to ignore unless the app crashes.

- MediaPipe Not Working/Downloading:
    Try:
   ```bash
    pip install mediapipe==0.10.14 opencv-python numpy 
   ```
   You can also try:
  ```bash
  python -c "import mediapipe as mp; print(mp.__version__); print('solutions?', hasattr(mp,'solutions'))"
  ```
  If it coems back with a version number and "Solutions? True" then your good.

**IT IS VERY IMPORTANT THAT YOU ARE USING THE LATEST VERSION OF PIP!**
*Additionaly, you may need to download Python 3.11.9 and add it to PATH!* You Can Find It Here: https://www.python.org/downloads/release/python-3119/

#### *As always, when in doubt: ask Google or ChatGPT.*

### License
**This project is released under the MIT License.**

You can:

- use it commercially

- modify it

- redistribute it

- embed it in other projects

*Just don’t sue anyone when your webcam becomes self-aware.*

### Future Direction
This release is a foundation, not a final system. Supported expansion paths include:

ML-based gesture classification

temporal smoothing and motion tracking

face pose + gaze estimation

automation hooks and action mapping

recording + dataset generation

plugin-based modules and pipelines

**If it can track your fingers today, it can control an entire interface tomorrow.**
