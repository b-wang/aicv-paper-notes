### CVPR 2020 Human Pose Estimation Papers

#### 3D human pose estimation - monocular
* [Deep Kinematics Analysis for Monocular 3D Human Pose Estimation](http://openaccess.thecvf.com/content_CVPR_2020/html/Xu_Deep_Kinematics_Analysis_for_Monocular_3D_Human_Pose_Estimation_CVPR_2020_paper.html)
  * Key idea: correct the errors in a hierarchical way. 1) 2D pose correction. 2) Decomposed 3D pose estimation. 3) 3D trajectory completion. 
    * In 2D pose correction, they found 2D temporal refinement doesn't help too much for final 3D pose esitmation improvment.
    * Their solution for 2D pose correction is to use projection constraint. Enforce a projection loss using the etimated 2D pose and GT 3D pose. To compute this loss `f` and `c`, the intrinsic parameters are needed, they assume it's given or it can be derived from ground-truth 2D and 3D pose, they left the automatic estimation of intrinsic parameters as a future work. 
      * Note that: our project loss is `| 2D_Proj - 2D_GT |`，we minimize the difference between the projected 2D pose from 3D and the 2D GT. They compute the `f` and `c` using 2D and 3D pose GT, given estimated 2D pose and 3D GT, they compute `f'` and `c'`, so they project loss is on intrinsic parameters `| f - f1 | + | c - c' |`.

#### 2D human pose estimation
- HigherHRNet: Scale-Aware Representation Learning for Bottom-Up Human Pose Estimation

#### 3D human pose estimation - multi-view

