# Detect and Decode a QR code

Detect and decode a QR code from an image or camera. By default it
returns the text value from the QR code if detected, or NULL if no QR
was found. If `draw = TRUE` then it returns an annotated image with the
position and value of the QR drawn into the image, and qr text value as
an attribute. The `qr_scanner` function opens the camera device (if
available on your computer) and repeats ocv_qr_detect until it a QR is
detected.

## Usage

``` r
ocv_qr_detect(image, draw = FALSE, decoder = c("wechat", "quirc"))

qr_scanner(draw = FALSE, decoder = c("wechat", "quirc"))
```

## Arguments

- image:

  an ocv image object created from e.g.
  [`ocv_read()`](https://docs.ropensci.org/opencv/reference/opencv.md)

- draw:

  if TRUE, the function returns an annotated image showing the position
  and value of the QR code.

- decoder:

  which decoder implementation to use, see details.

## Value

if a QR code is detected, this returns either the text value of the QR,
or if `draw` it returns the annotated image, with the value as an
attribute. Returns NULL if no QR was found in the image.

## Details

OpenCV has two separate QR decoders. The 'wechat' decoder was added in
libopencv 4.5.2 and generally has better performance and
fault-tolerance. The old 'quirc' decoder is available on some older
versions of libopencv as a plug-in, but many Linux distros did not
include it. If you get an error *Library QUIRC is not linked. No
decoding is performed.* this sadly means your Linux distribution is too
old and does not support QR decoding.

## Examples

``` r
png("test.png")
plot(qrcode::qr_code("This is a test"))
dev.off()
#> agg_record_6f040ecf26 
#>                     2 
ocv_qr_detect(ocv_read('test.png'))
#> [1] "This is a test"
#> attr(,"points")
#>      [,1] [,2]
#> [1,]    0    0
#> [2,]  479    0
#> [3,]  479  479
#> [4,]    0  479
unlink("test.png")
```
