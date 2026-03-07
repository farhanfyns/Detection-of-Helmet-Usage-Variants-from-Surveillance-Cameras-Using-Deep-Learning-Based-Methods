# Detection of Helmet Usage Variants from Surveillance Cameras Using Deep Learning Based Methods

Bachelor's Thesis — Informatics, Telkom University (2025)  
Published on Telkom University Open Library

Made by Farhan Faturahman

---

## Overview

Most existing helmet detection research only classifies riders into two categories: wearing a helmet or not. This project takes a more granular approach by detecting four distinct helmet usage classes that reflect real conditions on Indonesian roads, using low-resolution surveillance footage (480p and below).

**Detection Classes:**
- `helmet_fullface`
- `helmet_halfface`
- `helmet_nonstandard` (helmet without visor)
- `no_helmet`

---

## Dataset

Self-collected via DSLR camera configured to simulate surveillance camera conditions (480p resolution), recorded at the main roundabout gate of Telkom University during daytime in December 2024 – January 2025.

- Total frames: 1,118
- Total annotations: 1,944
- Camera angle: head-level (not overhead)
- Annotation and preprocessing: Roboflow (auto orientation, resized to 640x640)

Dataset split:
- Training: 70% (783 frames)
- Validation: 15% (168 frames)
- Testing: 15% (167 frames)

Dataset available on Roboflow: [4 Class Helmet Detection Dataset](https://universe.roboflow.com/dataset-ta-hroly/4-class-helmet-detection-dataset)

---

## Model

**YOLOv8n (Nano)** was used exclusively for its efficiency and fast inference, making it suitable for real-time detection on low-resolution footage.

Training configuration:
- Optimizer: AdamW
- Learning rate: 0.01
- Weight decay: 0.0005
- Image size: 640x640
- Epochs tested: 25, 50, 100
- Batch sizes tested: 4, 16, 32

---

## Results

Best configuration: **100 epochs, batch size 32**

| | Precision | Recall | F1-Score | mAP@50 | mAP@50-95 |
|---|---|---|---|---|---|
| Validation | 0.953 | 0.952 | 0.953 | 0.984 | 0.819 |
| Testing | 0.955 | 0.960 | 0.958 | 0.985 | 0.802 |

Full training results for all scenarios including weights, confusion matrices, F1 curves, and CSVs are available in the `Hasil Pengujian Epoch/` folder.

---

## Requirements

- Python 3.8+
- ultralytics
- pandas

Install dependencies:
```bash
pip install ultralytics pandas
```

---

## How to Run

1. Clone this repository and place your dataset folder containing `data.yaml` in the project directory
2. Update `base_path` to match your local directory:
```python
base_path = r"your\local\path\to\project"
```
3. Open the notebook for your desired scenario (e.g. `Epoch_100_Batch_32`) and run all cells to start training
4. After training, update `model_path` to point to the best weights generated from training:
```python
model_path = r"your\local\path\to\Epoch 100\Batch 32\train\weights\best.pt"
```
5. Run the evaluation cells to test the model on the test set and generate confusion matrix, F1 curve, and results CSV

Training results and model weights will be saved automatically to the specified `save_dir`.

**Inference on video:**
Update `model_path` and `video_path` in `Model_Inference` notebook and run all cells. Results will be saved automatically to an `inference_results` folder in the same directory as the video.
