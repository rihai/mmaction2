# Benchmark

We compare our results with some popular frameworks and official releases in terms of speed.

## Comparision Rules

Here we compare our MMAction repo with other video understanding toolboxes in the same data and model settings
by the training time per iteration.

To ensure the fairness of the comparison, the comparison experiments will be conducted under the same hardware environment and using the same dataset.
For each model setting, we keep the same data preprocessing methods to make sure the same feature input.
In addition, we also use MemCache, a distributed cached system, to load the data for the same IO time.

The time we measured is the average training time for an iteration, including data processing and model training.


## Recognizers

| Model | MMAction (s/iter) | MMAction V0.1 (s/iter) | [Temporal-Shift-Module](https://github.com/mit-han-lab/temporal-shift-module) (s/iter) | [PySlowFast](https://github.com/facebookresearch/SlowFast) (s/iter) |
| :---: | :---------------: | :--------------------: | :----------------------------: | :-----------------: |
| TSN ([tsn_r50_1x1x3_100e_kinetics400_rgb](/configs/recognition/tsn/tsn_r50_1x1x3_100e_kinetics400_rgb.py))   | **0.29** | 0.36 | 0.45 | x |
| I3D ([i3d_r50_32x2x1_100e_kinetics400_rgb](/configs/recognition/i3d/i3d_r50_32x2x1_100e_kinetics400_rgb.py)) | **0.45** | 0.58 | x | x |
| I3D ([i3d_r50_8x8x1_100e_kinetics400_rgb](/configs/recognition/i3d/i3d_r50_8x8x1_100e_kinetics400_rgb.py))   | **0.32** | x | x | 0.56 |
| TSM ([tsm_r50_1x1x8_50e_kinetics400_rgb](/configs/recognition/tsm/tsm_r50_1x1x8_50e_kinetics400_rgb.py))     | **0.30** | x | 0.38 | x |
| Slowonly ([slowonly_r50_4x16x1_256e_kinetics400_rgb](/configs/recognition/slowonly/slowonly_r50_4x16x1_256e_kinetics400_rgb.py)) | **0.30** | x | x | 1.03 |
| Slowonly ([slowonly_r50_8x8x1_256e_kinetics400_rgb](/configs/recognition/slowonly/slowonly_r50_8x8x1_256e_kinetics400_rgb.py))   | **0.50** | x | x | 1.29 |
| Slowfast ([slowfast_r50_4x16x1_256e_kinetics400_rgb](/configs/recognition/slowfast/slowfast_r50_4x16x1_256e_kinetics400_rgb.py)) | **0.80** | x | x | 1.40 |
| Slowfast ([slowfast_r50_8x8x1_256e_kinetics400_rgb](/configs/recognition/slowfast/slowfast_r50_8x8x1_256e_kinetics400_rgb.py))   | **1.05** | x | x | 1.41 |
| R(2+1)D ([r2plus1d_r34_8x8x1_180e_kinetics400_rgb](/configs/recognition/r2plus1d/r2plus1d_r34_8x8x1_180e_kinetics400_rgb.py))    | **0.48** | x | x | x |

## Localizers

| Model | MMAction (s/iter) | [BSN(boundary sensitive network)](https://github.com/wzmsltw/BSN-boundary-sensitive-network) (s/iter) |
| :---: | :---------------: | :-------------------------------------: |
| BSN ([TEM + PEM + PGM](/configs/localization/bsn)) | **0.074(TEM)+0.040(PEM)** | 0.101(TEM)+0.040(PEM) |
| BMN ([bmn_400x100_2x8_9e_activitynet_feature](/configs/localization/bmn/bmn_400x100_2x8_9e_activitynet_feature.py)) | **3.27** | 3.30 |

## Hardware

- 8 NVIDIA Tesla V100 (32G) GPUs
- Intel(R) Xeon(R) Gold 6148 CPU @ 2.40GHz

## Software Environment

- Python 3.7
- PyTorch 1.4
- CUDA 10.1
- CUDNN 7.6.03
- NCCL 2.4.08