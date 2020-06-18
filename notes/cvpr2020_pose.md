### CVPR 2020 Human Pose Estimation Papers

#### 3D human pose estimation - monocular
* [Deep Kinematics Analysis for Monocular 3D Human Pose Estimation](http://openaccess.thecvf.com/content_CVPR_2020/html/Xu_Deep_Kinematics_Analysis_for_Monocular_3D_Human_Pose_Estimation_CVPR_2020_paper.html)
  * Key idea: correct the errors in a hierarchical way. 1) **2D pose correction**. 2) **Decomposed 3D pose estimation**. 3) **3D trajectory completion**. 
    * In 1) **2D pose correction**, they found 2D temporal refinement doesn't help too much for final 3D pose esitmation improvment.
    * Their solution for 2D pose correction is to use projection constraint. Enforce a projection loss using the etimated 2D pose and GT 3D pose. To compute this loss `f` and `c`, the intrinsic parameters are needed, they assume it's given or it can be derived from ground-truth 2D and 3D pose, they left the automatic estimation of intrinsic parameters as a future work. 
      * Note that: our project loss is `| 2D_Proj - 2D_GT |`，we minimize the difference between the projected 2D pose from 3D and the 2D GT. They compute the `f` and `c` using 2D and 3D pose GT, given estimated 2D pose and 3D GT, they compute `f'` and `c'`, so they project loss is on intrinsic parameters `| f - f1 | + | c - c' |`.
    * In 2) **Decomposed 3D pose estimation**, they emphasize the motion trajectory of children joint relative to its parent (defined by human skeleton) forms a spherical curve.
    * They decompose the original 3D pose regression problem to length and direction regression, use two-stream architecture for length and direction estimation. This decomposion leads to dimension reduction in estimated parameters from `3 × T × J` to `2 × T × J + J`. They also claim that the loss of length and direction reduces the learning difficulties. 
  * In 3) **3D trajectory completion**, they notice the estimated joints errors are not equal, mostly from four limbs. They also make use of the confidence score `K'` from 2D estimator. Combining both, they optimize four-limb joints assigned with low 2D confidence score.
    * In order to remove the unreliable joints, they used a dropout layer directly on the joints associated with four limbs, and set the dropout rate as `1 - K'`, this means the unrilable joints have higher chance to be dropped and then completed by the network using other reliable ones. Their completion network is a bi-directional LSTM. 
  * They performed evaluation on H3.6M and HumanEva, and their results are not as good as some published papers such as occlusion-aware networks or spatio-temporal network. 

#### 2D human pose estimation
- HigherHRNet: Scale-Aware Representation Learning for Bottom-Up Human Pose Estimation

#### 3D human pose estimation - multi-view

