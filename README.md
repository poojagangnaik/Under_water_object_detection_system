# Underwater Object Detection System

> An IoT-based real-time underwater object detection system using YOLO11, OpenCV, Raspberry Pi 4, and ESP32 — capable of identifying marine debris, aquatic objects, and submerged structures from live camera feeds.

---

## Overview

Underwater environments are difficult to monitor continuously — poor visibility, high equipment costs, and limited accessibility make traditional inspection methods impractical. This project tackles that with a low-cost, automated pipeline: a waterproof camera captures live underwater footage, a Raspberry Pi runs real-time YOLO inference at the edge, and an ESP32 handles IoT communication to trigger local alerts and transmit results to a remote dashboard.

The model is a custom-trained YOLO11n fine-tuned on an annotated underwater dataset of 8 object classes, annotated using Label Studio and trained on Google Colab.

---

## Detected Classes

The model detects 8 object categories:

| ID | Class |
|---|---|
| 0 | Green Leaf |
| 1 | Metal Key |
| 2 | Plastic Car |
| 3 | Plastic Fish |
| 4 | Plastic Waste |
| 5 | Sea Shell |
| 6 | Wooden Bangle |
| 7 | Wooden Block |

---

## System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    Underwater Environment                │
│   Waterproof Camera  ──▶  Live Video Feed               │
└────────────────────────────┬────────────────────────────┘
                             │
                    ┌────────▼────────┐
                    │  Raspberry Pi 4 │
                    │  YOLO11n model  │
                    │  OpenCV + cvzone│
                    │  Edge Inference │
                    └───┬─────────┬───┘
                        │         │
              ┌─────────▼──┐  ┌───▼──────────────┐
              │   Monitor  │  │  ESP32            │
              │ Bounding   │  │  IoT Comms (MQTT) │
              │ boxes +    │  │  LCD Alert        │
              │ confidence │  │  Buzzer           │
              └────────────┘  └───────┬───────────┘
                                      │
                           ┌──────────▼──────────┐
                           │   Remote Dashboard  │
                           │  Wireless Monitoring│
                           └─────────────────────┘
```

---

## Workflow

```
Dataset Collection (underwater images & videos)
        ↓
Annotation using Label Studio
        ↓
Model Training — YOLO11n on Google Colab
  !yolo task=detect mode=train model=yolo11n.pt
       data=data.yaml epochs=20 imgsz=240
        ↓
Export best.pt → deploy on Raspberry Pi
        ↓
Real-time inference via OpenCV (every 3rd frame)
        ↓
Serial communication → ESP32 → LCD + Buzzer
        ↓
IoT transmission → Remote Dashboard
```

---

## Repository Structure

```
underwater-object-detection/
│
├── best.pt                                            # Trained YOLO11n model weights
├── classes.txt                                        # 8 detection class names
├── coco.obj.txt                                       # COCO-format class list
├── notes.json                                         # Label Studio category metadata
│
├── Yolo11WatObj8-checkpoint.ipynb                     # Real-time detection on Raspberry Pi
├── Yolo11CustomImgModelTrainWatObj8-checkpoint.ipynb  # Model training on Google Colab
├── CameraTestVideoSave-checkpoint.ipynb               # Camera test + video recording
│
└── docs/
    └── Under Water Proj Doc.docx                      # Full project documentation
```

---

## Hardware Requirements

| Component | Specification |
|---|---|
| Raspberry Pi 4 | 4GB RAM |
| ESP32 | Microcontroller for IoT comms |
| Waterproof Camera | USB / CSI, rated for underwater use |
| LCD Display | Status alerts |
| Power Supply | Battery pack for portable deployment |
| MicroSD Card | 16GB+ for OS and model |
| Jumper wires | For ESP32 connections |

---

## Software Requirements

| Tool / Library | Purpose |
|---|---|
| Raspberry Pi OS | Edge device OS |
| Python 3 | Primary language (Pi) |
| Arduino C | ESP32 firmware |
| Ultralytics YOLO | Object detection framework |
| OpenCV | Video capture and frame rendering |
| cvzone | Bounding box overlay utilities |
| NumPy | Array operations |
| PySerial | Serial communication to ESP32 |
| MQTT / HTTP | IoT data transmission |
| Label Studio | Dataset annotation |
| Arduino IDE | ESP32 firmware upload |
| Thonny | Python IDE for Raspberry Pi |
| Google Colab | Model training environment |

---

## Setup & Run

### 1. Train the model (Google Colab)

```python
# Install ultralytics
!pip install ultralytics

# Mount Google Drive and extract dataset
from google.colab import drive
drive.mount('/content/gdrive')
!unrar x "/content/gdrive/MyDrive/YoloImgTrainVal.rar" "/content/datasets/"

# Train YOLO11n
!yolo task=detect mode=train model=yolo11n.pt \
      data=/content/datasets/YoloImgTrainVal/data.yaml \
      epochs=20 imgsz=240 plots=True
```

Copy the output `best.pt` to the Raspberry Pi.

### 2. Test the camera

Run `CameraTestVideoSave-checkpoint.ipynb` on the Raspberry Pi to verify the camera is recognised and recording correctly before deployment.

### 3. Run real-time detection

Run `Yolo11WatObj8-checkpoint.ipynb` on the Raspberry Pi:

```python
from ultralytics import YOLO
import cv2, serial

model = YOLO("best.pt")
cap = cv2.VideoCapture(0)

while True:
    ret, frame = cap.read()
    frame = cv2.flip(frame, 1)
    results = model.track(frame, persist=True, imgsz=256)
    # render results + serial output to ESP32
```

Detection runs on every 3rd frame to maintain real-time performance on the Pi.

---

## Results

- Real-time detection achieved on Raspberry Pi 4 with low latency edge inference
- 8-class custom model trained in 20 epochs on a lightweight YOLO11n backbone
- Detection performance degrades with increasing water turbidity and low light — expected for vision-only systems
- Best results in clear water with direct or diffused lighting

---

## Applications

- Marine debris and pollution monitoring
- Coral reef and aquatic ecosystem observation
- Underwater surveillance and safety
- Aquaculture and fisheries management
- Oceanographic research
- Underwater archaeology and exploration

---

## Future Enhancements

- Larger annotated dataset for improved accuracy and class diversity
- Low-light and high-turbidity model adaptations
- Sonar sensor fusion for non-visual detection
- Object tracking across frames
- Cloud-based analytics and detection logging
- Human/diver detection for safety and rescue operations
- Integration with autonomous underwater vehicles (AUVs)

---

## Team

| Name | Roll No. |
|---|---|
| Pooja Mahesh Gangnaik | 1BI22EC107 |
| Prakruthi G | 1BI22EC110 |
| Nidhi V | 1BI22EC096 |
| Pooja B M | 1BI22EC106 |

**Guide:** Swathi — Assistant Professor, Dept. of ECE, BIT Bangalore

---

## References

- IEEE — Underwater Monitoring Systems
- Automatic Fish Detection using Machine Learning
- IoT-Based Marine Litter Detection
- Improved YOLO-based Underwater Object Detection
- AIoT-based Underwater Trash Management
- [Ultralytics YOLO Documentation](https://docs.ultralytics.com)
