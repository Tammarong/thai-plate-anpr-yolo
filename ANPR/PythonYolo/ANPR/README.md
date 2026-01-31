# ANPR — Automatic Number Plate Recognition 🔧🚗

**Quick overview**

This repository contains an ANPR (Automatic Number Plate Recognition) pipeline built with YOLO (Ultralytics) for vehicle/plate detection and OCR (PaddleOCR / EasyOCR) for text recognition. The project is implemented primarily as a Jupyter notebook (`Anpr.ipynb`) and includes dataset folders and pretrained/training weights.

---

## 🔍 Features

- Train YOLO model on a license plate dataset
- Run inference and save annotated images
- Crop detected plates and run OCR (PaddleOCR or EasyOCR)
- Example notebook showing training, inference, cropping, and OCR steps

---

## 📁 Repository structure (important files)

- `Anpr.ipynb` — main notebook with training and inference examples
- `best.pt` — trained model weights (output from training)
- `yolo11n.pt` — base YOLO model used for transfer/training
- `licence-plate-dataset/` — dataset (contains `train/`, `valid/`, `test/` and `data.yaml`)
- `cropped_objects/` — directory created when cropping detected plates
- `train4/weights/` — alternative training weights (e.g., `best.pt`, `last.pt`)

---

## ✅ Requirements

Recommended Python packages (install via pip):

```
pip install ultralytics torch torchvision opencv-python matplotlib numpy paddlepaddle paddleocr easyocr
```

Notes:
- Use the appropriate `paddlepaddle` package for your platform (CPU/GPU). See PaddlePaddle installation docs for specifics.
- GPU (CUDA) is recommended for training.

---

## 🚀 Quick start

1. Open `Anpr.ipynb` and run the cells in order.

2. Training (from the notebook):

```python
from Anpr import train  # or use the train() cell in the notebook
train(model_path="yolo11n.pt", dataset_dir="licence-plate-dataset", epochs=50, device="cuda")
```

Trained weights are saved in `runs/detect/train/weights/best.pt` by the Ultralytics training routine.

3. Inference example (notebook):

```python
from ultralytics import YOLO
model = YOLO("best.pt")
results = model("test_3.jpeg", save=True)  # annotated image saved under runs/detect/predict
xyxy = results[0].boxes.xyxy.cpu().numpy()
```

4. Crop detected plates and run OCR (example flow in notebook):

- Use saved bounding boxes to crop and save plate images under `cropped_objects/`
- Use PaddleOCR or EasyOCR to extract plate text from cropped images

---

## 🗂 Dataset

**This repository does not include the dataset.** Download or obtain a license-plate dataset and place it under `licence-plate-dataset/` with the following structure:

```
licence-plate-dataset/
  train/
    images/
    labels/
  valid/
    images/
    labels/
  test/
    images/
    labels/
  data.yaml
```

Example `data.yaml` (YOLO/Ultralytics format):

```yaml
train: licence-plate-dataset/train/images
val: licence-plate-dataset/valid/images
test: licence-plate-dataset/test/images
nc: 1
names: ['plate']
```

Recommended ways to get a dataset:

- Roboflow or similar dataset hosting (export to YOLO format). Example placeholder: `https://app.roboflow.com/datasets/your-dataset`.
- Kaggle datasets (search for "license plate" or "vehicle plates").
- Create your own dataset and convert labels to YOLO format.

Quick download & extraction example (replace `DATASET_URL` with the real link):

```bash
curl -L -o dataset.zip "DATASET_URL"
unzip dataset.zip -d licence-plate-dataset
# verify the folder structure matches the expected layout above
```

Notes & best practices:

- If your dataset contains subfolders or different structure, move images/labels into the folders shown above or update `data.yaml` accordingly.
- Do **not** commit large datasets or binary images to the main Git repository. Add the dataset directory to `.gitignore` or use Git LFS for large files:

```
# .gitignore
/licence-plate-dataset/
```

> Tip: Verify `data.yaml` paths before training to avoid path errors. If you want, I can add a template `download_dataset.sh` or add `licence-plate-dataset/` to `.gitignore` for you.

---

## ⚠️ Notes & Troubleshooting

- If training fails due to missing dataset, check that `licence-plate-dataset/data.yaml` exists and that its paths are correct.
- For OCR, try both `PaddleOCR` and `EasyOCR`—results may vary depending on lighting, plate fonts, and orientation.
- If using CUDA, ensure compatible `torch` and `paddlepaddle` builds are installed.

---

## 🧾 License & Contact

This repository contains research/experimentation code. Add a license file if you plan to publish or share publicly.

If you want the README expanded (installation scripts, reproducible training commands, or Dockerfile), tell me what you'd like and I can add it. ✨
