isionTrack Experiment Log

## Experiment 2 — Fine-tune 5 (epochs), lr0=0.0001

### Objective
Evaluate fine_tuned YOLO11n on the Penn-Fudan
Pedestrian Dataset for 5 epochs, lr0=0.0001.

### Model
finetune_5_epochs_low_lr.

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
epochs: 5
lr0 = 0.0001

### Metrics
Precision: 0.91
Recall: 0.97
mAP50: 0.98
mAP50-95: 0.76
Inference time: TBD

### Observations
Lowering learning rate did better job than higher learnng rate but still baseline pretrained model is beeter.

