# OpenCV keypoints

Find key points in images

## Usage

``` r
ocv_keypoints(
  image,
  method = c("FAST", "Harris"),
  control = ocv_keypoints_options(method, ...),
  ...
)
```

## Arguments

- image:

  an ocv grayscale image object

- method:

  the type of keypoint detection algorithm

- control:

  a list of arguments passed on to the algorithm

- ...:

  further arguments passed on to ocv_keypoints_options

## FAST algorithm arguments

- threshold threshold on difference between intensity of the central
  pixel and pixels of a circle around this pixel.

- nonmaxSuppression if true, non-maximum suppression is applied to
  detected corners (keypoints).

- type one of the three neighborhoods as defined in the paper:
  TYPE_9_16, TYPE_7_12, TYPE_5_8

## Harris algorithm arguments

- numOctaves the number of octaves in the scale-space pyramid

- corn_thresh the threshold for the Harris cornerness measure

- DOG_thresh the threshold for the Difference-of-Gaussians scale
  selection

- maxCorners the maximum number of corners to consider

- num_layers the number of intermediate scales per octave

## Examples

``` r
mona <- ocv_read('https://jeroen.github.io/images/monalisa.jpg')
mona <- ocv_resize(mona, width = 320, height = 477)

# FAST-9
pts <- ocv_keypoints(mona, method = "FAST", type = "TYPE_9_16", threshold = 40)
#> Keypoint detection disabled as module xfeatures2d from opencv_contrib is not present.
# Harris
pts <- ocv_keypoints(mona, method = "Harris", maxCorners = 50)
#> Keypoint detection disabled as module xfeatures2d from opencv_contrib is not present.

# Convex Hull of points
pts <- ocv_chull(pts)
```
