# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

Five steps to detecting the lane lines. 1) For ease convert the image to grayscale. 2) To reduce noise in our image apply a Gaussian smoothing. 3) To identify the edge use the Canny edge detection algorithm. 4) To focus on the lanes only, mask only the region with the lanes. 5) To connect the edges detected as lines run the Hough transform.

I modified the draw_lines function to return the least squares solution to the lines found by the Hough transform algorithm. This allows us to interpolate the segmented lines in the lanes to lanes. The function sorts the left lane vs right lane lines by looking at the negative vs positive slopes and also takes note of the max x coordinate for the left lane and the min x coordinate for the right lane. These are necessary to draw the lanes from the most right point of the left lane and the most left point of the right lane. The most left point of the left lane can be found by using the least squares equation with y as the max height of the image. Same for the most right point of the right lane. This gets us the resulting images in the test_videos_output directory with the names prefixed with "processed_".

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline

My current pipeline takes a few assumptions such as the masking of the lane. A potential shortcoming would be if the camera were not positioned ideally or if the lanes were wider. Pipeline also assumes clear visibility of the lanes. Possible shortcomings from this assumption can be obstacles that obstruct the view of the lanes or lack of visibility because of darkness.

### 3. Suggest possible improvements to your pipeline

I could make improvements to the efficiency of my draw lines code. The least squares function iterates over the lines that I manually iterate to sort from left to right.
