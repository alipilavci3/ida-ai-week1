# IDA Buoy Detection – Perception Module (Week 1)

## Project Goal

This project implements a computer vision–based **buoy detection perception module** for an unmanned surface vehicle (IDA).
The goal is to detect buoys from camera images and output their locations as bounding boxes, providing input to higher-level autonomy and navigation modules.

---

## System Overview

**Pipeline:**

```
Camera Image → Preprocessing → Object Detection Model → Bounding Boxes (+ Count)
```

* The system focuses only on **perception** (no decision-making or control).
* Outputs are intended to be consumed by downstream autonomy logic.

---

## Dataset

* **Source:** Roboflow Universe
  Workspace: `alipilavci3`
  Project: `ida-ai-week1-2`
  Version: `3`
* **Format:** YOLO (train / valid / test folders + `data.yaml`)
* **Classes:** 1 class → `buoy`
* **Split sizes:**

  * Train: 84 images
  * Validation: 6 images
  * Test: 3 images
  * **Total:** 93 images
* **License:** CC BY 4.0
* **Storage:** Dataset is kept locally under `data/buoy-dataset/` and is not tracked by git (to avoid large files).

---

## Data Organization

```
data/
└── buoy-dataset/
    ├── train/
    │   ├── images/
    │   └── labels/
    ├── valid/
    │   ├── images/
    │   └── labels/
    ├── test/
    │   ├── images/
    │   └── labels/
    └── data.yaml
```

---

## Model

* **Model type:** RF-DETR Nano (Transformer-based object detection)
* **Platform:** Roboflow
* **Task:** Single-class object detection (buoy)
* **Rationale:** Chosen for stability on small objects and tolerance to limited datasets.

---

## Training & Inference

* Training was performed on **Roboflow Cloud**.
* Inference outputs include:

  * Bounding box coordinates
  * Class label (`buoy`)
  * Confidence score
* Threshold tuning was used to reduce null predictions during testing.

---

## Results (Qualitative)

* Successful detections on clear and nearby buoys.
* Missed detections on very small or distant buoys.
* Occasional confusion with visually similar objects (e.g., boats).
* Overall behavior reflects dataset size and class imbalance constraints.

---

## Limitations

* Small dataset size limits generalization.
* Single-class setup does not explicitly handle confusing objects.
* No temporal filtering or tracking is applied.

---

## Future Work

* Expand dataset with real-world maritime images.
* Introduce multi-class detection (buoy + boat).
* Integrate perception output with autonomy and collision-avoidance logic.
* Evaluate larger models or alternative backbones.

---

## Repository Structure

```
ida-ai-week1/
├── data/        # Local dataset (not tracked by git)
├── src/         # Training and inference scripts
├── models/      # Model metadata / weights (not tracked by git)
└── README.md
```
