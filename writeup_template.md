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

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps:
1. Convert the images to grayscale
<div align="center">
    <img src="https://github.com/Ventu012/P1_FindingLaneLines/blob/main/test_images_output/solidWhiteCurve_gray.jpg" width="500" />
</div>

2. Apply Gaussuan Blur to smooth the images
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

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:
1. computing the slope and intercept for each line
2. dividing the lines into two groups: lines with positive slope and lines with negative slope
3. computing the average slope and intercept for each of the two group of lines
4. using the avg slope and intercept computed in the previous step reconstruct the two lines


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the road is not straight but turns to the left or the right, or even during a change in the slope of the road (uphill/downhill). Using a first grade equation (y=mx+b) to derive the lane lines, even a small curve in the lanes could lead to missinterpretaions.

Another potential shortcoming would be extracting a region of interest from original images using fixed parameters. This could lead to filter out the lane lines that we are trying to detect when the road changes its shape. 


### 3. Suggest possible improvements to your pipeline

A possible improvement to the detection of curve lane lines could be to use an higher grade equation to derive the lane lines. 
But this could lead to worsen the performance of the pipeline. The final goal would be to find the right tradeoff between accuracy and performance.

In the case of the fixed parameter a possible improvement could be to use 
