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




---

## Datasets
- **VisDrone2019-DET:** Public UAV aerial dataset for vehicle detection. Used for ablation and comparison experiments.  https://github.com/VisDrone/VisDrone-Dataset
- **DroneVehicle:** UAV RGB-Infrared cross-modality dataset to validate detection performance across modalities.  https://github.com/VisDrone/DroneVehicle
- **UAV_videos:** Self-collected UAV video streams used for multi-object tracking evaluation. Not publicly available.

---


## Outputs
- The weights trained by the improved model are available in the link below
- Please send a private message to receive the extraction code
- experimental_ckpt：https://pan.baidu.com/share/init?surl=u8THZmk7ednGKiqUtGaVuw   
- The original data trained by the improved model is available at the link below
- Please send a private message to receive the extraction code
- experimental_data：https://pan.baidu.com/share/init?surl=bYQrizn5jBcjPLapR-BwCQ
