# MIPD-YOLO: Lightweight Morphology-Guided Defect Detection for Photovoltaic Quartz Crucibles

This repository is the official project page for **MIPD-YOLO**, a lightweight morphology-guided defect detection framework for photovoltaic quartz crucible inner-wall inspection under complex imaging conditions, including curved-surface distortion, high reflectivity, and partial occlusion.

MIPD-YOLO is built upon YOLOv11n and introduces task-oriented improvements for:
- morphology-aligned representation of elongated and orientation-varying defects,
- feature reconstruction under occlusion and reflection,
- attention-enhanced lightweight detection,
- stable bounding-box regression for extreme-aspect-ratio defects.

## Availability

The source code, model configuration files, and trained weights will be released upon acceptance/publication of the manuscript.

During peer review, verification materials may be provided to editors or reviewers upon reasonable request.

## Dataset

The quartz crucible inner-wall defect dataset is currently not publicly available due to ongoing industrial research and intellectual property considerations. It contains 1,881 annotated images covering six defect types:

- black spot
- bubble
- water drop bubble
- white spot
- devitrification spot
- bubble cluster

For experiments on public industrial defect data, GC10-DET is used to evaluate generalization. Please obtain GC10-DET from its official source and organize it in YOLO format.

## Results

On the self-built quartz crucible test set, MIPD-YOLO achieves:

- mAP50: 95.4%
- mAP50-95: 69.6%
- Parameters: 2.88M
- FLOPs: 6.8G
- FPS: 126 on RTX 4060 Ti

On GC10-DET, MIPD-YOLO improves mAP50 by 7.7 percentage points over YOLOv11n.

## Citation

The citation information will be updated after publication.
