# OpenCV_GeometricAI

![image](https://github.com/wayne540500/OpenCV_GeometricAI/assets/69573286/18fa8cea-eab1-4a01-8de5-0f69a1f27d06)

Title: Understanding ORB in OpenCV

Introduction:
For enthusiasts of OpenCV, the ORB (Oriented FAST and Rotated BRIEF) algorithm holds a special significance, particularly because it originated from the innovative minds at "OpenCV Labs." In 2011, Ethan Rublee, Vincent Rabaud, Kurt Konolige, and Gary R. Bradski introduced this groundbreaking algorithm in their paper titled "ORB: An efficient alternative to SIFT or SURF." As the title suggests, ORB offers an attractive alternative to SIFT and SURF in terms of computational efficiency, matching performance, and, most notably, the absence of restrictive patents – unlike SIFT and SURF.

Key Components of ORB:
ORB can be thought of as a fusion of the FAST keypoint detector and the BRIEF descriptor, with several enhancements to boost its performance. Here's how it works:

Keypoint Detection:

ORB initially employs FAST to identify keypoints in an image.
It then applies the Harris corner measure to select the top N keypoints.
Additionally, ORB utilizes a pyramid approach to create multiscale features, enhancing its robustness.
Orientation Handling:

FAST doesn't calculate orientation, posing a challenge for rotation invariance.
To overcome this, ORB calculates the intensity-weighted centroid of the patch centered on the detected corner. The vector from this corner to the centroid determines the orientation.
For improved rotation invariance, moments are computed based on the patch's size within a circular region of radius r.
Descriptor Generation:

ORB employs BRIEF descriptors. However, BRIEF is known to perform poorly with rotation.
To address this, ORB "steers" BRIEF according to the orientation of keypoints. It rotates the BRIEF pattern according to the patch's orientation.
Steering and Descriptors:

ORB discretizes the angle into 12-degree increments, creating a lookup table of precomputed BRIEF patterns.
When the keypoint orientation θ is consistent across views, the appropriate set of rotated BRIEF patterns (Sθ) is used to compute the descriptor.
rBRIEF:

ORB conducts a search among all possible binary tests to select those with high variance, means close to 0.5, and low correlation. This optimized result is referred to as rBRIEF.
Descriptor Matching:

ORB employs multi-probe Locality-Sensitive Hashing (LSH) for descriptor matching, improving upon traditional LSH.
The paper indicates that ORB outperforms SURF and SIFT in terms of speed and descriptor quality, making it an ideal choice for low-power devices, such as panorama stitching.
Using ORB in OpenCV:
To use ORB in OpenCV, you need to create an ORB object through the cv.ORB() function or by utilizing the feature2d common interface. You can specify various optional parameters, including nFeatures (maximum retained features), scoreType (Harris score or FAST score for feature ranking), and WTA_K (number of points for oriented BRIEF descriptor, affecting the matching distance).

In practice, ORB proves to be a valuable tool for computer vision tasks such as panorama stitching and more, offering a powerful and patent-free alternative to traditional feature detection and description methods.

reference: https://docs.opencv.org/3.4/d1/d89/tutorial_py_orb.html
picture: https://thirdspacelearning.com/blog/what-are-2d-and-3d-shapes/
