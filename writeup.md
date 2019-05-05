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

My pipeline consisted of 3 steps. i.e., 

- Hightlight edges (`highlight_edges`). That applies **grascale**, **gaussian blur** with 5x5 kernel and **canny edge detection** with 75 low & 150 high threshold. As a result, I achieved (relatively) noiseless image with black background and white foreground as foreground being the shape edges in the image.
- Remove environment noise (`remove_environment_noise`). Based on lane lines on a straight road will start appearing from the sides of the image and converge to one point at horizontal line, we **mask** out all the **edges detected outside the triangular(ish) shape**. As a result, we are left with only lane data. I am not confident that this solution would work on turns.
- Highlight lanes (`highlight_lanes`). That runs **hough line detection** with rho=1, theta=(PI/180), threshold=75, min_line_len=10, max_line_gap=30. That gives me a nice collection of outlines for the lanes
- Draw lines on top of original image (`weighted_img`). Draws a single line per lane by connecting extreme edges of detected line coordinates for left and right lane. In this method, I use slope of the line to determine where it stands (left or right)

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by grouping line coordinates per line slope and drawing a single line using both extremes of those coordinate groups 

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when car comes across a road rotating towards left or right

Another shortcoming could be having a obstacle in beween the lines. Current algorithm group lines per slope and that obstacle would introduce noise and potentially misdrawn lane.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ???

Another potential improvement could be to ???
