## Bottom-up Higher-Resolution Networks for Multi-Person Pose Estimation

(Paper released on Aug 27, 2019)

### Background of bottom-up pose estimation , pros and cons

Typical bottom-up pipeline consists of two main steps:
- heatmap prediction
- keypoint grouping

Pros and cons of bottom-up pose estimation methods compared to the top-down ones:
- Pros
  - Unlike top-down methods that rely on a separate person detector and need to estimate pose for every person individually, bottom normally computationally less intensive.
  - Because top-down methods consists of several modules such as detection and pose estimation, so they're not truly end-to-end systems. In contrast, bottom-up methods could be designed as true end-to-end systems.
- Cons
  - Unlike top-down methods can normalize all the persons to approximately the same scale by cropping and resizing the detected person bounding boxes, bottom-up methods are sensitive to the scale variance of persons
    - Most state-of-the-art performances on various multi-person human pose estimation benchmarks are achieved by top-down methods

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

### Further reading
1. [Associative Embedding: End-to-End Learning for Joint Detection and Grouping, NIPS'17](https://papers.nips.cc/paper/6822-associative-embedding-end-to-end-learning-for-joint-detection-and-grouping.pdf)
2. [PersonLab: Person Pose Estimation and Instance Segmentation with a Bottom-Up, Part-Based, Geometric Embedding Model, ECCV'18](https://arxiv.org/pdf/1803.08225.pdf)
