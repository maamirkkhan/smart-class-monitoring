# 🎓 Smart Class Monitoring

An AI-powered classroom monitoring system that uses facial recognition and phone detection to automate attendance tracking with high accuracy.
---

## Table of Contents
- [Overview]
- [Features]
- [1. Student Registration]
- [2. Face Recognition]
- [3. Phone Detection]
- [4. Attendance Management]
- [System Requirements]
- [Software Requirements]
- [Installation Guide]
- [HOW TO RUN]
- [Step A: Student Registration]
- [Step B: Train the Model]
- [Step C: Take Attendance]
- [Step D: View Records]


---

## Overview

This system provides a complete solution for classroom management:

- **Automated Attendance**: Mark attendance using facial recognition
- **Phone Detection**: Detect phone usage during class sessions  
- **Student Registration**: Easy face capture from multiple angles
- **Record Management**: Export attendance data to CSV
- **Multi-Subject Support**: Handle different subjects and time slots

Each student gets their own trained model, ensuring high accuracy and minimal false matches.


---

## Features

### 1. Student Registration
- Capture face images from **5 angles** (Front, Left, Right, Up, Down)
- **2500 images** captured per student for maximum accuracy
- Automatic naming with `EnrollmentID_Name` format
- No bounding boxes saved in images (clean face data)

### 2. Face Recognition
- **InsightFace buffalo_s** for accurate face detection at distance
- **LBPH** (Local Binary Pattern Histogram) for recognition
- **Per-student models** - each student has their own `Trainer_<ID>.yml`
- **confidence threshold** (adjustable)
- **640×640** detection size for classroom distance

### 3. Phone Detection
- **Custom trained model (`best.pt`)
- Pre-trained model yolo11l.pt
- Real-time phone detection during attendance
- Automatic screenshots when phone detected

### 4. Attendance Management
- Subject-wise attendance tracking
- **3 time slots** per session (e.g., 08:00, 09:00, 10:00)
- 60-second window for each time slot
- CSV export for records
- Green box (registered) / Red box (unknown) visual feedback


---

## System Requirements

### Hardware Requirements
| Component | Minimum | Recommended |
|-----------|---------|-------------|
| RAM | 8 GB | 64 GB |
| Webcam | 720p | 1080p |

### Software Requirements
- **Operating System**: Windows 10/11
- **Python**
- **Editor**: VS Code (recommended)

### Python Dependencies
opencv-python
opencv-contrib-python
Pillow
pandas
numpy
insightface
onnxruntime
torch
ultralytics
tkinter


---

### Installation Guide
i-  git clone https://github.com/maamirkkhan/smart-class-monitoring.git
ii- cd smart-class-monitoring
iii- python -m venv .venv
iv- .venv\Scripts\activate
v- pip install -r requirements.txt


### Download the buffalo_s Model

i-  pip install insightface onnxruntime
ii- python -c "import insightface; from insightface.app import FaceAnalysis; app = FaceAnalysis(name='buffalo_s'); app.prepare(ctx_id=0)"


---

### HOW TO RUN

--- STEP A: STUDENT REGISTRATION ---
1. Open Command Prompt
2. cd D:\smart-class-monitoring
3. .venv\Scripts\activate
4. Run your app.py (e.g. python app.py)
5. In the GUI, go to Student Registration
6. Enter: Student Name and Roll Number (Enrollment ID)
7. Click "Take Images"
8. A webcam window opens. Follow the on-screen instructions:
   - Look STRAIGHT (500 images captured)
   - Turn face LEFT (500 images)
   - Turn face RIGHT (500 images)
   - Tilt face UP (500 images)
   - Tilt face DOWN (500 images)
   Total: 2500 clean face images saved (NO bounding boxes in saved images)
9. Dataset saved to: TrainingImage\<EnrollmentID>_<Name>\

--- STEP B: TRAIN THE MODEL ---
1. After registering, go to "Train Model" in the GUI
2. Click "Train Model"
3. The system will:
   - Read each student's folder in TrainingImage\
   - Create ONE personal model per student: Trainer_<ID>.yml
   - Also save combined Trainner.yml
4. Wait for "Training Complete" message

IMPORTANT: Re-train every time you add a new student.
           Each student gets their own model for accurate recognition.

--- STEP C: TAKE ATTENDANCE ---
1. Run the attendance module from the GUI
2. Enter Subject Name (e.g. "Mathematics")
3. A time slot selection window appears:
   - Choose 3 time slots (e.g. 08:00, 09:00, 10:00)
4. Click "Start Attendance"
5. Webcam opens automatically
6. PHONE DETECTION runs continuously from start to end
7. For each time slot:
   - System waits until that time
   - Then marks attendance for 60 seconds
   - Registered students → Green box + Name
   - Unknown persons  → Red box + "Unknown"
8. Attendance saved to: Attendance\<SubjectName>\<SubjectName>_<Date>_<Time>.csv

--- STEP D: VIEW RECORDS ---
1. Go to Records module in GUI
2. Select subject and record type
3. View attendance sheets (CSV/Excel)
4. View Screenshots of PHONE DETECTION