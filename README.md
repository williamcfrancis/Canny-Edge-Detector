# Canny Edge Detector

## Introduction
Canny edge detector is implemented via,
* Filter image by derivatives of Gaussian
* Compute magnitude of gradient
* Compute edge orientation
* Detect local maximum
* Edge linking
* Threshold Tuning

The final goal of this project is to compute the Canny Edges for any RGB image as shown below:
![image](https://user-images.githubusercontent.com/38180831/214776238-fe0313e0-7490-4213-a629-430e4fbbeea8.png)

* (INPUT) I: H x W x 3 matrix representing the RGB image, where H, W
are the height and width of the input image respectfully.
* (OUTPUT) E: H x W binary matrix representing the canny edge map,
where a 1 is an Edge pixel while 0 is a Non-Edge pixel.

Tasks:
1. Apply Gaussian smoothing and compute local edge gradient magnitude
as well as orientation.
2. Seek local maximum edge pixel in corresponding orientation.
3. Find the appropriate thresholds to get good edges

## Image Derivative
We implement Gaussian smoothing, compute magnitude and orientation of derivatives for the image.
* (INPUT) I_gray: H x W matrix representing the grayscale image.
* (OUTPUT) Mag: H x W matrix representing the magnitude of deriva-
tives.
* (OUTPUT) Magx: H x W matrix representing the magnitude of deriva-
tives along the x-axis.
* (OUTPUT) Magy: H x W matrix representing the magnitude of deriva-
tives along the y-axis.
* (OUTPUT) Ori: H x W matrix representing the orientation of derivatives.

## Detect Local Maximum
The function ’nonMaxSup’ is to find local maximum edge pixel using non-
maximum suppression along the line of the gradient. The operation further
suppresses noises.
* (INPUT) Mag: H x W matrix representing the magnitude of derivatives.
* (INPUT) Ori: H x W matrix representing the orientation of derivatives.
* (OUTPUT) M: H x W binary matrix representing the edge map after non-maximum suppression.

## Edge Linking 
After non maximum suppression, we have the potential edge map. To get the
final result, we use low and high thresholds to divide current edges to three
categories. If the Magnitude of the edge is below low threshold, then it is noise
and we discard it. If it is above high threshold, then we accept it as part of final
edge map. We also call it the strong edge. For these edges that are between two
thresholds, we are uncertain about them. They are also known as weak edges.
In the edgeLink function, we try to link weak edges to strong edges. Those
weak edges that can be connected to strong edges stay in the final edge map
and others are discarded. 

* (INPUT) M: H x W logical map after non-max suppression
* (INPUT) Mag: H x W matrix represents the magnitude of gradient
* (INPUT) Ori: H x W matrix represents the orientation of gradient
* (INPUT) low: low threshold
* (INPUT) high: high threshold
* (OUTPUT) E: H x W binary matrix represents the final canny edge de-
tection map

