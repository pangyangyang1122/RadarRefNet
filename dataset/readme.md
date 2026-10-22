# RADDet-REC Annotations

This directory provides the annotation files of **RADDet-REC**, a radar referring expression comprehension (REC) benchmark constructed based on the original RADDet dataset.

RADDet-REC augments radar target instances with natural-language referring expressions for language-guided instance localization on 3D Range–Azimuth–Doppler (RAD) spectra.

The original radar data are not redistributed in this repository. Please obtain the RADDet dataset from the official repository:

https://github.com/ZhangAoCanada/RADDet

## Files

The dataset directory contains two types of annotations:

```text
dataset/
├── RADDet_REC_train.jsonl
├── RADDet_REC_test.jsonl
├── structured_attributes_train.csv
├── structured_attributes_test.csv
└── README.md
```

The exact filenames may vary depending on the released version.

### 1. Natural-Language REC Annotations

The `.jsonl` files contain the natural-language referring expression annotations used for the final REC task.

Each line corresponds to one referring instance and contains:

- `dataID`: identifier of the corresponding radar frame;
- `description`: natural-language referring expression describing the target instance;
- `boxes.class`: target category;
- `range_doppler_azimuth_box`: target bounding-box annotation in the RAD representation;
- `cartesian_box`: corresponding target bounding-box annotation in Cartesian coordinates.

An example is shown below:

```json
{
  "dataID": "part_1/000028",
  "description": "A car is driving close at a moderate speed from the front left.",
  "boxes": {
    "class": "car",
    "range_doppler_azimuth_box": {
      "center_range": 169.5,
      "center_azimuth": 91.5,
      "center_doppler": 42.0,
      "height_range": 22.0,
      "width_azimuth": 28.0,
      "width_doppler": 19.0
    },
    "cartesian_box": {
      "center_cart_range": 173.0,
      "center_cart_azimuth": 230.5,
      "height_cart_range": 23.0,
      "width_cart_azimuth": 16.0
    }
  }
}
```

Multiple referring expressions can be generated for the same radar target instance. Accordingly, the same `dataID` and target annotation may appear in multiple entries with different natural-language descriptions.

### 2. Structured Target Attributes

The `.csv` files contain the **structured target attributes** associated with individual radar target instances.

These attributes provide an intermediate semantic representation between radar observations and free-form natural-language referring expressions. They are used during RADDet-REC construction and in the **Radar Region–Attribute Semantic Alignment** stage of RadarRefNet.

The structured target attributes include:

- target category;
- range;
- azimuth;
- speed state;
- motion direction;
- risk level.

These attributes are obtained from the original radar target annotations and predefined quantization rules, and are subsequently used to generate natural-language referring expressions.

A representative structured description may contain information such as:

```text
Class: car
Range: close distance
Azimuth: front left
Speed: moderate speed
Direction: approaching
Risk Level: safe
```

The structured target attributes serve as intermediate semantic descriptors rather than the final REC queries. The final REC task uses the free-form natural-language expressions provided in the `.jsonl` annotation files.

## Dataset Usage

To use RADDet-REC:

1. Download the original RADDet radar data from the official RADDet repository \url{https://github.com/ZhangAoCanada/RADDet.git}.
2. Place the RADDet data according to the directory structure required by the provided preprocessing scripts.
3. Download the RADDet-REC annotation files from this directory.
4. Use the `.jsonl` files for natural-language REC training and evaluation.
5. Use the structured target attribute files for radar region–attribute semantic alignment when reproducing the progressive three-stage training strategy.

Detailed preprocessing and training instructions will be provided in the main repository documentation.

## Data Split

RADDet-REC follows the corresponding training and testing split of the original RADDet dataset.

The released files include separate annotations for training and testing.

## Citation

If you use RADDet-REC or RadarRefNet in your research, please cite our work:

```bibtex
@article{pang2026radarrefnet,
  title  = {Language-Guided mmWave Radar Referring Expression Comprehension for Road Scene Understanding},
  author = {Pang, Siqi and Zhang, Xu and Chen, Hongliang and Guo, Kaitai and Zheng, Yang and Liang, Jimin},
  year   = {2026}
}
```

Please also cite the original RADDet dataset when using the underlying radar data.

## Acknowledgement

RADDet-REC is constructed based on the RADDet dataset. We thank the authors of RADDet for making the original radar dataset publicly available.
