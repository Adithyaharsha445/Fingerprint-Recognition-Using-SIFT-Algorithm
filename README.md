# Fingerprint Recognition Using SIFT Algorithm

## Introduction
This project demonstrates the use of the Scale-Invariant Feature Transform (SIFT) algorithm for fingerprint recognition. The primary goal of the project is to match a sample fingerprint image against a collection of real fingerprint images using keypoint detection and feature matching.

## Prerequisites
Before running the code, ensure that you have the following Python packages installed:

- `opencv-python`: OpenCV library to handle image processing tasks.
- `opencv-contrib-python`: This includes extra modules such as SIFT.
- `matplotlib`: For visualizing images and keypoints.
- `numpy`: For numerical computations.

To install the necessary packages, run the following commands:

```bash
pip install opencv-python opencv-contrib-python matplotlib numpy


## Project Workflow

### 1. Loading and Displaying the Sample Fingerprint Image
The first step in the fingerprint recognition process involves loading the sample fingerprint image from a specified file path. The image is then displayed using matplotlib.

### 2. Initializing the SIFT Detector
The SIFT algorithm is initialized using OpenCV’s `cv2.SIFT_create()` function. This function will detect keypoints and compute descriptors for the fingerprint images. These keypoints are used to match features between the sample image and the real fingerprint images.

### 3. Loading Real Fingerprint Images
Real fingerprint images are loaded from a folder specified in the code. The `glob` library is used to list all `.BMP` files from the directory. These images will be compared against the sample image.

### 4. Feature Matching Using FLANN-based Matcher
The FLANN-based Matcher (Fast Library for Approximate Nearest Neighbors) is used for matching the descriptors between the sample fingerprint and the real fingerprint images.

- **K-Nearest Neighbors (k-NN)**: For each keypoint descriptor in the sample image, we find the k-nearest neighbors in the real fingerprint images.
- **Lowe's Ratio Test**: To filter out poor matches, we apply Lowe’s ratio test. If the distance of the first match is less than 0.1 times the distance of the second match, it is considered a good match.

### 5. Visualizing Keypoints in the Sample Image
The detected keypoints in the sample fingerprint image are drawn using OpenCV’s `cv2.drawKeypoints()` function. These keypoints are displayed using matplotlib to provide a visual understanding of where the SIFT algorithm has detected features.

### 6. Finding and Displaying the Best Match
The code compares all fingerprint images in the folder and calculates a match score based on the number of good keypoint matches. The best match (the image with the highest match score) is identified and displayed along with the match score.

### 7. Drawing Matches Between the Sample and Best Matching Fingerprint
Finally, the matches between the sample fingerprint and the best matching real fingerprint image are visualized. The matches are drawn using `cv2.drawMatches()` and displayed using matplotlib.

## Results
The program outputs the best match (file path of the real fingerprint image) along with the match score. It also displays the keypoints detected in the sample image, and the result of the best match with its visual representation of matching points.


## Sample Output:
BEST MATCH: C:/Users/dell/Downloads/SOCOFing/Real\150__M_Left_index_finger.BMP SCORE: 20.51282051282051

## Visualizations:
- **Keypoints in Sample Image**: This shows the keypoints detected by the SIFT algorithm in the sample fingerprint image.
- **Best Match Visualization**: A side-by-side image showing the best match between the sample and a real fingerprint image with the matching keypoints connected.

## Code Walkthrough

### Installing Required Packages
The first step is to install the required libraries:

```bash
pip install opencv-python opencv-contrib-python matplotlib numpy



### Loading the Sample Image
python
Copy code
sample = cv2.imread("path_to_sample_image")
This loads the sample fingerprint image for recognition.

#### SIFT Initialization and Real Image Loading
python
Copy code
sift = cv2.SIFT_create()
real_images = glob.glob("path_to_real_images/*.BMP")
Here, the SIFT detector is initialized, and real fingerprint images are loaded from the specified directory.

### Keypoint Detection and Matching
python
Copy code
keypoints_1, descriptors_1 = sift.detectAndCompute(sample, None)
keypoints_2, descriptors_2 = sift.detectAndCompute(fingerprint_image, None)
The SIFT algorithm detects keypoints and computes descriptors for both the sample and the real fingerprint images. These descriptors are then matched using FLANN-based matching.

### Visualization of Keypoints
python
Copy code
keypoint_image = cv2.drawKeypoints(sample, keypoints_1, None)
Keypoints are drawn on the sample image for visualization.

![image](https://github.com/user-attachments/assets/ffb67d91-a150-4711-96da-c6cdaa759c7e)


### Finding the Best Match
python
Copy code
matches = flann.knnMatch(descriptors_1, descriptors_2, k=2)
The best match is computed by comparing the descriptors of the sample fingerprint image with those in the real images.

### Displaying the Result
python
Copy code
result = cv2.drawMatches(sample, kp1, image, kp2, mp, None)

The best match is displayed by drawing lines between matching keypoints in the sample and the best-matching real fingerprint image.

![image](https://github.com/user-attachments/assets/74a8b621-906c-485a-89f3-2f7cfd02a00b)

