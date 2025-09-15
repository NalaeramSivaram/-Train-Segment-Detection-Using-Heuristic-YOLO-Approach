# 🚂 Train-Segment-Detection-Using-Heuristic-YOLO-Approach
This repository contains a Python-based project that detects and counts train segments—Engines, Wagons, and Brakevans—from side-view train videos using a heuristic approach with YOLO. The solution works without requiring custom training.

## Project Overview ##
The goal of this project is to automatically analyze train videos and estimate the **number of engines, wagons, and brakevans.**
Since no labeled dataset was available for train components, a **heuristic method** was developed using the **pretrained YOLOv8 model** (trained on COCO) to detect general train objects and estimate the train composition.

### How It Works ###
**Step 1: Frame Extraction**

  *  The input train video is split into individual frames.
  *  Frames are extracted at a regular interval (e.g., every 30 frames) to reduce computation.
  *  Extracted frames are saved for processing and optional annotation.

**Step 2: YOLO Detection**

  *  A pretrained YOLOv8 model (yolov8n.pt) is used to detect objects in each frame.
  *  Since YOLO does not know about "engine" or "brakevan" by default, the model detects train objects.

**Step 3: Heuristic Counting**

  *  A  The detected train bounding boxes are sorted left-to-right in each frame.
  *  Counting rules:
        Engine → first bounding box in the frame (front of the train).
        Brakevan → last bounding box in the frame (end of the train).
        Wagons → all intermediate bounding boxes.
This allows approximate counting of train components without requiring labeled data or custom YOLO training.

**Step 4: Annotated Frames**

  *  Each detected train segment is optionally annotated with bounding boxes.
  *  Annotated frames can be saved for visualization or further analysis.

**Step 5: Report Generation**
     
    A PDF report summarizes:
  *  Count of engines, wagons, and brakevans
  *  Total segments detected
  *  Visual bar chart of distribution
    A performance summary text file is also generated.

A performance summary text file is also generated.
