### CVPR 2020 Human Pose Estimation Papers

#### 3D human pose estimation - monocular
* [Deep Kinematics Analysis for Monocular 3D Human Pose Estimation](http://openaccess.thecvf.com/content_CVPR_2020/html/Xu_Deep_Kinematics_Analysis_for_Monocular_3D_Human_Pose_Estimation_CVPR_2020_paper.html)
  * Key idea: correct the errors in a hierarchical way. 1) **2D pose correction**. 2) **Decomposed 3D pose estimation**. 3) **3D trajectory completion**. 
    * In 1) **2D pose correction**, they found 2D temporal refinement doesn't help too much for final 3D pose esitmation improvment.
    * Their solution for 2D pose correction is to use projection constraint. Enforce a projection loss using the etimated 2D pose and GT 3D pose. To compute this loss `f` and `c`, the intrinsic parameters are needed, they assume it's given or it can be derived from ground-truth 2D and 3D pose, they left the automatic estimation of intrinsic parameters as a future work. 
      * Note that: our project loss is `| 2D_Proj - 2D_GT |`，we minimize the difference between the projected 2D pose from 3D and the 2D GT. They compute the `f` and `c` using 2D and 3D pose GT, given estimated 2D pose and 3D GT, they compute `f'` and `c'`, so they project loss is on intrinsic parameters `| f - f' | + | c - c' |`.
    * In 2) **Decomposed 3D pose estimation**, they emphasize the motion trajectory of children joint relative to its parent (defined by human skeleton) forms a spherical curve.
    * They decompose the original 3D pose regression problem to length and direction regression, use two-stream architecture for length and direction estimation. This decomposion leads to dimension reduction in estimated parameters from `3 × T × J` to `2 × T × J + J`. They also claim that the loss of length and direction reduces the learning difficulties. 
  * In 3) **3D trajectory completion**, they notice the estimated joints errors are not equal, mostly from four limbs. They also make use of the confidence score `K'` from 2D estimator. Combining both, they optimize four-limb joints assigned with low 2D confidence score.
    * In order to remove the unreliable joints, they used a dropout layer directly on the joints associated with four limbs, and set the dropout rate as `1 - K'`, this means the unrilable joints have higher chance to be dropped and then completed by the network using other reliable ones. Their completion network is a bi-directional LSTM. 
  * They performed evaluation on H3.6M and HumanEva, and their results are not as good as some published papers such as occlusion-aware networks or spatio-temporal network. 

