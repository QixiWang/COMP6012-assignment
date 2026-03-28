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
```

---

## Dataset Description

The project uses a dataset containing corresponding **blurred**, **deblurred**, and **sharp/reference** images for object detection analysis.

The processed dataset is organised into:
- blur domain
- deblur domain
- sharp domain

Each domain is split into:
- train
- val
- test

This consistent split allows fair comparison of object detection performance across different image conditions using matched image content.

## Method Summary

### 1. Restoration Baselines
Two simple restoration baselines were explored:
- Unsharp masking
- Wiener filtering

These methods were first tested on sample images and then evaluated across a batch using:
- MSE
- PSNR
- SSIM

### 2. Pretrained Object Detection
A pretrained **YOLOv8n** detector was applied to:
- blurred images
- unsharp-masked images

This was used to test whether a simple restoration step could improve downstream detection before any retraining.

### 3. Processed Dataset Construction
A processed dataset was prepared for training and evaluation:
- unsharp masking outputs were used as the deblurred domain
- train / validation / test splits were created
- pseudo-labels were generated from the sharp images
- YAML files were created for each domain
### 4. Fine-Tuning
A YOLOv8n model was fine-tuned on the deblurred training set, then evaluated on:
- blur test set
- deblur test set
- sharp test set

This makes it possible to compare cross-domain performance after training on restored images.

---

## Main Results Summary

The notebook shows three main findings:

1. **Simple restoration baselines were limited**
   - Unsharp masking provided only minor visual enhancement
   - Wiener filtering performed poorly under the chosen assumptions

2. **Pretrained detection improved only slightly after simple restoration**
   - Unsharp masking gave small improvements in some cases
   - The gains were limited and not fully consistent

3. **Fine-tuning on the deblurred domain improved detection clearly**
   - The fine-tuned model outperformed the pretrained detector on the deblurred test set
   - The deblurred domain achieved the strongest precision and mAP results
   - The sharp domain achieved the strongest recall in the final evaluation

Overall, the results suggest that **domain adaptation through fine-tuning is more effective than relying only on simple restoration preprocessing**.

---

## How to Run

### 1. Clone the repository
```bash
git clone https://github.com/QixiWang/COMP6012-assignment.git
cd COMP6012-assignment
```

### 2. Create and activate a virtual environment
```bash
python -m venv venv
```

On Windows:
```bash
venv\Scripts\activate
```

On macOS / Linux:
```bash
source venv/bin/activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

If `requirements.txt` is not yet available, install the key libraries manually:
```bash
pip install jupyter numpy pandas matplotlib opencv-python scikit-image scipy ultralytics pyyaml
```

### 4. Ensure the dataset is placed correctly
Put the raw dataset into the `data/` folder and confirm that the processed dataset folders are available under `prepared_dataset/`.

### 5. Open the notebook
```bash
jupyter notebook
```

Then open:
```text
assignment1.ipynb
```

Run the notebook cells in order.

---

## Reproducibility Notes

To improve reproducibility, this repository includes:
- the main notebook used for the experiments
- processed dataset folders
- AI development logs
- YOLO training outputs and checkpoints

For best reproducibility, the following should be kept consistent:
- dataset paths
- train / validation / test split
- YOLO model version
- Python package versions
- random seeds where applicable

---

## Training Outputs

The YOLO fine-tuning outputs are stored in:

```text
runs/detect/runs_deblur_train/
```

This folder may contain:
- training logs
- result figures
- validation summaries
- best model checkpoints

---

## AI Usage Log

This project used AI assistance during development for:
- debugging
- code refinement
- markdown improvement
- explanation drafting

AI interaction records are stored in:

```text
ai_logs/
```

All final code, analysis and conclusions were checked and adapted for the assignment context.

---

## Ethics, Limitations and Bias

### Ethics
This project uses AI tools to support coding and writing.  
AI-generated suggestions were reviewed, modified and validated before being included in the final submission.

### Limitations
This project has several limitations:
- restoration methods were relatively simple baselines
- pseudo-labels were automatically generated rather than manually annotated
- the dataset size was limited
- the final detector was trained on a single restored domain rather than multiple restoration settings

### Bias and Validity
The results may be affected by:
- errors in pseudo-label generation
- domain shift between blur, deblur and sharp images
- model bias inherited from the pretrained YOLO weights
- metric sensitivity to dataset composition and object scale

Therefore, the findings should be interpreted as an experimental comparison rather than a universal conclusion about all deblurring pipelines.

---

## Attribution

This project uses:
- **YOLOv8n** from the Ultralytics framework for object detection
- standard image quality metrics including **MSE**, **PSNR** and **SSIM**
- Python libraries for image processing, evaluation and visualisation

Please refer to the corresponding package documentation for full implementation details and licensing information.

---

## Deliverables Included

This repository supports the main assignment deliverables:
- notebook / source code
- processed dataset structure
- AI usage log
- Git version history
- training outputs

Additional written report and presentation slides are prepared separately as required by the assignment.

---

## Author

Xiang Lu  
University of Adelaide
