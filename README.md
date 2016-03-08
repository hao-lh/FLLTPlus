# FLLT+
Some improvements on current [fast level line transform (FLLT)](http://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=841532) algorithm.

# FLLT
Fast Level Line Transform (FLLT), originally postponed by Pascal Monasse and Frédéric Guichard at May 2000, with the idea of combining max-tree and min-tree to form a non-reduant tree of shapes (TOS), has following features:

* Adaptive to scale transform, which is common in computer vision segmentation.
* Invariant to contrast, which means the TOS remains the same before and after a monotonous function acts on image I.

However, FLLT has two limitations:

* FLLT trends to provide an over-segmented image, resulting in many fractured shapes, which was in-dominant during visual perception and result in heavy burden on network transmission as well as local storage.
* FLLT makes no distinction on targets and bakcground, which is controversal to our purpose, as details are only needed on human region of interest (ROI) areas.

# Procedure
To overcome the above issues, this work proposed:

* Detect target regions with [MB+](http://cs-people.bu.edu/jmzhang/fastmbd.html) algorithm.
* Combine non-dominant regions in the background to advoid eye-distracting as well as many other issues.

