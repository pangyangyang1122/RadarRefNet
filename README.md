# RadarRefNet
Language-Guided Referring Expression Comprehension on mmWave Radar for Road Scene Understanding.

# RadarRefNet

Official repository for **“Language-Guided mmWave Radar Referring Expression Comprehension for Road Scene Understanding”**.

RadarRefNet introduces **Referring Expression Comprehension (REC)** into dense 3D Range–Azimuth–Doppler (RAD) spectra, enabling natural-language-guided instance localization for mmWave radar perception.

<p align="center">
  <img src="assets/teaser.png" width="90%">
</p>

## Overview

Conventional mmWave radar perception mainly follows a single-modal detection paradigm and provides limited capability for localizing specific target instances according to high-level semantic instructions.

We introduce radar referring expression comprehension, where the input consists of a 3D RAD spectrum and a natural-language referring expression, and the goal is to localize the target instance described by the expression.

This repository contains the implementation of **RadarRefNet** and the annotations of **RADDet-REC**.

## RADDet-REC

**RADDet-REC** is a radar referring expression comprehension benchmark constructed based on the RADDet dataset.

It contains:

- 6 road-object categories
- 57,072 referring instances
- 3D RAD spectra
- target annotations
- natural-language referring expressions

Structured target attributes are further used during dataset construction and radar region–attribute semantic alignment.

> The original radar data are not redistributed in this repository. Please obtain the RADDet dataset from its official source and use the provided annotations and processing scripts to construct RADDet-REC.

<p align="center">
  <img src="assets/dataset_pipeline.png" width="90%">
</p>

## RadarRefNet

RadarRefNet performs language-guided target localization directly on 3D RAD spectra.

The framework contains:

- a 3D Transformer radar encoder
- a frozen RoBERTa text encoder
- **Text-Guided Radar Feature Modulation (TGRFM)**
- **Multi-Level Radar–Text Fusion**
- 3D feature aggregation
- a 3D detection head

TGRFM injects global referring semantics into radar feature extraction, while multi-level radar–text cross-attention enables fine-grained interaction between linguistic tokens and hierarchical radar representations.

<p align="center">
  <img src="assets/framework.png" width="95%">
</p>

## Progressive Three-Stage Training

RadarRefNet is trained using a progressive three-stage strategy:

1. **Radar MAE Pretraining**  
   Learns intrinsic RAD-spectrum representations through masked reconstruction.

2. **Radar Region–Attribute Semantic Alignment**  
   Establishes fine-grained correspondence between localized radar regions and structured target attribute semantics.

3. **Natural-Language REC Fine-Tuning**  
   Transfers the learned cross-modal correspondence to free-form natural-language referring expressions.

## Main Results

RadarRefNet achieves:

| Metric | Result |
|---|---:|
| mAP@0.1 | 79.8% |
| mAP@0.3 | 64.3% |
| mAP@0.5 | 36.2% |

Experiments further show that language guidance improves target localization and provides notable gains on tail classes.

<p align="center">
  <img src="assets/qualitative.png" width="95%">
</p>

## Code and Data

The repository will provide:

- RadarRefNet training and evaluation code
- configurations for the three training stages
- RADDet-REC referring-expression annotations
- structured target attributes
- dataset preparation scripts
- evaluation scripts
- pretrained model checkpoints

The repository is currently being organized. The complete implementation and annotations will be released shortly.

## Installation

Installation instructions will be provided with the code release.

```bash
git clone https://github.com/YOUR_USERNAME/RadarRefNet.git
cd RadarRefNet
```

## Dataset Preparation

Please first download the original **RADDet** dataset from its official source.

The RADDet-REC annotations and conversion scripts provided in this repository can then be used to prepare the language-guided radar REC benchmark.

Detailed instructions will be provided soon.

## Citation

If you find this work useful, please consider citing our paper:

```bibtex
@article{pang2026radarrefnet,
  title   = {Language-Guided mmWave Radar Referring Expression Comprehension for Road Scene Understanding},
  author  = {Pang, Siqi and Zhang, Xu and Chen, Hongliang and Guo, Kaitai and Zheng, Yang and Liang, Jimin},
  journal = {IEEE Transactions on Circuits and Systems for Video Technology},
  year    = {2026}
}
```

> Citation information will be updated after publication.

## Acknowledgement

This work is supported by the National Natural Science Foundation of China under Grant Nos. 62476205 and 62301405.

We thank the authors of RADDet and the open-source community for their contributions to radar perception research.
