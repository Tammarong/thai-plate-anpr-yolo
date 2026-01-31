
# ThaiPlate-ANPR-YOLO 🇹🇭🚗
Automatic Number Plate Recognition (ANPR) system for Thai license plates using YOLO.

This repository focuses on **license plate detection** from vehicle images and provides
a ready-to-run notebook for inference using a trained YOLO model.

---

## Features
- Detect Thai license plates from car images
- YOLO-based detection model
- Easy-to-use Jupyter Notebook
- Ready for OCR pipeline integration

---

## Sample Images
Example test images are provided in the `assets/` folder:
- `test_image.jpg`
- `test_2.jpg`
- `test_3.jpeg`

---

## Setup

### 1. Create a virtual environment (recommended)
```bash
python -m venv .venv
source .venv/bin/activate      # macOS / Linux
# .venv\Scripts\activate       # Windows
2. Install dependencies
pip install -r requirements.txt
Run Inference (Notebook)
Open and run:

Anpr.ipynb
Make sure the paths are correct:

Model weights: weights/best.pt

Input images: assets/

Output directory: outputs/
