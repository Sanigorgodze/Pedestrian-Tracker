# VisionTrack Experiment Log

## Experiment 1 — Fine-tune 5 (epochs), lr0=0.001

### Objective
Evaluate fine_tuned YOLO11n on the Penn-Fudan
Pedestrian Dataset for 5 epochs, lr0=0.001.

### Model
finetune_5_epochs.

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
lr0: 0.01
epochs:5

### Metrics
Precision: 0.94
Recall: 0.95
mAP50: 0.97
mAP50-95: 0.73
Inference time: TBD

### Observations
Fine tuning reduced accuracy on validation set images. 