* [Cascaded Deep Monocular 3D Human Pose Estimation With Evolutionary Training Data](http://openaccess.thecvf.com/content_CVPR_2020/html/Li_Cascaded_Deep_Monocular_3D_Human_Pose_Estimation_With_Evolutionary_Training_CVPR_2020_paper.html)
  * Key idea: a novel data augmentation method, based on kinematic tree, two random options are performed: crossover and mutation. 
  * Discussed with the author during live Q&A session. 
  * Q: Asked question how image feature is synthesized if a joint is randomly mutated or crossover. A: they focus on the augmentation for the method, there is a lifting network (2D kpts -> 3D kpts). In this case, just need to simulate corresponding 2D and 3D joints. 
  * Q: How's the improvement? A: they show after applying the augmentation, single image-based method can supass the temporal based method (within certain range of using training data). 
  * Q: How to extend this augmentation strategy to video method? A: random mutation is hard, as randomly change one joint at one frame, we have to change the neighboring frames to make the sequence smooth and natural. Crossover is easier, kind of just mirroring the whole sequence. 
  * Q: How to extend this method to synthesize both skeleton and image, like using GAN? A: GAN needs a lot of data, and the produced images are not good enough maybe. Maybe using CG human model to render on image and then using GAN to do a style transfer to make it more realistic. 
  
* [PandaNet : Anchor-Based Single-Shot Multi-Person 3D Pose Estimation](http://openaccess.thecvf.com/content_CVPR_2020/papers/Benzine_PandaNet_Anchor-Based_Single-Shot_Multi-Person_3D_Pose_Estimation_CVPR_2020_paper.pdf)
  * Discussed with the author during live Q&A session.
  * This is a bottom-up multi-person 3D human pose estimation method. In order to solve the problem that bottom-up method cannot deal with smaller persons, they propose to use anchor like in object detection. Using anchor introduces another issue which is when people overlap with each other. They propose a Pose-Aware Anchors Selection method to deal with this.
  * They evaluated on multipe multi-person 3D datasets: JTA, Panoptic, MuPoTS-3D. The JTA dataset is not that good becuase it only contains pedistrans. They mentioned a new dataset: [Human pose estimation for real-world crowded scenarios](https://arxiv.org/pdf/1907.06922.pdf). 
  * They show that running time comparison against Moon et al. ICCV'19. 
  
* [PandaNet : Anchor-Based Single-Shot Multi-Person 3D Pose Estimation](http://openaccess.thecvf.com/content_CVPR_2020/html/Benzine_PandaNet_Anchor-Based_Single-Shot_Multi-Person_3D_Pose_Estimation_CVPR_2020_paper.html)
  
* [Attention Mechanism Exploits Temporal Contexts: Real-Time 3D Human Pose Reconstruction](http://openaccess.thecvf.com/content_CVPR_2020/html/Liu_Attention_Mechanism_Exploits_Temporal_Contexts_Real-Time_3D_Human_Pose_Reconstruction_CVPR_2020_paper.html)

* [Self-Supervised 3D Human Pose Estimation via Part Guided Novel Image Synthesis](http://openaccess.thecvf.com/content_CVPR_2020/html/Kundu_Self-Supervised_3D_Human_Pose_Estimation_via_Part_Guided_Novel_Image_CVPR_2020_paper.html)

#### 2D human pose estimation
* [HigherHRNet: Scale-Aware Representation Learning for Bottom-Up Human Pose Estimation](http://openaccess.thecvf.com/content_CVPR_2020/html/Cheng_HigherHRNet_Scale-Aware_Representation_Learning_for_Bottom-Up_Human_Pose_Estimation_CVPR_2020_paper.html)
  * Discussed with the author on 06-17 for this paper duing Q&A session
  * Why need to do higher resolution, because HRNet cannot deal with smaller person - bottom-up method suffers from it.
  * HigherHRNet do deconvolution to upsample to `1/2` of the input resolution and do a supervision, the result is better.
  * Why not going all the way up to full resolution? COCO dataset doesn't annotate smaller person, actually full resolution makes the result slightly worse. 

* [The Devil Is in the Details: Delving Into Unbiased Data Processing for Human Pose Estimation](http://openaccess.thecvf.com/content_CVPR_2020/html/Huang_The_Devil_Is_in_the_Details_Delving_Into_Unbiased_Data_CVPR_2020_paper.html)
  * Discussed with the author duing live Q&A session
  * Why need to do UDP (unbiased data processing)? because like flipping, processing on regular grid is discrete, cause precision problem, especially for smaller persons.
  * Why processing on regular grid is discrete is such an important issue for pose estimation, why not for object detection? A: because the evaluation of pose estimation is coordinate difference, sensitive to subpixel accuracy, especially for smaller person.
  * I suggested the authors to do a subset analysis to just compute the performance improvement on smaller persons, the improvement of this method may improve even more. 
  * I also tried to ask the author if the method applies to both buttom-up and top-down methods, buttom-up for sure, top-down, not so sure. The author seems to be not familar with detection bounding box. And then the connect lost, the connect of zoom live session was not stable. 

* [UniPose: Unified Human Pose Estimation in Single Images and Videos](http://openaccess.thecvf.com/content_CVPR_2020/html/Artacho_UniPose_Unified_Human_Pose_Estimation_in_Single_Images_and_Videos_CVPR_2020_paper.html)

* [15 Keypoints Is All You Need](http://openaccess.thecvf.com/content_CVPR_2020/html/Snower_15_Keypoints_Is_All_You_Need_CVPR_2020_paper.html)
  * The transformer module make it very efficient, it's being the 1 on PoseTrack leaderboard for 4 months from 2019 to 2020. 

* [Distribution-Aware Coordinate Representation for Human Pose Estimation](http://openaccess.thecvf.com/content_CVPR_2020/html/Zhang_Distribution-Aware_Coordinate_Representation_for_Human_Pose_Estimation_CVPR_2020_paper.html)
  * No. 3 ICCV'19 COCO keypoints detection challenge (code avaiable). 
  * Decode the predicted heat map, maximum relocation, and resolution recovery.  

#### 3D human pose estimation - multi-view

