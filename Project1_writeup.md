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

1. convert the image to greyscale
![alt text][greyscale]
2. apply a gaussian smotthing 
3. mask the image with a 4 side poligon that deleimit the area of the road
![alt text][selection]
4. apply the canny transform 
![alt text][edges]
5. apply the hough transform to detect the coodinates of the detected lines
![alt text][segments]
6. use the detected lines to draw the lines on the image
![alt text][extendedLines]


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by :
1. first using the slope to separated the segment belonging to the left and the right.
2. average the values of the each points to approximate the most representative segment
3. extend the segement to the bottom of the image by using the slope of the most representative segment to solve the coordinate of the  intersection of the line with the bottom of the image.

4. the function draws for each lines the segment from the intersection to the top most coordinate.


### 2. Identify potential shortcomings with your current pipeline

1. It is possible that the paramter for the canny and the haugh tranform would not work when the 
ligthing condition changes, when driving at night for exemple
2. The current algorithm does not work well with the curved line. 

### 3. Suggest possible improvements to your pipeline

1. To improve the algorithm we could apply the pipe line with different paramter and choose the first paramters that produce a number of line exceeding a predefine threshold

2. Use the coordinate found during the hough tranform to approximate a quadratic curve instead of a line. The draw_line function will have to apply a curve fitting alogorithm to find the most representative curve apssing through the lines found by the hough transform.
