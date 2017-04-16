<h2>Behavioral Cloning</h2>

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
 <<00>><<INSERT IMAGE HERE>>
 
 <h3>Perspective Transformation on Distortion corrected Images</h3><br>
 
 Perspective transformation is applied on the distortion corrected chess board image and the output is shown below:
 <<01><<INSERT IMAGE HERE>>
 
 <h3>Creating thresholded binary images</h3>
 Following approaches were used to generate thresholded binary images
 * <h5>Distortion Correction</h5>
 
  * Using Above stated approache, the distortion in the images was corrected. An example of distortion corrected image is shown below
<<02><<INSERT IMAGE HERE>> 

* <h5>Sobel gradient in X and Y directions</h5>
 
 * Sobel is joint Gausssian smoothing plus differentiation operation where we can specify the direction of derivatives to be taken, vertical or horizontal
 * Sobel gradient for a sample test image is shown below
 
* <h5>Gradient Magnitude</h5>
 
 * As a next step, I have applied threshold to overall magnitude of the gradient in both x and y directions using the formula:
      abs_sobxy = sqrt(sobel(x)^2 + sobel(y)^2)
    
* <h5>Gradient Direction</h5>
 
 * As a next step, I have applied threshold to overall magnitude of the gradient in both x and y directions using the formula:
      abs_sobxy = sqrt(sobel(x)^2 + sobel(y)^2)
      
 
 
