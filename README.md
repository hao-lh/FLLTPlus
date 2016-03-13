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

![ds01w](https://cloud.githubusercontent.com/assets/14138581/13728372/05770728-e951-11e5-99f3-10ba73ee46d6.png)
![ds02w](https://cloud.githubusercontent.com/assets/14138581/13728374/05775d54-e951-11e5-8ee5-9912f3f49217.png)
![ds03w](https://cloud.githubusercontent.com/assets/14138581/13728371/0572d16c-e951-11e5-8fcd-a467c6063f03.png)
![ds04w](https://cloud.githubusercontent.com/assets/14138581/13728373/057746fc-e951-11e5-8e91-6472776c63ec.png)

# Experiment
Result of the algorithm on synthetic image can be seen as follows, with merging conditions from loose to strict.
![synthetic_result](https://cloud.githubusercontent.com/assets/14138581/13603181/4fffbaa8-e576-11e5-8350-ddac5fbcc021.png)

Part of algorithm's performance on [MIT300 saliency detection dataset](http://saliency.mit.edu), ranging from people, animals, architecture, artificial objects to natural scene, with merging conditions from loose to strict.
![scene_result](https://cloud.githubusercontent.com/assets/14138581/13729089/7010d12a-e967-11e5-9e03-ff7b773b0772.png)

* first column is original image.
* second column is MB+ saliency detection result on original image.
* columns from three to five corresponding to image's simplification results, with merging conditions from loose to strict.

# Miscellaneous
* Copyright: [GNU LGPLv3](http://choosealicense.com/licenses/lgpl-3.0/)
* Special thanks to reference code [MegaWave2](https://github.com/nilx/megawave) and discussion with [Pascal Monasse](mailto:monasse@imagine.enpc.fr)
