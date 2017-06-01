# **Finding Lane Lines on the Road**

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. As below

`grayscale`
    \/
`gaussian_blur`
    \/
`canny`
    \/
`region_of_interest`
    \/
`hough_lines`


To draw single line, on left and right lanes. First, all the lines were extrapolated, to span the whole height of the region of interest. This allows for logic in later stages to be much simpler. After extrapolation, all the lines are grouped into sets which have slope within `.01`. Ex, if one line had slope `.08`, and another `.075`, both would belong to the same set.

Once the groups are formed, I find the average line for each group. And then pick one group with -ve slope and one with +ve (the ones having maximum number of lines). There are some other tweaks like, ignoring groups which have x beyond the image region (after extrapolation).

### 2. Identify potential shortcomings with your current pipeline

There are quite a few shortcomings of the current approach. Its quite brittle.
1. Lane marks should be present and visible on the road. Ex, if lanes are blocked by cars in front of you, this might not work.
2. Steep curves (algorithm assumes the lanes to be mostly straight lanes).
3. Since we are looking for bright gradient edges, any other straight lines around the lanes might trip the algorithm.

### 3. Suggest possible improvements to your pipeline

- Doesn't consider the past. Ex, every image is processed afresh, and ignores where the car was, before that state.
- Probably look at more situations, and figure out what different variations are possible. But again, their might be too many, to accommodate.
