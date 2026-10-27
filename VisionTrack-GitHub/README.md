# VisionTrack

### End-to-End Pedestrian Detection Using YOLO11n

VisionTrack is a computer vision project developed to demonstrate a complete machine learning workflow, including dataset preparation, model fine-tuning, evaluation, optimization, and deployment.

The project uses YOLO11n to detect pedestrians in photographs and provides a web interface where users can upload images and visualize detections.

## 1. Features

- Pedestrian detection using YOLO11n.
- Penn-Fudan pedestrian dataset preprocessing.
- Conversion of segmentation masks into YOLO bounding-box annotations.
- Model fine-tuning and comparison experiments.
- Precision, recall, and mAP evaluation.
- Inference speed benchmarking.
- Visual error analysis.
- FastAPI REST API.
- HTML, CSS, and JavaScript web interface.
- Automated API tests.

## 2. Technology Stack

**Programming language:** Python 3.12

**Machine learning:** PyTorch, Ultralytics YOLO11n

**Computer vision:** OpenCV, NumPy

**Visualization:** Matplotlib

**Backend:** FastAPI, Uvicorn

**Frontend:** HTML, CSS, JavaScript

**Development environment:** Ubuntu Linux

## 3. Dataset

The project uses the Penn-Fudan Pedestrian Dataset.

The dataset contains 170 images and corresponding instance-segmentation masks.

The dataset is divided into:

| Split | Images |
|---|---:|
| Training | 119 |
| Validation | 25 |
| Testing | 26 |

The split is generated using random seed 42.

### Download and prepare the dataset

From the project directory:

```bash
mkdir -p data/raw

wget https://www.cis.upenn.edu/~jshi/ped_html/PennFudanPed.zip \
-O data/raw/PennFudanPed.zip

unzip data/raw/PennFudanPed.zip -d data/raw/
```

Prepare the YOLO annotations:

```bash
python src/prepare_dataset.py
```

The script converts the segmentation masks into normalized YOLO bounding-box labels.

Visualize annotations:

```bash
python src/visualize_labels.py
```

Check annotation validity:

```bash
python src/check_labels.py
```

## 4. Installation

Clone the repository:

```bash
git clone <REPOSITORY_URL>
cd visiontracker
```

Create a virtual environment:

```bash
python3 -m venv ml_venv
source ml_venv/bin/activate
```

Install dependencies:

```bash
python -m pip install -r requirements.txt
```

The application runs on CPU, so CUDA is not required.

The pretrained YOLO11n weights are obtained through Ultralytics when needed.

## 5. Model Training

The project uses pretrained YOLO11n weights as the starting point for fine-tuning.

The following experiments were performed:

| Experiment | Epochs | Learning rate |
|---|---:|---:|
| Original pretrained model | 0 | — |
| Fine-tuning A | 5 | 0.001 |
| Fine-tuning B | 5 | 0.0001 |

Training configuration:

- Image size: 320
- Batch size: 2
- Optimizer: AdamW
- Device: CPU
- Random seed: 42

Run the training script:

```bash
python src/train.py
```

The training script's settings determine which fine-tuning experiment is reproduced.

## 6. Model Evaluation

Evaluate the pretrained baseline:

```bash
python src/evaluate_baseline.py
```

Compare available model checkpoints:

```bash
python src/compare_models.py
```

Run visual error analysis:

```bash
python src/error_analysis.py
```

Run the final test evaluation:

```bash
python src/final_test.py
```

### Validation results

| Model | Precision | Recall | mAP50 | mAP50-95 |
|---|---:|---:|---:|---:|
| Pretrained YOLO11n | 0.9229 | 0.9701 | 0.9862 | 0.8458 |
| Fine-tuned, LR 0.001 | 0.9474 | 0.9254 | 0.9782 | 0.7353 |
| Fine-tuned, LR 0.0001 | 0.9124 | 0.9701 | 0.9834 | 0.7677 |

The pretrained model achieved the highest validation mAP50-95.

## 7. Optimization

The pretrained model was evaluated at three input resolutions on an Intel Core i5-8250U CPU.

| Resolution | mAP50-95 | Inference time |
|---|---:|---:|
| 320 | 0.8458 | 26.48 ms |
| 416 | 0.8584 | 39.81 ms |
| 640 | 0.9050 | 126.77 ms |

Reducing the resolution from 640 to 320 decreased inference latency substantially, at the cost of reduced bounding-box localization accuracy.

The 320 resolution was selected for the application.

These measurements represent model inference time, not complete API response time.

## 8. Final Test Results

The selected model was evaluated on 26 held-out test images.

| Metric | Result |
|---|---:|
| Precision | 0.9199 |
| Recall | 0.9091 |
| mAP50 | 0.9449 |
| mAP50-95 | 0.7647 |
| Inference time | 34.43 ms |

These results provide an estimate of performance on unseen Penn-Fudan images.

## 9. Web Application

Start the FastAPI server:

```bash
uvicorn src.api:app --host 127.0.0.1 --port 8000
```

Open the visual interface:

`http://127.0.0.1:8000/`

The application allows users to upload an image and displays:

- Original photograph.
- Image with pedestrian bounding boxes.
- Detected pedestrian count.
- Processing time.

### API documentation

FastAPI's interactive documentation is available at:

`http://127.0.0.1:8000/docs`

### API endpoints

`GET /health`

Returns application status and model information.

`POST /predict`

Accepts a JPEG or PNG image and returns pedestrian bounding boxes, confidence scores, detection count, processing time, and an annotated image.

## 10. Automated Tests

Run:

```bash
python -m pytest tests/ -v
```

The tests check the homepage, health endpoint, invalid image handling, and pedestrian detection response structure.

## 11. Source Code Overview

| File | Purpose |
|---|---|
| `explore_dataset.py` | Inspect original images and masks |
| `prepare_dataset.py` | Generate YOLO-compatible annotations |
| `visualize_labels.py` | Display ground-truth bounding boxes |
| `check_labels.py` | Validate annotation coordinates |
| `predict.py` | Run pretrained model inference |
| `train.py` | Fine-tune YOLO11n |
| `evaluate_baseline.py` | Evaluate original pretrained model |
| `evaluate.py` | Evaluate a selected fine-tuned checkpoint |
| `compare_models.py` | Compare model performance |
| `error_analysis.py` | Generate visual prediction comparisons |
| `benchmark.py` | Measure accuracy and inference latency |
| `final_test.py` | Evaluate the selected model on test images |
| `api.py` | Serve pedestrian detection through FastAPI |
| `static/index.html` | Provide the graphical user interface |
| `tests/test_api.py` | Test backend application behavior |

## 12. Limitations

- The dataset is relatively small.
- Some visible pedestrians may not be individually annotated.
- Performance may differ on other cameras, environments, and lighting conditions.
- The current implementation uses CPU inference.
- No large-scale real-world deployment testing was performed.
- The current application processes uploaded images rather than continuous video.

## 13. Future Improvements

Potential improvements include:

- Training on larger and more diverse datasets.
- More extensive error analysis.
- ONNX Runtime inference.
- Video and webcam support.
- Model monitoring.
- Production API performance and security testing.

## 14. AI Assistance Disclosure

ChatGPT was used to support the development of VisionTrack, including explanations of machine learning concepts, Python implementation guidance, debugging, experiment planning, and documentation.

The project was developed through an iterative workflow involving manual implementation, execution, inspection of outputs, and evaluation of model performance.

All reported metrics come from actual experiments rather than AI-generated estimates.

## 15. Project Purpose

VisionTrack was developed as an end-to-end computer vision engineering project for the Upgaming Machine Learning Engineer technical assignment.