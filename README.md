# Detection of Helmet Usage Variants from Surveillance Cameras Using Deep Learning Based Methods

Bachelor's Thesis — Informatics, Telkom University (2025)  
Published on Telkom University Open Library

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

Dataset available on Roboflow: [insert link]

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

| Metric | Validation | Testing |
|---|---|---|
| mAP@50 | 0.984 | 0.985 |
| mAP@50-95 | 0.819 | 0.802 |
| Precision | 0.953 | 0.955 |
| Recall | 0.952 | 0.960 |
| F1-Score | 0.953 | 0.958 |

---

## Requirements

[Fill in once you check your code files]

---

## How to Run

[Fill in based on your actual code]
