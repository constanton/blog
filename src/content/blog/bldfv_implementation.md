---
title: "An implementation of a person (and object) re-identification method"
pubDate: "2014-11-30T21:46:52.000Z"
description: "Implementing Fisher-vector person re-identification in C++ with OpenCV and VLFeat."
---
Hi! I would like to present you my latest upload on GitHub:

[https://github.com/constanton/bLDFV](https://github.com/constanton/bLDFV "bLDFV on GitHub")

It’s the implementation of a research publication on human re-identification \[1\] in C++ (…with a very minimal OO design though).

This programme was created for academic purposes (!) and it can most probably also be used to re-identify other (similarly distinctive) objects as well, although this has not been tested. It divides the image into 3×4 blocks and uses very simple features (HSV values, first and second order derivatives).

As you will see on the GitHub page, the programme uses the open source [OpenCV](http://opencv.org/ "OpenCV") and [VLFeat](http://www.vlfeat.org/ "VLFeat") libraries. Also, it was developed on a Fedora 19 64bit machine using the Eclipse IDE.

I am aware that without proper documentation, the learning curve for using this programme might be steep but I hope I will find time to prepare something. All configuration happens inside the config.xml file. Using this file, after the training procedure (function zero), the programme creates a _gmm\_parameters.xml_ file which must be used aftewards during all other program functions (one, two and three) in order to produce the _fisher.xml_ files that contain the image’s Fisher vectors and the .csv files that contain the Euclidean distances. The results are very similar to those of the publication using the same evaluation methods.

Nonetheless, improvements can be made. For example, during the training process, there is no random selection of the image features. This will improve the performance of the programme. Various other improvements are also possible.

\[1\] B. Ma, Y. Su, and F. Jurie, “[Local descriptors encoded by fisher vectors for person re-identification](https://jurie.users.greyc.fr/papers/12_ECCVW_reidentification.pdf "Local descriptors encoded by Fisher vectors")” in ECCV Workshops (1) (A. Fusiello, V. Murino, and R. Cucchiara, eds.), vol. 7583 of Lecture Notes in Computer Science, pp. 413–422, Springer, 2012.
