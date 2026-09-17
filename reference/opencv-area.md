# OpenCV area manipulation

Manipulate image regions

## Usage

``` r
ocv_rectangle(image, x = 0L, y = 0L, width, height)

ocv_polygon(image, pts, convex = FALSE, crop = FALSE, color = 255)

ocv_bbox(image, pts)

ocv_chull(pts)
```

## Arguments

- image:

  an ocv image object

- x:

  horizontal location

- y:

  vertical location

- width:

  width of the area

- height:

  height of the area

- pts:

  a list of points with elements x and y

- convex:

  are the points convex

- crop:

  crop the resulting area to its bounding box

- color:

  color for the non-polygon area

## Examples

``` r
mona <- ocv_read('https://jeroen.github.io/images/monalisa.jpg')

# Rectangular area
ocv_rectangle(mona, x = 400, y = 300, height = 300, width = 350)
#> <pointer: 0x55d292c395a0>
#> attr(,"class")
#> [1] "opencv-image"
ocv_rectangle(mona, x = 0, y = 100, height = 200)
#> <pointer: 0x55d2966223a0>
#> attr(,"class")
#> [1] "opencv-image"
ocv_rectangle(mona, x = 500, y = 0, width = 75)
#> <pointer: 0x55d292c4c510>
#> attr(,"class")
#> [1] "opencv-image"

# Polygon area
img <- ocv_resize(mona, width = 320, height = 477)
pts <- list(x = c(184, 172, 146, 114,  90,  76,  92, 163, 258),
            y = c(72,   68,  70,  90, 110, 398, 412, 385, 210))
ocv_polygon(img, pts)
#> <pointer: 0x55d28ff67370>
#> attr(,"class")
#> [1] "opencv-image"
ocv_polygon(img, pts, crop = TRUE)
#> <pointer: 0x55d295c0d130>
#> attr(,"class")
#> [1] "opencv-image"
ocv_polygon(img, pts, convex = TRUE, crop = TRUE)
#> <pointer: 0x55d28f20e830>
#> attr(,"class")
#> [1] "opencv-image"

# Bounding box based on points
ocv_bbox(img, pts)
#> <pointer: 0x55d292c4c680>
#> attr(,"class")
#> [1] "opencv-image"

# Bounding box of non-zero pixel area
area <- ocv_polygon(img, pts, color = 0, crop = FALSE)
area
#> <pointer: 0x55d28f23a0d0>
#> attr(,"class")
#> [1] "opencv-image"
area <- ocv_bbox(area)
area
#> <pointer: 0x55d291b11f90>
#> attr(,"class")
#> [1] "opencv-image"
```
