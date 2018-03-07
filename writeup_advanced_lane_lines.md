## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Advanced Lane Finding Project**

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

[//]: # (Image References)

[image1]: ./examples/undistort_output.png "Undistorted"
[image2]: ./test_images/test1.jpg "Road Transformed"
[image3]: ./examples/binary_combo_example.jpg "Binary Example"
[image4]: ./examples/warped_straight_lines.jpg "Warp Example"
[image5]: ./examples/color_fit_lines.jpg "Fit Visual"
[image6]: ./examples/example_output.jpg "Output"
[video1]: ./project_video.mp4 "Video"

## [Rubric](https://review.udacity.com/#!/rubrics/571/view) Points

### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---

### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  [Here](https://github.com/udacity/CarND-Advanced-Lane-Lines/blob/master/writeup_template.md) is a template writeup for this project you can use as a guide and a starting point.  

You're reading it!

All my code is in the file "advanced_lane_line.ipynb"

### Camera Calibration

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

code of calibrate camera is in the function "calibrate_camera"

effection of undistort:

![undistort of calibrate image]('output_images/undistort-camera.png')

### Pipeline (single images)

#### 1. Provide an example of a distortion-corrected image.

To demonstrate this step, I will describe how I apply the distortion correction to one of the test images like this one:

![undistort of example image]('output_images/undistort-example.png')

#### 2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.

i combined sobel, hls and lab color space fetures to create a thresholded binary image.

- code of sobel thresholded image is in the function "apply_sobel_threshold"

thresholded binary image of sobel features:

![sobel feature image]('output_images/sobel_feature.png')

- code of hls thresholded image is in the function "apply_hls_threshold"

thresholded binary image of hls features:

![hls feature image]('output_images/hls_feature.png')

- code of lab thresholded image is in the function "apply_lab_threshold"

thresholded binary image of hls features:

![hls feature image]('output_images/lab_feature.png')

#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

my perspective transform includes two functions, one function called "perspective_transform", another function called "get_perspective_transform_from_image_data"

I chose the hardcode the source and destination points in the following manner:

```python
src = np.float32([(575,464),
                  (707,464), 
                  (258,682), 
                  (1049,682)])
    dst = np.float32([(450,0),
                  (w-450,0),
                  (450,h),
                  (w-450,h)])```

This resulted in the following source and destination points:

| Source        | Destination   | 
|:-------------:|:-------------:| 
| 575, 464      | 450, 0        | 
| 707, 464      | 830, 0      |
| 258, 692	    | 450, 720      |
| 1049, 682      | 830, 720        |

I verified that my perspective transform was working as expected by drawing the `src` and `dst` points onto a test image and its warped counterpart to verify that the lines appear parallel in the warped image.

![perspective transform]('./test_images/perspective_transform.png')

#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

i identified lane line and draw them in two functions, one function called "sliding_window_polyfit", another function called "draw_lane", for example:

![lane line identification]('./test_images/lane_line_identify.png')

![lane line draw]('./test_images/lane_line_draw.png')

#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

I did this in the function "calc_curv_rad_and_center_dist"

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

I implemented this step in the function "draw_line"

![curv and radius example]('./test_images/radius_curv_lane_line.png')

---

### Pipeline (video)

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a [link to my project video result](./output_videos/project_video.mp4)

Here's a [link to my challenge video result](./output_videos/challenge_video.mp4)

Here's a [link to my challenge video result](./output_videos/harder_challenge_video.mp4)

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further. 

in some frame of video, correctness of lane line identifying have more improvements, it needs more smooth algorithm to do with it. 
