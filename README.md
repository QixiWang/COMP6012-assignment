# COMP6012 Assignment 1

## Project Title
Image Restoration and Object Detection under Motion Blur

## Project Overview
This project investigates whether simple image restoration can improve downstream object detection performance on motion-blurred images.

The work is organised into three main stages:

1. **Image restoration**
   - Apply simple deblurring / sharpening baselines to blurred images
   - Evaluate restoration quality using MSE, PSNR and SSIM

2. **Object detection analysis**
   - Apply a pretrained YOLOv8n detector to blurred and restored images
   - Compare detection counts, confidence scores and qualitative detection results

3. **Domain-specific fine-tuning**
   - Build a processed dataset with blur, deblur and sharp domains
   - Generate pseudo-labels from the sharp images
   - Fine-tune YOLOv8n on the deblurred training set
   - Evaluate the fine-tuned model on blur, deblur and sharp test sets

The main notebook for the assignment is `assignment1.ipynb`.

---

## Repository Structure

```text
COMP6012-assignment/
├── ai_logs/                         # AI prompt / output records used during development
├── data/                            # Original dataset files
├── prepared_dataset/                # Processed dataset with train/val/test splits
├── runs/
│   └── detect/
│       └── runs_deblur_train/       # YOLO training outputs, logs, checkpoints
├── assignment1.ipynb                # Main notebook for the assignment
├── yolov8n.pt                       # Pretrained YOLOv8n weights
├── README.md                        # Project documentation
└── .gitignore

---
## Dataset Description

The project uses a dataset containing corresponding blurred, deblurred, and sharp/reference images for object detection analysis.

The processed dataset is organised into:

blur domain
deblur domain
sharp domain

Each domain is split into:

train
val
test

This consistent split allows fair comparison of object detection performance across different image conditions using matched image content.
