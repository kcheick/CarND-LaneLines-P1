# **Finding Lane Lines on the Road** 

## Project1 writeup
---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)
[greyscale]: ./writeup_images/grayImage.png
[edges]: ./writeup_images/maskedEdges.png 
[selection]: ./writeup_images/region_selection.png 
[segments]: ./writeup_images/image_segments.png 
[greyscale]: ./writeup_images/grayImage.png
[extendedLines]: ./writeup_images/finalResult.png

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps.

1. Convert the image to greyscale
![alt text][greyscale]
2. Apply a gaussian smoothing 
3. Mask the image with a 4 side polygon that delimit the area of the road
![alt text][selection]
4. Apply the canny transform 
![alt text][edges]
5. Apply the hough transform to detect the coordinates of the detected lines
![alt text][segments]
6. Use the detected lines to draw the lines on the image
![alt text][extendedLines]


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by :
1. First using the slope to separate the segments belonging to the left and the right lines.

2. Average for each sides the values of the each points to approximate the most representative segments

3. Extend the segments to the bottom of the image by finding  the intersection of the line with the bottom of the image.

4. the function draws for each lines the segment from the intersection to the top most coordinate.


### 2. Identify potential shortcomings with your current pipeline

1. It is possible that the parameter for the canny and the haugh transform would not work when the 
lighting condition changes, when driving at night for example
2. The current algorithm does not work well with the curved line. 

### 3. Suggest possible improvements to your pipeline

1. To improve the algorithm we could apply the pipe line with different parameter and choose the first parameters that produce a number of line exceeding a predefined threshold

2. Use the coordinate found during the hough transform to approximate a quadratic curve instead of a line. The draw_line function will have to apply a curve fitting algorithm to find the most representative curve passing through the lines found by the hough transform.
