# TrashCAN V2.1 Dataset

**Project:** AI-Enabled Underwater Garbage Detection Using Computer Vision

**Dataset:** TrashCAN material_version – V2.1

**Total annotated images:** 7,212  
**Number of source videos:** 312  
**Number of classes:** 16

## Dataset Split

| Split | Images | Source Videos | Instances |
|---|---:|---:|---:|
| Training | 5,078 | 218 | 9,080 |
| Validation | 1,050 | 47 | 1,623 |
| Testing | 1,084 | 47 | 1,630 |
| Total | 7,212 | 312 | 12,333 |

## Dataset Preparation

The dataset was organized using a video-level group-aware splitting strategy to prevent frames from the same source video from appearing across different subsets.

All images have corresponding annotation files. The dataset contains 16 object categories covering underwater marine life, ROVs and marine debris.

## Dataset Access

The complete dataset, including images and annotations, is available through the Google Drive link provided separately.

**Note:** The validation and test sets were kept separate from training and oversampling operations.
