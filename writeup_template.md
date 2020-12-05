# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

<div align="center">
    <img src="https://github.com/Ventu012/P1_FindingLaneLines/blob/main/examples/line-segments-example.jpg" width="500" />
</div>

---

### Reflection

### 1. Pipeline Description and draw_lines() Function

My pipeline consisted of 5 steps:
1. Convert of input images to grayscale
<div align="center">
    <img src="https://github.com/Ventu012/P1_FindingLaneLines/blob/main/test_images_output/solidWhiteCurve_gray.jpg" width="500" />
</div>

2. Apply Gaussian Blur to smooth the images
<div align="center">
    <img src="https://github.com/Ventu012/P1_FindingLaneLines/blob/main/test_images_output/solidWhiteCurve_blur_gray.jpg" width="500" />
</div>

3. Perform edge detection
<div align="center">
    <img src="https://github.com/Ventu012/P1_FindingLaneLines/blob/main/test_images_output/solidWhiteCurve_edges.jpg" width="500" />
</div>

4. Find the region of interest in order to focus only on the part of the images where lane lines are more likely to be
<div align="center">
    <img src="https://github.com/Ventu012/P1_FindingLaneLines/blob/main/test_images_output/solidWhiteCurve_masked_edges.jpg" width="500" />
</div>

5. From the points detected in the edge detection step, masked by the region of interest, find continuous lane lines.
<div align="center">
    <img src="https://github.com/Ventu012/P1_FindingLaneLines/blob/main/test_images_output/solidWhiteCurve_output.jpg" width="500" />
</div>


---

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:
1. Computing the slope and intercept for each line
2. Dividing the lines into two groups: lines with positive slope and lines with negative slope
3. Computing the average slope and average intercept for each of the two groups of lines. This is done considering only lines with length greater than 80 and a slope, in absolute value, between 0.5 and 0.8
4. Using the average slope and intercept computed in the previous step reconstruct the two lines (left and right)


### 2. Potential shortcomings of the current pipeline


A potential flaw could be what would happen when the road is not straight but turns left or right, or even when a slope change (uphill / downhill) occurs. Using a first degree equation (y = mx + b) to derive lane lines, even a small curve in the lanes could lead to misinterpretations.

Another potential flaw would be the extraction of a region of interest from the original images using fixed parameters. This could lead to filtering out the lane lines we are trying to detect when the road changes shape.


### 3. Possible improvements for the current pipeline

A possible improvement in detecting curved lane lines could be the use of a higher degree equation to compute lane lines.
But this could lead to poor pipeline performance.
The ultimate goal would be to find the right compromise between precision and performance.

In the case of the region of interest computed using fixed parameters, a possible improvement could be to use variable parameters computed at each step based on the lane line calculated in the previous steps. 
In this way we could detect a change in the shape of the lane lines and adjust the region of interest accordingly.


