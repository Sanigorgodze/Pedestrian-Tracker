# VisionTrack Experiment Log

## Experiment 0 — Pretrained Baseline

### Objective
Evaluate pretrained YOLO11n on the Penn-Fudan
Pedestrian Dataset before fine-tuning.

### Model
YOLO11n pretrained on COCO.

### Dataset
Penn-Fudan Pedestrian Dataset.

Training images: 119
Validation images: 25
Test images: 26

### Evaluation Configuration
Image size: 320
Batch size: 1
Device: CPU
Target class: person

### Metrics
Precision: 0.92
Recall: 0.97
mAP50: 0.98
mAP50-95: 0.84
Inference time: TBD

### Observations
To be completed after evaluation.

### Limitations
The model has 80 original COCO classes.
Our dataset contains one class.

Evaluation class mapping must be verified.