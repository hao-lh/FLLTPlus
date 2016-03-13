# FLLTPlus
Some enhancement on current [Fast Level Line Transform (FLLT)](http://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=841532) algorithm.

# FLLT
![synthetic_image](https://cloud.githubusercontent.com/assets/14138581/13603173/3ef60370-e576-11e5-9085-e0dc8f51aa8b.png)
FLLT was originally proposed by *Pascal Monasse* and *Frédéric Guichard* in 2000, by combining `lower level tree` as well as `upper level tree` to form a non-reduant `tree of shapes (TOS)` structure of original image, with following features:

* **Adaptive to scale transform**, which was inevitable in segmentation etc. applications.
* **Invariant to contrast change**, where **image's topological structure** can be preserved before and after **monotonous functions'** acting on TOS.

Despite FLLT's brilliant performance, there still exists some limitations:

1. FLLT makes no distinction on target and bakcground areas, which is controversal to our purpose, only details from human's `region of interest (ROI)` areas are needed, those non-dominant fragmentized regions could break human's visual perception process, which should be avoided.
2. FLLT tends to provide an `over-segmentation` image, resulting in many fragmentized shapes, especially those laid in image's background, which can hardly be noticed, but add burden on network transmission as well as local arcievement.

# Procedure
Some enhancement was made in this work to overcome above mentioned issues respectively:

* Add [saliency detection model](http://mmcheng.net/zh/salobjbenchmark/) with imitation of human's [fixation](https://en.wikipedia.org/wiki/Fixation_(visual)) and [saccade](https://en.wikipedia.org/wiki/Saccade) process and extract regions with salient geometric and texture structure as target (ROI), while remaining as backgroud. Especially a [MB+](http://cs-people.bu.edu/jmzhang/fastmbd.html) saliency detection model was adopted with consideration of performance and efficiency.
* Convert image from [RGB Color Space](https://en.wikipedia.org/wiki/RGB_color_space) to [CIE Lab Color Space](https://en.wikipedia.org/wiki/Lab_color_space) and perform FLLT on image's L band.
* Merge non-dominant regions in image's background regions.

![ds02w](https://cloud.githubusercontent.com/assets/14138581/13728326/76bceb5c-e94f-11e5-87e2-62d4564e0b43.png)
![ds03w](https://cloud.githubusercontent.com/assets/14138581/13728327/76c53a6e-e94f-11e5-9824-2c43c0e6a154.png)
![ds04w](https://cloud.githubusercontent.com/assets/14138581/13728328/76cc4c0a-e94f-11e5-967f-407fb0e7a876.png)

Result of the algorithm on synthetic image can be seen as follows, with merging conditions from loose to strict.
![synthetic_result](https://cloud.githubusercontent.com/assets/14138581/13603181/4fffbaa8-e576-11e5-8350-ddac5fbcc021.png)

# Experiment
![scene_result](https://cloud.githubusercontent.com/assets/14138581/13603186/573a934c-e576-11e5-846d-ab7316b328b5.png)
Here we adopted [MIT300 saliency dataset](http://saliency.mit.edu) to validate our algorithm, the results are as follows:

* first column is original image.
* second column is MB+ saliency detection result on original image.
* columns from three to five corresponding to image's simplification results, with merging conditions from loose to strict.

# Copyright
[GNU LGPLv3](http://choosealicense.com/licenses/lgpl-3.0/)
