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

<h3>Camera Matrix and Distortion coefficient Computation </h3><br>
Calculating Camera matrix and distortion coefficient involves following steps:<br>

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
 
 
