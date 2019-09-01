## Bottom-up Higher-Resolution Networks for Multi-Person Pose Estimation

(Paper released on Aug 27, 2019)

### Background of bottom-up pose estimation , pros and cons

Typical bottom-up pipeline consists of two main steps:
- heatmap prediction
- keypoint grouping

Pros and cons of bottom-up pose estimation methods:
- Pros
  - xxx
- Cons
  - yyy


### Key ideas of this paper
- Bottom-up multiperson human pose estimation and focuses on **better heatmap prediction**
  - An extension of the HRNet framework
- HigherHRNet generates higher-resolution feature maps by **deconvolving the high-resolution feature maps** outputted by
HRNet
  - The higher-resolution feature maps are **spatially more accurate** for small and medium persons
  - Basically the proposed method builds **high-quality multi-level features** and perform **multi-scale pose prediction**
- The extra computation overhead is marginal and negligible compared to the existing methods
  - existing methods rely on:
  - **multi-scale image pyramids** or **large input image size** to generate accurate pose heatmaps
- HigherHRNet surpasses all existing bottom-up methods on the COCO dataset **without using multi-scale test**
