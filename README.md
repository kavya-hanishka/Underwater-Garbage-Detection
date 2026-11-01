# TrashCAN V2.1 – Underwater Garbage Detection Dataset

A cleaned and reorganized version of the TrashCAN `material_version` dataset, prepared for underwater object detection using YOLO-based deep learning models.

## Project Overview

This dataset was prepared as part of the project **AI-Enabled Underwater Garbage Detection Using Computer Vision**.

The objective is to detect and classify underwater objects, including marine organisms, remotely operated vehicles (ROVs), and different categories of marine debris.

The dataset contains 7,212 annotated images across 16 object classes.

## Dataset Statistics

| Property | Details |
|---|---|
| Dataset | TrashCAN – material_version |
| Version | V2.1 |
| Total images | 7,212 |
| Source videos | 312 |
| Object classes | 16 |
| Total annotations | 12,333 |
| Annotation format | YOLO |
| Input resolution used | 640 × 640 |

## Dataset Split

A video-level group-aware splitting strategy was used to prevent frames originating from the same source video from appearing in multiple subsets.

| Split | Images | Source Videos | Instances |
|---|---:|---:|---:|
| Training | 5,078 | 218 | 9,080 |
| Validation | 1,050 | 47 | 1,623 |
| Testing | 1,084 | 47 | 1,630 |
| **Total** | **7,212** | **312** | **12,333** |

There is no source-video overlap between the training, validation, and testing subsets.

All images have corresponding annotation files.

## Object Classes

The dataset contains the following 16 classes:

| Class ID | Class Name |
|---:|---|
| 0 | rov |
| 1 | plant |
| 2 | animal_fish |
| 3 | animal_starfish |
| 4 | animal_shells |
| 5 | animal_crab |
| 6 | animal_eel |
| 7 | animal_etc |
| 8 | trash_etc |
| 9 | trash_fabric |
| 10 | trash_fishing_gear |
| 11 | trash_metal |
| 12 | trash_paper |
| 13 | trash_plastic |
| 14 | trash_rubber |
| 15 | trash_wood |

## Dataset Directory Structure

```text
V2.1/
│
├── images/
│   ├── train/
│   ├── val/
│   └── test/
│
├── labels/
│   ├── train/
│   ├── val/
│   └── test/
│
└── data.yaml
```

Each image has a corresponding YOLO-format annotation file.

## Dataset Preparation

The V2.1 dataset was prepared through the following steps:

1. Audited the original dataset and identified duplicate image files.
2. Removed 20 duplicate `(1).jpg` files that did not have corresponding annotation files.
3. Verified image and annotation availability.
4. Identified source-video relationships for the images.
5. Reorganized the dataset using video-level group-aware splitting.
6. Ensured that no source video was shared between training, validation, and testing.
7. Maintained separate validation and test sets for reliable model evaluation.

The split approximately balances image counts and class instances while maintaining video-level separation. It is not a perfectly class-stratified split.

## Preprocessing

- Images were prepared for YOLO-based object detection.
- Aspect-ratio-preserving resizing with letterboxing was used for 640 × 640 model input.
- YOLO-format bounding-box annotations were retained.
- Training-only augmentation and sampling experiments were conducted separately.
- Validation and test sets were kept unchanged during oversampling experiments.

## Model Experiments

The V2.1 dataset was used to evaluate multiple YOLO configurations.

| Model Configuration | Precision | Recall | mAP@50 | mAP@50–95 |
|---|---:|---:|---:|---:|
| YOLO11s Baseline | **0.519** | 0.234 | **0.236** | **0.143** |
| YOLO11s Oversampled | 0.494 | 0.198 | 0.203 | 0.125 |
| YOLOv8s Baseline | 0.439 | **0.238** | 0.216 | 0.130 |

**Best completed configuration:** YOLO11s Baseline

Training configuration:
- Pretrained YOLO11s weights
- Image size: 640 × 640
- Epochs: 100
- Parameters: approximately 9.42 million
- GFLOPs: 21.5

The YOLO11s baseline achieved the best aggregate validation performance among the completed V2.1 experiments.

*Note: These are validation results, not final test-set results.*

## Class Imbalance

The dataset exhibits considerable class imbalance, with frequently occurring categories such as `rov`, `trash_etc`, and `trash_plastic`, while categories such as `trash_rubber`, `trash_paper`, and `trash_fishing_gear` have fewer instances.

Targeted oversampling was investigated to improve rare-class detection. However, the V2.1 oversampling experiment did not improve aggregate validation performance.

This highlighted the limitations of simple image repetition and the need for more effective class-balancing strategies.

## Dataset Access

The complete dataset, including images, annotations, and configuration files, is hosted externally because of GitHub's file-size limitations.

**Google Drive:** [Insert your V2.1 Google Drive folder link here]

The folder should contain the complete `images/`, `labels/`, and `data.yaml` structure.

## Reproducibility

The dataset configuration file `data.yaml` defines the dataset paths, number of classes, and class names.

Example training command:

```bash
pip install ultralytics

yolo detect train \
    model=yolo11s.pt \
    data=data.yaml \
    epochs=100 \
    imgsz=640
```

Update the dataset paths in `data.yaml` according to your local directory structure before training.

## Important Notes

- The dataset is intended for research and educational purposes.
- The original TrashCAN dataset should be acknowledged when using its data.
- Refer to the original dataset source for licensing and usage conditions.
- The reported model metrics correspond to validation experiments.
- The final test set must remain untouched during model selection.

## Acknowledgements

This work was carried out as part of an internship project on **AI-Enabled Underwater Garbage Detection Using Computer Vision**, involving dataset preparation, object detection, model comparison, class imbalance analysis, and evaluation.

**Technologies:** Python, PyTorch, Ultralytics YOLO, OpenCV, Google Colab, and Kaggle.

---

*Dataset Version: V2.1*  
*Project: Underwater Garbage Detection Using Computer Vision*
