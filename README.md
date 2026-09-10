# Drowsiness Detection System

## 📋 Project Description
The **AI-Based Drowsiness Detection System** is a real-time computer vision application designed to prevent accidents caused by driver fatigue or sleepiness. Using live video feeds from a webcam, the system identifies human faces, extracts facial landmarks around the eyes, and continuously computes the **Eye Aspect Ratio (EAR)**. When a driver's eyes remain closed below a predetermined threshold for a specified duration, the system triggers real-time visual warnings on the screen along with an audible voice alert ("Alert! DROWSINESS ALERT!").

---

## 📌 Features
- **Real-Time Facial Landmark Tracking:** Detects 68 facial landmark coordinates using `dlib`'s HOG-based face detector.
- **Eye Aspect Ratio (EAR) Calculation:** Computes the Euclidean distance between vertical and horizontal eye landmarks to accurately track eye closure.
- **Voice & Visual Alarms:** Plays voice notifications via text-to-speech (`pyttsx3`) and displays high-visibility warning overlays on the video stream when drowsiness is detected.
- **Multi-Threaded Video Stream:** Utilizes `imutils.video.VideoStream` for smooth, low-latency camera frame processing.

---

## 🛠️ Prerequisites & Dependencies
Make sure you have Python installed on your system. Install the required Python dependencies:

```bash
pip install opencv-python dlib imutils scipy pyttsx3
```

> **Note on Dlib:** Installing `dlib` requires C++ build tools (CMake). On Windows, ensure CMake and Visual Studio C++ Build Tools are installed prior to running `pip install dlib`.

---

## 🚀 How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/Harshitha-2121/drowsiness_detection.git
   cd drowsiness_detection
   ```

2. Run the detection script with the pre-trained landmark predictor model:
   ```bash
   python detect_drowsiness.py --shape-predictor shape_predictor_68_face_landmarks.dat
   ```

3. Press `q` while focused on the video window to stop detection and exit.

---

## 📂 Project Structure
```text
drowsiness_detection/
├── detect_drowsiness.py                    # Main Python detection script
├── shape_predictor_68_face_landmarks.dat  # Dlib 68 facial landmarks pre-trained model file
├── Drowsiness detection.pdf               # Project documentation / presentation PDF
└── README.md                               # Comprehensive project documentation
```

---

## ⚙️ Algorithm & Workflow
1. **Face Detection & Landmark Extraction:** Grabs webcam frames, converts them to grayscale, and locates facial landmarks (specifically left eye indices 36–41 and right eye indices 42–47).
2. **EAR Thresholding:** Calculates the Eye Aspect Ratio:
   $$\text{EAR} = \frac{||p_2 - p_6|| + ||p_3 - p_5||}{2 \times ||p_1 - p_4||}$$
   If the averaged EAR for both eyes drops below `0.20` for `10` consecutive frames, drowsiness is flagged.
3. **Alert Trigger:** The system displays `DROWSINESS ALERT!` on the frame and triggers a voice alert using `pyttsx3`.
