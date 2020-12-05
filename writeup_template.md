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

My pipeline consisted of 5 steps:
1. Convert the images to grayscale
[image2]: ./test_images_output/solidWhiteCurve_gray.jpg "Grayscale"
2. Apply Gaussuan Blur to smooth the images
[image3]: ./test_images_output/solidWhiteCurve_blur_gray.jpg "Gaussian Blur"
3. Perform edge detection
[image4]: ./test_images_output/solidWhiteCurve_edges.jpg "Canny"
4. Find the region of interest in order to focus only on the part of the images where lane lines are more likely to be
[image5]: ./test_images_output/solidWhiteCurve_masked_edges.jpg "Region of interest"
5. From the points detected in the edge detection step, masked by the region of interest, find continuous lane lines.
[image6]: ./test_images_output/solidWhiteCurve_output.jpg "Lane Lines"

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:
1. computing the slope and intercept for each line
2. dividing the lines into two groups: lines with positive slope and lines with negative slope
3. computing the average slope and intercept for each of the two group of lines
4. using the avg slope and intercept computed in the previous step reconstruct the two lines


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the road is not straight but turns to the left or the right, or even during a change in the slope of the road (uphill/downhill). Using a first grade equation (y=mx+b) to derive the lane lines even a small curve in the lanes could lead to missinterpretaions.

Another potential shortcoming would be extracting a region of interest from original images using fixed parameters. This could lead to filter out the lane lines that we are trying to detect. 


### 3. Suggest possible improvements to your pipeline

A possible improvement to the detection of curve lane lines could be to use an higher grade equation to derive the lane lines.

In the case of the fixed parameter a possible improvement could be to use 
