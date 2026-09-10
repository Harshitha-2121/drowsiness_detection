# Drowsiness Detection System

An AI-powered real-time driver drowsiness detection system built with OpenCV, Dlib, and Pyttsx3. The system tracks facial landmarks to calculate the Eye Aspect Ratio (EAR) from live webcam video streams and triggers audio/visual alarms when drowsiness is detected.

## 📌 Features
- **Real-Time Facial Landmark Tracking:** Detects 68 facial landmark coordinates using `dlib`'s HOG-based face detector.
- **Eye Aspect Ratio (EAR) Calculation:** Measures vertical vs. horizontal distance between eye landmarks to detect closed eyes.
- **Audio & Visual Alerts:** Plays voice notifications ("Alert! DROWSINESS ALERT!") using text-to-speech (`pyttsx3`) and displays warning overlays on the video stream when eyes remain closed across consecutive frames.
- **Live Video Stream Processing:** Efficient multi-threaded video stream handling via `imutils`.

## 🛠️ Prerequisites & Dependencies
Make sure you have Python installed. Install the required packages using pip:

```bash
pip install opencv-python dlib imutils scipy pyttsx3
```

> **Note on Dlib:** Installing `dlib` requires C++ build tools (CMake). On Windows, ensure CMake and Visual Studio C++ Build Tools are installed prior to running `pip install dlib`.

## 🚀 How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/Harshitha-2121/drowsiness_detection.git
   cd drowsiness_detection
   ```

2. Run the detection script by passing the facial landmark predictor model path:
   ```bash
   python detect_drowsiness.py --shape-predictor shape_predictor_68_face_landmarks.dat
   ```

3. Press `q` to exit the video stream window.

## 📂 Project Structure
```text
drowsiness_detection/
├── detect_drowsiness.py                    # Main detection script
├── shape_predictor_68_face_landmarks.dat  # Dlib 68 facial landmarks pre-trained model
├── Drowsiness detection.pdf               # Project documentation / paper
└── README.md                               # Project documentation
```

## ⚙️ How It Works
1. **Face Detection & Landmark Extraction:** Grabs webcam frames, converts them to grayscale, and locates facial landmarks (specifically left eye indices 36–41 and right eye indices 42–47).
2. **EAR Thresholding:** Calculates `EAR = (||p2-p6|| + ||p3-p5||) / (2 * ||p1-p4||)`. If the average EAR drops below `0.20` for `10` consecutive frames, drowsiness is flagged.
3. **Alert Trigger:** The system displays `DROWSINESS ALERT!` on the frame and triggers a voice alert.
