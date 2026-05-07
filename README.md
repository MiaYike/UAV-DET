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

Repository Structure
UAV-DET/
├─ datasets/          # VisDrone2019-DET, DroneVehicle, self-collected UAV videos
├─ models/            # Pre-trained MSFSA-Net weights
├─ utils/             # Helper functions
├─ train.py           # Training script
├─ test.py            # Evaluation script
├─ track.py           # VI-Track tracking
└─ README.md
Installation
git clone https://github.com/MiaYike/UAV-DET.git
cd UAV-DET
pip install -r requirements.txt
Python 3.8
PyTorch 1.13.0
CUDA 11.7
Usage
Detection
python test.py --data /path/to/dataset --weights models/msfsa_net.pth --img-size 640
Tracking
python track.py --video /path/to/uav_video.mp4 --det-model models/msfsa_net.pth
Training
python train.py --data /path/to/dataset --epochs 100 --batch-size 16
Datasets
VisDrone2019-DET: Public UAV aerial dataset for vehicle detection. Used for ablation and comparative experiments.
VisDrone2019-DET Challenge
DroneVehicle: UAV RGB-Infrared cross-modality vehicle detection dataset. Used to validate detection performance across modalities.
Refer to Sun et al., IEEE T-CSVT, 2024 [22]
UAV video streams (self-collected): Videos captured by UAVs to evaluate VI-Track multi-object tracking algorithm under dense and intersecting motion scenarios. These videos are not publicly available but used for tracking validation only.
Model Architecture
MSFSA-Net
Backbone: High-resolution multi-scale feature fusion
Neck: SARAFE module for content-adaptive upsampling
Detection Head: Additional T-Head for micro-object detection
VI-Track
Motion consistency evaluated using cosine similarity between trajectory velocity and candidate displacement vectors
Weighted penalty applied for direction deviations
