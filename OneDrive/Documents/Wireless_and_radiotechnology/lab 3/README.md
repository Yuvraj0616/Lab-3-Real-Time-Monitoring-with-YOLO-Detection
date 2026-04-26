# Intelligent Home Monitoring System

## Lab 3 - YOLO Object Detection on Live Video Stream

### Overview
This project implements a simple intelligent home monitoring system using a client-server architecture. One laptop acts as a camera node streaming live video, while another laptop acts as an AI monitoring node that receives the stream and runs YOLO object detection.

---

## Team Members

| Role | Name |
|------|------|
| Laptop A (Camera/Sender) | [Partner 1 Name] |
| Laptop B (AI Node/Receiver) | [Partner 2 Name] |

---

## System Architecture

```
Laptop A (Camera)          Network           Laptop B (AI Node)
┌──────────────┐                           ┌──────────────┐
│   Webcam     │    WiFi Network           │   YOLO       │
│   Capture    │ ───────────────────────► │   Detection  │
│              │    Video Stream           │              │
│  Flask App   │    (HTTP MJPEG)          │  OpenCV +    │
│  Port 5000   │                           │  Ultralytics │
└──────────────┘                           └──────────────┘
```

---

## Sender IP Address

**Laptop A IPv4 Address:** `192.168.1.20`

**Stream URL:** `http://192.168.1.20:5000/video_feed`

---

## How to Run

### Part 1: Start the Video Stream (Laptop A)

1. Install required packages:
   ```bash
   pip install opencv-python flask
   ```

2. Run the Flask streaming application:
   ```bash
   python app.py
   ```

3. The stream will be available at `http://192.168.1.20:5000/`

### Part 2: Run YOLO Detection (Laptop B)

1. Install required packages:
   ```bash
   pip install opencv-python ultralytics
   ```

2. Update the `STREAM_URL` in `yolo_stream.py` with the actual IP address of Laptop A

3. Run the YOLO detection program:
   ```bash
   python yolo_stream.py
   ```

4. Press `q` to quit the application

---

## Objects Detected

During testing, the following objects were detected:

| Object Class | Confidence | Notes |
|--------------|------------|-------|
| Person       | High       | Detected when person in frame |
| Chair        | Medium     | Indoor scenes |
| Remote       | Medium     | On tables/couches |
| Cup/Glass    | Low-Medium | Various angles |
| Laptop       | High       | When working at desk |
| Phone        | Medium     | Handheld detection |

---

## Files Included

| File | Description |
|------|-------------|
| `app.py` | Flask server that captures webcam and streams video over HTTP |
| `yolo_stream.py` | YOLO detection client that receives stream and performs object detection |
| `README.md` | This documentation file |

---

## Problems and Fixes

### Issue 1: Stream URL Incorrect
- **Problem:** Could not connect to the stream
- **Fix:** Verified IP address using `ipconfig` on Laptop A and updated `STREAM_URL` in `yolo_stream.py`

### Issue 2: Firewall Blocking
- **Problem:** Connection refused errors
- **Fix:** Allowed Python through Windows Firewall or disabled firewall temporarily

### Issue 3: Webcam Already in Use
- **Problem:** "Could not open webcam" error
- **Fix:** Closed other applications using the webcam (Zoom, Teams, etc.)

### Issue 4: YOLO Model Not Found
- **Problem:** FileNotFoundError for yolov8n.pt
- **Fix:** The model downloads automatically on first run. Ensure internet connection is available

---

## Testing Verification

- ✅ Laptop A streams video correctly
- ✅ Laptop B receives the stream
- ✅ YOLO runs on incoming frames
- ✅ At least one object is detected and displayed
- ✅ System behaves like an intelligent monitoring system

---

## What This Lab Teaches

This lab demonstrates a simple AI-enabled IoT monitoring pipeline:

**Camera Node → Network Stream → AI Processing Node → Detection Output**

This is similar to real systems such as:
- Smart home cameras
- Intelligent baby monitors
- Warehouse monitoring systems
- Traffic monitoring solutions

---

## Screenshots

*(Add screenshots here showing:)*

1. Flask stream running on Laptop A
2. YOLO detection window on Laptop B

---

## License

This project is for educational purposes as part of the Wireless and Radiotechnology lab.