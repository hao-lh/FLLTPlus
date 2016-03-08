# FLLTPlus
Some enhancement on current [`Fast Level Line Transform (FLLT)`](http://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=841532) algorithm.

# FLLT
FLLT was originally proposed by *Pascal Monasse* and *Frédéric Guichard* in 2000, by combining `lower level tree` as well as `upper level tree` to form a non-reduant `tree of shapes (TOS)` structure of original image, with following features:

* **Adaptive to scale transform**, which was inevitable in segmentation etc. applications.
* **Invariant to contrast change**, which means TOS can **preserve image's topological structure** before and after **monotonous functions'** acting.

Despite FLLT's brilliant performance, there still exists some limitations:

1. FLLT makes no distinction on target and bakcground areas, which is controversal to our purpose, only details from human's `region of interest (ROI)` areas are needed, those non-dominant fragmentized regions could break human's visual perception process, which should be avoided.
2. FLLT tends to provide an `over-segmentation` image, resulting in many fragmentized shapes, especially those laid in image's background, which can hardly be noticed, but add burden on network transmission as well as local arcievement.

# Procedure
Some enhancement was made in this work to overcome above mentioned issues respectively:

* Add [`saliency detection model`](http://saliency.mit.edu) with imitation of human's [`fixation`](https://en.wikipedia.org/wiki/Fixation_(visual)) and [`saccade`](https://en.wikipedia.org/wiki/Saccade) process and extract regions with salient geometric and texture structure as target (ROI), while remaining as backgroud. Especially a [MB+ saliency detection model](http://cs-people.bu.edu/jmzhang/fastmbd.html) was adopted with consideration of performance and efficiency.
* Convert image from [`RGB Color Space`](https://en.wikipedia.org/wiki/RGB_color_space) to [`CIE Lab Color Space`](https://en.wikipedia.org/wiki/Lab_color_space) and perform FLLT on image's L band.
* Merge non-dominant regions in image's background regions.

# Experiment
Here we adopted MIT300 dataset to validate our algorithm, the results are as follows:

* first column is original image
* second column is MB+ saliency detection result on original image
* columns from three to five corresponding to image's simplification results with parameters from strict to loose.
