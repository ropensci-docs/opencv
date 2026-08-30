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
#> <pointer: 0x55c7464f7cb0>
#> attr(,"class")
#> [1] "opencv-image"
ocv_rectangle(mona, x = 0, y = 100, height = 200)
#> <pointer: 0x55c7465d0290>
#> attr(,"class")
#> [1] "opencv-image"
ocv_rectangle(mona, x = 500, y = 0, width = 75)
#> <pointer: 0x55c7465cfdd0>
#> attr(,"class")
#> [1] "opencv-image"

# Polygon area
img <- ocv_resize(mona, width = 320, height = 477)
pts <- list(x = c(184, 172, 146, 114,  90,  76,  92, 163, 258),
            y = c(72,   68,  70,  90, 110, 398, 412, 385, 210))
ocv_polygon(img, pts)
#> <pointer: 0x55c74655c0a0>
#> attr(,"class")
#> [1] "opencv-image"
ocv_polygon(img, pts, crop = TRUE)
#> <pointer: 0x55c73cba4140>
#> attr(,"class")
#> [1] "opencv-image"
ocv_polygon(img, pts, convex = TRUE, crop = TRUE)
#> <pointer: 0x55c746453e10>
#> attr(,"class")
#> [1] "opencv-image"

# Bounding box based on points
ocv_bbox(img, pts)
#> <pointer: 0x55c74650c400>
#> attr(,"class")
#> [1] "opencv-image"

# Bounding box of non-zero pixel area
area <- ocv_polygon(img, pts, color = 0, crop = FALSE)
area
#> <pointer: 0x55c7437c2c90>
#> attr(,"class")
#> [1] "opencv-image"
area <- ocv_bbox(area)
area
#> <pointer: 0x55c7465ace90>
#> attr(,"class")
#> [1] "opencv-image"
```
