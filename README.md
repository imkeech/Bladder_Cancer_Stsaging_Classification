# 🧠 A COMPARATIVE STUDY FOR BLADDER CANCER SUBTYPING CLASSIFICATION : RESNET18 VS. EFFICIENTNETB0 VS. CONVNEXT-TINY (CT Slice-Based)

This repository presents a deep learning pipeline to classify bladder cancer stages (Stage II, III, IV) from CT scan slices using three modern CNN architectures: **ResNet18**, **EfficientNetB0**, and **ConvNeXt-Tiny**. It uses the TCGA-BLCA dataset from TCIA and applies **Grad-CAM** for model explainability.

---

## 🔍 Problem Statement
Manual staging from CT images is time-consuming and prone to variability. This project automates the process using deep learning, ensuring fast, consistent, and interpretable predictions.

---

## 🧰 Models Compared
- ✅ **ResNet18** – Classic residual network
- ✅ **EfficientNetB0** – Efficient and scalable CNN
- ✅ **ConvNeXt-Tiny** – Transformer-inspired CNN (Best performer)

---

## 🚀 Project Workflow

1. **Dataset Download:** TCGA-BLCA from [TCIA](https://www.cancerimagingarchive.net/collection/tcga-blca/)
2. **Patient-wise Segregation:** Use the metadata CSV to group CT, MR, PT scans per patient.
3. **Modality Filtering:** Retain only CT modality for this study.
4. **DICOM to NumPy Conversion:** Convert DICOM files into `.npy` format for fast processing.
5. **Slice Extraction:** Extract mid-slices (24 to 40) from each patient’s CT volume.
6. **Preprocessing:** Resize slices to 224×224, normalize to [0, 1], and encode stage labels.
7. **Model Training:** Train ResNet18, EfficientNetB0, ConvNeXt-Tiny using class-weighted loss and Stratified K-Folds.
8. **Evaluation & Visualization:** Evaluate using standard metrics and visualize predictions using Grad-CAM.

```mermaid
graph TD
A[Dataset Download] --> B[Segregate Patient wise with Modality]
B --> C[Filter CT for all the patients]
C --> D[DICOM to NPY Conversion]
D --> E[Slice Extraction: 24–40]
E --> F[Preprocessing: 
Resize + Normalize]
F --> G[Train Models: 
ResNet18, EfficientNetB0, ConvNeXt-Tiny]
G --> H[Evaluate Metrics]
H --> I[Grad-CAM Explainability]
```

---

## 📁 Directory Structure

| Folder | Description |
|--------|-------------|
| `utils/` | Core functions and scripts (training, data loading, Grad-CAM) |
| `saved_models/` | Saved `.pth` model weights |
| `results/` | Grad-CAM heatmaps, metrics |
| `notebooks/` | Jupyter notebooks for experimentation |
| `data/` | Metadata CSV and NPY CT slices |

---

## 🧪 Evaluation Results

| Model           | Accuracy | Precision | Recall | F1-Score |
|----------------|----------|-----------|--------|----------|
| ResNet18        | 96.35%   | 95.80%    | 94.70% | 95.24%   |
| EfficientNetB0  | 97.01%   | 96.78%    | 95.82% | 96.30%   |
| ConvNeXt-Tiny   | **98.50%** | **98.12%** | **98.67%** | **98.39%** |

---

## 🔍 Grad-CAM Explainability

Grad-CAM was used to highlight the bladder regions influencing the model's prediction, improving clinical trust and transparency.

![Grad-CAM Sample](results/gradcam_examples/sample1.png)

---

## 💻 Usage

```bash
# Clone the repo
git clone https://github.com/yourusername/bladder-cancer-staging-cnn.git
cd bladder-cancer-staging-cnn

# Install requirements
pip install -r requirements.txt

# Train the model
python main.py --model convnext --epochs 30

# Run Grad-CAM on a test slice
python utils/gradcam.py --model_path saved_models/convnext_best.pth --image_path data/sample.npy
```

---

## 📦 Requirements

```
torch
torchvision
opencv-python
matplotlib
scikit-learn
pandas
tqdm
```

---

## 📚 Dataset

**Source**: [TCGA-BLCA – The Cancer Imaging Archive](https://www.cancerimagingarchive.net/collection/tcga-blca/)  
Modality: CT Scans  
Stages Used: Stage II, III, IV

---

## 🧑‍⚕️ Author

- **Krishna V KN** – Final Year B.Tech (AIDA), Sri Ramachandra Institute  
- Guide: **Ms. S. Deena**, Assistant Professor  
- 📧 Email: krishnavkn22@gmail.com

---

## 📌 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
