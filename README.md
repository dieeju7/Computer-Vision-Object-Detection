# Banana Object Detection – Faster R-CNN vs RetinaNet

## Project Overview

This project compares a **two-stage object detector (Faster R-CNN)** and a **one-stage object detector (RetinaNet)** on a custom banana detection dataset.

The goal is to analyze the trade-off between detection accuracy and inference speed under the same training conditions.

---

## Dataset

- 200 manually collected banana images
- Single object class: **banana**
- Annotations in **Pascal VOC (XML) format**
- Images resized to **512×512**
- Dataset split:
  - 160 images → Training set
  - 40 images → Test set

---

## Models Implemented

### 1. Faster R-CNN (Two-Stage Detector)
- Backbone: ResNet50 + FPN (pretrained on COCO)
- Backbone frozen (as required)
- Optimizer: SGD (lr=0.005, momentum=0.9)
- Trained for 5 epochs

### 2. RetinaNet (One-Stage Detector)
- Backbone: ResNet50 + FPN (pretrained on COCO)
- Backbone frozen (as required)
- Optimizer: SGD (lr=0.005, momentum=0.9)
- Trained for 5 epochs

---

## Evaluation Metrics

Models were evaluated using:

- **mAP** (mean Average Precision)
- **mAP@0.5**
- **Inference time (ms per image)**

Evaluation was performed using `torchmetrics` (MeanAveragePrecision).

---

## Results

| Model         | mAP   | mAP@0.5 | Inference Time |
|--------------|--------|----------|----------------|
| Faster R-CNN | ~0.6386  | ~0.9201    | Slower         |
| RetinaNet    | ~0.00  | ~0.00    | Slightly faster|

---

## Discussion

Faster R-CNN significantly outperformed RetinaNet on this small custom dataset.  
With a frozen backbone and limited training data, the one-stage detector (RetinaNet) struggled to learn meaningful object representations.

These results align with theoretical expectations:

- **Two-stage detectors** are generally more robust with small datasets.
- **One-stage detectors** are typically faster but require more data to achieve strong performance.

---

## Visualization

Green boxes represent ground truth annotations.  
Red boxes represent model predictions.

<img width="520" height="528" alt="image" src="https://github.com/user-attachments/assets/1b691107-c912-4a0f-9aa9-71c1a1e19c77" />


---

## Requirements

- Python 3.9+
- PyTorch
- torchvision
- torchmetrics
- numpy
- matplotlib

## Project Structure
```

Computer-Vision-Object-Detection/
│
├── dataset/ # Dataset directory
│ ├── annotations/ # Pascal VOC XML files
│ │ ├── train/
│ │ └── test/
│ │
│ └── images/ # Image files
│ ├── train/
│ └── test/
│
├── bananaDetection.ipynb # Training & evaluation notebook
└── README.md
```

Install dependencies:

```bash
pip install torch torchvision torchmetrics numpy matplotlib
```

### How to Run

1. Clone the repository:
```bash
git clone https://github.com/dieeju7/Computer-Vision-Object-Detection.git
```

2. Run the notebook:
```
bananaDetection.ipynb
```
