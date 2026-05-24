# MIPD-YOLO: Lightweight Morphology-Guided Defect Detection for Photovoltaic Quartz Crucibles

This repository contains the official implementation of **MIPD-YOLO**, a lightweight and robust defect detection method for inner-wall defects of photovoltaic quartz crucibles under complex imaging conditions (curved-surface distortion, high reflectivity, occlusion, etc.). The method is built upon YOLOv11n and introduces four novel components: C3k2-MALGB, C2DPB, SEAM-Detect, and PIoU loss.



## Key Features

- **C3k2-MALGB** – Morphology-aligned local-global block embedded into backbone to handle stretched/orientation-varying defects caused by curved-wall projection.
- **C2DPB** – Dynamic position bias module to reconstruct features under occlusion and reflection.
- **SEAM-Detect** – Lightweight detection head with spatial enhancement attention for suppressing background false alarms.
- **PIoU Loss** – Target-scale-adaptive bounding box regression loss that eliminates abnormal box expansion and improves edge fitting for extreme-aspect-ratio defects.

## Project Structure
- `GC10-DET_dataset/` - Public metallic surface defect dataset (already split)
  - `images/` - Images (train/val/test subdirectories)
  - `labels/` - YOLO-format labels
  - `data.yaml` - Dataset config
- `models/` - Custom modules and configs
  - `MIPD-YOLO.yaml` - Full model configuration
  - `yolo11.yaml` - Baseline YOLOv11n configuration
  - `C2DPB.py` - C2DPB module
  - `C3k2-MALGB.py` - C3k2 backbone with MALGB
  - `Detect_SEAM.py` - SEAM-Detect head
  - `MALGBlock.py` - Core MALGB block
  - `PIoU.py` - Powerful-IoU loss
  - `SEAM.py` - Spatial Enhancement Attention Module
- `split_data.py` - Dataset split script (for your own datasets)
- `train.py` - Training script
- `val.py` - Validation script
- `yolo11n.pt` - Pretrained YOLOv11n weights
- `README.md` - This file



## Environment Setup

- Python >= 3.10
- PyTorch >= 2.6.0
- CUDA 12.6 (recommended)

Install dependencies:
pip install ultralytics numpy opencv-python matplotlib



## Dataset Preparation

### Quartz Crucible Inner-Wall Dataset (private)

Due to ongoing industrial research, this dataset is **not publicly available**. It contains 1,881 annotated images of six defect types (black spot, bubble, water drop bubble, white spot, devitrification spot, bubble cluster).  
If you need to train on your own data, organize it in YOLO format:
- `dataset/`
  - `images/`
    - `train/`
    - `val/`
    - `test/`
  - `labels/`
    - `train/`
    - `val/`
    - `test/`



### GC10-DET Public Dataset (optional)

The GC10-DET dataset has already been downloaded and properly split into train/val/test sets inside the `GC10-DET_dataset/` directory. No additional download is required. The dataset is used to evaluate the generalization ability of the model.

## Training

1. Modify `train.py` to set your dataset paths, model configuration (use `models/MIPD-YOLO.yaml`), and hyperparameters (image size 640×640, batch size 16, epochs 300.).
2. Run training:
python train.py



To enable/disable specific modules, edit the model building part in `train.py` accordingly.

## Validation & Testing
python val.py --weights path/to/your/trained_weights.pt --data your_dataset.yaml



## Results

On the self-built quartz crucible test set, MIPD-YOLO achieves:

- **mAP50**: 95.4% (+2.4% over YOLOv11n)
- **mAP50-95**: 69.6% (+1.7% over YOLOv11n)
- **Parameters**: 2.88M
- **FLOPs**: 6.8G
- **FPS**: 126 (on RTX 4060 Ti)

On GC10-DET public dataset, mAP50 improves by 7.7% over YOLOv11n, demonstrating strong generalization.

