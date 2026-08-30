# OpenCV Computer Vision

Tools to experiment with computer vision algorithms. Use ocv_read and
ocv_write to load/save images on disk, or use ocv_picture / ocv_video to
use your webcam. In RSudio IDE the image objects will automatically be
displayed in the viewer pane.

## Usage

``` r
ocv_face(image)

ocv_facemask(image)

ocv_read(path)

ocv_write(image, path)

ocv_destroy(image)

ocv_bitmap(image)

ocv_edges(image)

ocv_picture()

ocv_resize(image, width = 0, height = 0)

ocv_mog2(image)

ocv_knn(image)

ocv_hog(image)

ocv_blur(image, ksize = 5)

ocv_sketch(image, color = TRUE)

ocv_stylize(image)

ocv_markers(image)

ocv_info(image)

ocv_copyto(image, target, mask)

ocv_display(image)

ocv_video(filter, stop_on_result = FALSE)

ocv_grayscale(image)

ocv_version()
```

## Arguments

- image:

  an ocv image object created from e.g. `ocv_read()`

- path:

  image file such as png or jpeg

- width:

  output width in pixels

- height:

  output height in pixels

- ksize:

  size of blurring matrix

- color:

  true or false

- target:

  the output image

- mask:

  only copy pixels from the mask

- filter:

  an R function that takes and returns an opecv image

- stop_on_result:

  stop if an object is detected

## Examples

``` r
# Silly example
mona <- ocv_read('https://jeroen.github.io/images/monalisa.jpg')

# Edge detection
ocv_edges(mona)
#> <pointer: 0x55c73cad9420>
#> attr(,"class")
#> [1] "opencv-image"
ocv_markers(mona)
#> <pointer: 0x55c742015920>
#> attr(,"class")
#> [1] "opencv-image"

# Find face
faces <- ocv_face(mona)

# To show locations of faces
facemask <- ocv_facemask(mona)
attr(facemask, 'faces')
#>   radius   x   y
#> 1    174 582 478

# This is not strictly needed
ocv_destroy(mona)
```
