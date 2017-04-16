<h2>Advanced Lane Finding</h2>

[//]: # (Image References)

[image1]: ./images/00_Dist_Correction.jpg
[image2]: ./images/01_Perspective_Transformed.jpg
[image3]: ./images/02_Distortion_Corrected.jpg
[image4]: ./images/03_Sobel_Gradient.jpg
[image5]: ./images/04_Grad_Mag.jpg
[image6]: ./images/05_Grad_Dir.jpg
[image7]: ./images/06_Color_Thres.jpg
[image8]: ./images/07_Multi_Thres.jpg
[image9]: ./images/08_Perspective_Trans.jpg
[image10]: ./images/09_SlidingWindow.jpg
[image11]: ./images/10_Shaded_Lanes.jpg



The goals / steps of this project are the following:
  * Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
  * Apply a distortion correction to raw images.
  * Use color transforms, gradients, etc., to create a thresholded binary image.
  * Apply a perspective transform to rectify binary image ("birds-eye view").
  * Detect lane pixels and fit to find the lane boundary.
  * Determine the curvature of the lane and vehicle position with respect to center.
  * Warp the detected lane boundaries back onto the original image.
  * Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

<h3>Camera Matrix and Distortion coefficient Computation </h3>

Calculating Camera matrix and distortion coefficient involves following steps:
  * Calculate 
    * <b>Image points</b> - (x, y) pixel position of each of the corners in the image plane with each successful chessboard detection
    * <b>Object points</b> -  (x, y, z) coordinates of the chessboard corners in the grid for the chess grid using cv2.findChessboardCorners()
  * Calculate camera matrix and distortion using cv2.calibrateCamera() function
  * Using camera matrix and distortion from above step in cv2.undistort() to get the undistorted image
 
 Original vs Distortion corrected image is shown below
 ![alt text][image1]
 
 <h3>Perspective Transformation on Distortion corrected Images</h3><br>
 
 Perspective transformation is applied on the distortion corrected chess board image and the output is shown below:
 ![alt text][image2]
 
 <h3>Creating thresholded binary images</h3>
 
 Following approaches were used to generate thresholded binary images
 * <h5>Distortion Correction</h5>
 
   * Using Above stated approache, the distortion in the images was corrected. An example of distortion corrected image is shown below
![alt text][image3]

* <h5>Sobel gradient in X and Y directions</h5>

  * Sobel is joint Gausssian smoothing plus differentiation operation where we can specify the direction of derivatives to be taken, vertical or horizontal
Sobel gradient for a sample test image is shown below
 ![alt text][image4]
 
 * <h5>Gradient Magnitude</h5>
 
   * As a next step, I have applied threshold to overall magnitude of the gradient in both x and y directions using the formula:
       abs_sobxy = sqrt(sobel(x)^2 + sobel(y)^2)
![alt text][image5]

 * <h5>Gradient Direction</h5>
 
   * As a next step, the direction of the gradient is calculated which is the inverse tangent y gradient divided by x gradient
![alt text][image6]

 * <h5>Color Thresholds</h5>
 
   * Color Channel HLS and HSV Thresholding - I extracted the S-channel of the original image in HLS format and combine the result with the extracted V-channel of the original image in HSV format.
![alt text][image7]

 * <h5>Combined Thresholds</h5>
 
   * A combination of above stated approaches is experimented and used. Below image shows the difference between above individual thresholds and combinations
![alt text][image8]

<h4>Perspective Transformation</h4>

Perspective transform is applied on the binary thresholded images to generate an image with the effect of looking down on the road from above. OpenCV warpPerspective() function helps with this. I have defined a preset coordinate list to use for the perspective transformation, and the OpenCV getPerspectiveTransform() function generates a perspective matrix using these.

On applying perspective transformation, the image looks as follows

![alt text][image9]

<h3>Finding Lanes</h3>

In this step, we extract the lane pixels from right and left lanes and to fit their positions using a polynomial. After developing functions for sliding_windows and shaded_lanes, lanes are seen as below:

![alt text][image10]
![alt text][image11]

<h3> Fitting the Lanes </h3>

 * Once the right and left lanes are identified as above, the radius of curvature for each lane is estamitaed using polynomial fitting. The U.S. government specifications for highway curvature data is used for checking the quality of the estimates. 
* I have tracked the changes in left_x and right_x from frame to frame to check the qualit of the estimate


