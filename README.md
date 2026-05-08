UAV-DET: High-Resolution Multi-Scale Feature Fusion for UAV Vehicle Detection and Tracking
Reproducibility Statement

All core experiments reported in the paper can be reproduced using the publicly available datasets (VisDrone2019-DET and DroneVehicle) and the provided code in this repository.
The self-collected UAV video streams are only used to evaluate the tracking algorithm (VI-Track) in dense and intersecting motion scenarios. These videos are not publicly available, but they do not affect the reproducibility of the main detection experiments.
This repository includes all scripts required to train, test, and track vehicles, as well as instructions to reproduce the reported performance metrics.

Overview

UAV-DET implements MSFSA-Net for vehicle detection and VI-Track for multi-object tracking in UAV aerial images. It addresses:

Small target scales
Complex, dynamic backgrounds
Motion ambiguity in dense trajectory intersections
Key Features
MSFSA-Net:
High-resolution multi-scale backbone preserves fine-grained features
SARAFE module for semantic-aware upsampling
Micro-object detection head (T-Head) for very small vehicles
VI-Track:
Velocity-direction weighted correlation correction
Reduces ID switching and trajectory fragmentation
Improves average trajectory lifetime
Performance
Dataset	mAP@0.5	mAP@0.5:0.95
VisDrone2019-DET	44.9%	25.0%
DroneVehicle	75.7%	-

VI-Track improves trajectory stability: total trajectories decrease, average trajectory lifetime increases, fragmentation index decreases (see Table 5 in paper).

```
- Python 3.8+
- PyTorch 1.13.0
- CUDA 11.7 (for GPU acceleration)

---

## Usage

### Detection
```bash
python scripts/test.py --data /path/to/dataset --weights models/yolov5s.pt --img-size 640
```

### Tracking
```bash
python scripts/track.py --video /path/to/uav_video.mp4 --det-model models/yolov5s.pt
```

### Training
```bash
python scripts/train.py --data /path/to/dataset --epochs 100 --batch-size 16
```

### Inference Example (Python)
```python
import torch

# Load YOLOv5 model
model = torch.hub.load("ultralytics/yolov5", "yolov5s")

# Input image (URL or local path)
img = "https://ultralytics.com/images/zidane.jpg"

# Perform inference
results = model(img)

# Process results
results.print()  # Console output
results.show()   # Display image
results.save()   # Save to outputs/
```

---

## Datasets
- **VisDrone2019-DET:** Public UAV aerial dataset for vehicle detection. Used for ablation and comparison experiments.  
- **DroneVehicle:** UAV RGB-Infrared cross-modality dataset to validate detection performance across modalities.  
- **UAV_videos:** Self-collected UAV video streams used for multi-object tracking evaluation. Not publicly available.

---

---

## Outputs
- Detection results and visualizations saved in `outputs/`  
- Cropped predictions and prediction tables accessible via Python results object
