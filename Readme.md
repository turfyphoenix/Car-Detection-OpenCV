# Car Detection Using OpenCV and Haar Cascade

A Python-based vehicle detection project that uses OpenCV and a Haar Cascade classifier to identify cars in video footage and highlight detected vehicles using bounding boxes.

## Project Overview

This project implements vehicle detection using a pretrained Haar Cascade classifier. It processes video footage frame by frame, identifies potential vehicles and draws rectangular bounding boxes around detected cars.

The primary objective was to understand traditional computer vision techniques, video processing and object detection using OpenCV.

## Technologies Used

- **Python** – Programming language
- **OpenCV** – Image and video processing
- **Haar Cascade** – Object detection
- **NumPy** – Numerical operations

## How It Works

The application follows these steps:

1. **Video Capture:** Reads the input video using `cv.VideoCapture()`.
2. **Frame Extraction:** Processes the video one frame at a time.
3. **Resizing:** Resizes each frame to the required resolution.
4. **Grayscale Conversion:** Converts BGR frames into grayscale using `cv.cvtColor()`.
5. **Vehicle Detection:** Uses `detectMultiScale()` to identify potential cars.
6. **Bounding Boxes:** Extracts vehicle coordinates and draws rectangles using `cv.rectangle()`.
7. **Video Display:** Displays the processed frames continuously until the user presses `Q`.

## Project Structure

```text
Car-Detection/
│
├── Videos/
│   └── carsmoving.mp4
│
├── cars.xml
├── main.py
└── README.md
```

## Installation and Setup

### 1. Clone the repository

```bash
git clone YOUR_REPOSITORY_URL
```

### 2. Navigate to the project directory

```bash
cd Car-Detection
```

### 3. Install dependencies

```bash
pip install opencv-python numpy
```

### 4. Add the required files

Ensure the following files are available:

- `cars.xml` – Haar Cascade classifier.
- `Videos/carsmoving.mp4` – Input video.

### 5. Run the project

```bash
python main.py
```

Press `Q` to close the video window.

## Implementation

The project uses OpenCV's `CascadeClassifier` and `detectMultiScale()` methods for vehicle detection.

```python
import cv2 as cv

cap = cv.VideoCapture('Videos/carsmoving.mp4')

car_cascade = cv.CascadeClassifier('cars.xml')

while True:
    ret, frame = cap.read()

    if not ret:
        print("Error loading the frame")
        break

    frame = cv.resize(frame, (1920, 1080))

    gray = cv.cvtColor(frame, cv.COLOR_BGR2GRAY)

    cars = car_cascade.detectMultiScale(
        gray,
        scaleFactor=1.2,
        minNeighbors=6
    )

    for (x, y, w, h) in cars:
        cv.rectangle(
            frame,
            (x, y),
            (x + w, y + h),
            (255, 0, 255),
            2
        )

    cv.imshow("Car Detection", frame)

    if cv.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv.destroyAllWindows()
```

## Detection Accuracy and Limitations

The detection results are not consistently accurate. Some vehicles may be missed, while certain background objects may occasionally be identified as cars.

These limitations are largely associated with the pretrained Haar Cascade classifier and its training data rather than necessarily indicating errors in the implementation.

### Factors Affecting Accuracy

**1. Training Data**

The classifier learns visual patterns from the positive and negative samples used during training. Its performance depends on the diversity and quality of those samples.

If the training dataset does not adequately represent different vehicle types, orientations, sizes and environmental conditions, detection performance can decrease.

**2. Camera Perspective**

The classifier may perform differently depending on the vehicle's orientation. A model trained primarily on side-view images may struggle with front-facing or rear-facing vehicles.

**3. Lighting and Background**

Shadows, varying illumination, low contrast and complex backgrounds can affect detection results.

**4. False Positives**

The classifier may occasionally identify background patterns or unrelated objects as vehicles.

**5. Missed Detections**

Actual vehicles may remain undetected when their appearance differs from the visual patterns learned during training.

### Why Parameter Tuning Cannot Solve Everything

Parameters such as `scaleFactor` and `minNeighbors` influence how the classifier searches for objects and accepts detections.

However, parameter adjustments cannot completely compensate for limitations in the original training dataset or the classifier itself.

Improving accuracy may require a more diverse training dataset and retraining the classifier.

**The key takeaway:** Imperfect detection does not automatically mean the implementation is incorrect. A correctly implemented detection pipeline can still produce inconsistent results because of limitations in its pretrained model.

## Future Improvements

- Experiment with different detection parameters.
- Test the classifier under different lighting conditions and camera perspectives.
- Implement vehicle counting.
- Explore vehicle tracking across consecutive frames.
- Train a more robust classifier using diverse vehicle images.
- Compare Haar Cascade with modern object detection models such as YOLO.

## Learning Outcomes

Through this project, I gained practical experience with:

- Reading and processing video frames.
- Working with OpenCV's video capture functionality.
- Grayscale image conversion.
- Haar Cascade classifiers.
- Object detection using `detectMultiScale()`.
- Extracting bounding box coordinates.
- Drawing rectangles around detected objects.
- Understanding the limitations of traditional computer vision techniques.

## Author

**Developed as part of my learning journey in Python and Computer Vision.**

**Project:** Car Detection using Haar Cascade  
**Language:** Python  
**Library:** OpenCV