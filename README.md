# FLLTPlus
Some enhancement on current [`Fast Level Line Transform (FLLT)`](http://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=841532) algorithm.

# FLLT
FLLT was originally proposed by *Pascal Monasse* and *Frédéric Guichard* in 2000, by combining `lower level tree` as well as `upper level tree` to form a non-reduant `tree of shapes (TOS)` structure of original image, with following features:

* **Adaptive to scale transform**, which was inevitable in segmentation etc. applications.
* **Invariant to contrast change**, where **image's topological structure** can be preserved before and after **monotonous functions'** acting on TOS.

Despite FLLT's brilliant performance, there still exists some limitations:

1. FLLT makes no distinction on target and bakcground areas, which is controversal to our purpose, only details from human's `region of interest (ROI)` areas are needed, those non-dominant fragmentized regions could break human's visual perception process, which should be avoided.
2. FLLT tends to provide an `over-segmentation` image, resulting in many fragmentized shapes, especially those laid in image's background, which can hardly be noticed, but add burden on network transmission as well as local arcievement.

# Procedure
Some enhancement was made in this work to overcome above mentioned issues respectively:

* Add [`saliency detection model`](http://mmcheng.net/zh/salobjbenchmark/) with imitation of human's [`fixation`](https://en.wikipedia.org/wiki/Fixation_(visual)) and [`saccade`](https://en.wikipedia.org/wiki/Saccade) process and extract regions with salient geometric and texture structure as target (ROI), while remaining as backgroud. Especially a [MB+](http://cs-people.bu.edu/jmzhang/fastmbd.html) saliency detection model was adopted with consideration of performance and efficiency.
* Convert image from [`RGB Color Space`](https://en.wikipedia.org/wiki/RGB_color_space) to [`CIE Lab Color Space`](https://en.wikipedia.org/wiki/Lab_color_space) and perform FLLT on image's L band.
* Merge non-dominant regions in image's background regions.

# Experiment
Here we adopted [MIT300 saliency dataset](http://saliency.mit.edu) to validate our algorithm, the results are as follows:

* first column is original image
* second column is MB+ saliency detection result on original image
* columns from three to five corresponding to image's simplification results with parameters from strict to loose.

# Copyright
The MIT License (MIT)
Copyright (c) <2016> <Hao>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
