isionTrack Experiment Log

## Experiment 3 — Fine-tune 15 (epochs), lr0=0.0001

### Objective
Evaluate fine_tuned YOLO11n on the Penn-Fudan
Pedestrian Dataset for 15 epochs, lr0=0.0001.

### Model
finetune_15_epochs_low_lr.

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
epochs: 15
lr0: 0.0001

### Metrics
Precision: 0.92
Recall: 0.95
mAP50: 0.98
mAP50-95: 0.79
Inference time: TBD

### Observations
Fine tuning reduced accuracy on validation set images. 

