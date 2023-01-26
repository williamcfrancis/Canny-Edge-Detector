# Canny Edge Detector

## Introduction
The Canny Edge Detector is a popular algorithm used to detect edges in an image. This implementation uses the following steps:
* Filter image by derivatives of Gaussian
* Compute magnitude of gradient
* Compute edge orientation
* Detect local maximum
* Edge linking
* Threshold Tuning

The final goal of this project is to compute the Canny Edges for any RGB image, as shown in the example below:
![image](https://user-images.githubusercontent.com/38180831/214776238-fe0313e0-7490-4213-a629-430e4fbbeea8.png)

The inputs for the algorithm are:

* (INPUT) I: H x W x 3 matrix representing the RGB image, where H, W
are the height and width of the input image respectfully.
* (OUTPUT) E: H x W binary matrix representing the canny edge map,
where a 1 is an Edge pixel while 0 is a Non-Edge pixel.

## Usage
1. Open [canny_edge_detector.ipynb](https://github.com/williamcfrancis/canny-edge-detector/blob/main/canny_edge_detector.ipynb) using Google colab, Jupyter Notebook or other supporting ipynb editor. 
2. Download the images and load it into the notebook.
3. Run the cells sequentially

## Image Derivative
The function findDerivatives implements Gaussian smoothing and computes the magnitude and orientation of derivatives for the image.
* (INPUT) I_gray: H x W matrix representing the grayscale image.
* (OUTPUT) Mag: H x W matrix representing the magnitude of deriva-
tives.
* (OUTPUT) Magx: H x W matrix representing the magnitude of deriva-
tives along the x-axis.
* (OUTPUT) Magy: H x W matrix representing the magnitude of deriva-
tives along the y-axis.
* (OUTPUT) Ori: H x W matrix representing the orientation of derivatives.

## Detect Local Maximum
The function nonMaxSup finds local maximum edge pixels using non-maximum suppression along the line of the gradient, further suppressing noise.
* (INPUT) Mag: H x W matrix representing the magnitude of derivatives.
* (INPUT) Ori: H x W matrix representing the orientation of derivatives.
* (OUTPUT) M: H x W binary matrix representing the edge map after non-maximum suppression.

## Edge Linking 
After non-maximum suppression, we have a potential edge map. To get the final result, we use low and high thresholds to divide current edges into three categories. If the Magnitude of the edge is below the low threshold, then it is considered noise and discarded. If it is above the high threshold, then we accept it as part of the final edge map. These edges are also known as strong edges. For edges that fall between the two thresholds, we are uncertain about them and these edges are also known as weak edges. In the edgeLink function, we try to link weak edges to strong edges. Those weak edges that can be connected to strong edges stay in the final edge map, and others are discarded.

* (INPUT) M: H x W logical map after non-max suppression
* (INPUT) Mag: H x W matrix represents the magnitude of gradient
* (INPUT) Ori: H x W matrix represents the orientation of gradient
* (INPUT) low: low threshold
* (INPUT) high: high threshold
* (OUTPUT) E: H x W binary matrix represents the final canny edge de-
tection map

## Threshold Tuning
For each image, we need to tune low and high thresholds and keep the result
in the thresh_dict. The rule of thumb is to tune the high threshold so that
enough edges are preserved and then setting low threshold to be around 0.4
high threshold to remove noise

## Results

![image](https://user-images.githubusercontent.com/38180831/214779496-52ec8c95-e7fc-4d6b-89b1-9448f4110a7a.png)

![image](https://user-images.githubusercontent.com/38180831/214779540-d132255a-1fa5-47d6-818f-8309a456b131.png)

![image](https://user-images.githubusercontent.com/38180831/214779654-41d7c1b2-9cf0-48d2-b35b-7f34a6963f36.png)

![image](https://user-images.githubusercontent.com/38180831/214779708-3cfa2f48-538c-45db-b007-460c4b52d258.png)

## Future Work
There are a few ways to improve the current implementation of the Canny Edge Detector algorithm. Some of the possible future work includes:

1. Parallel Processing: The current implementation of the algorithm is single-threaded, and thus it may take a significant amount of time to process large images. To speed up the process, we could parallelize the algorithm using multi-threading or GPU processing.

2. Adaptive Thresholding: The current implementation uses a fixed low and high threshold for all images. However, different images may require different threshold values to achieve the best results. An adaptive thresholding technique could be implemented to automatically adjust the threshold values based on the characteristics of the input image.

3. Robustness to Noise: The current implementation of the algorithm is sensitive to noise, and it may produce false edges in the presence of noise. To improve the robustness of the algorithm to noise, we could incorporate techniques such as median filtering or bilateral filtering.

4. Real-time Processing: The current implementation of the algorithm is suitable for offline processing, but it may not be suitable for real-time processing. To make the algorithm suitable for real-time processing, we could implement an optimized version of the algorithm that is more computationally efficient.
