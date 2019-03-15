``` r
#Load 
library(imager)
#> Warning: package 'imager' was built under R version 3.5.3
#> Loading required package: magrittr
#> 
#> Attaching package: 'imager'
#> The following object is masked from 'package:magrittr':
#> 
#>     add
#> The following objects are masked from 'package:stats':
#> 
#>     convolve, spectrum
#> The following object is masked from 'package:graphics':
#> 
#>     frame
#> The following object is masked from 'package:base':
#> 
#>     save.image


#load images
im <- load.image('./22.jpg')
plot(im)
```

![](https://i.imgur.com/gjrZAaR.png)

``` r


#filter by channels
im0 <- grayscale(im)
im1 <- channel(im,1) #red
im2 <- channel(im,2) #green
im3 <- channel(im,3) #blue


###ROI extraction
library(colocr)

img_rois <- im %>%
  roi_select(threshold = 50, n = 7)
# class of the returned object
class(im); class(img_rois)
#> [1] "cimg"         "imager_array" "numeric"
#> [1] "cimg"         "imager_array" "numeric"

# name of added attribut
names(attributes(im)); names(attributes(img_rois))
#> [1] "class" "dim"
#> [1] "class" "dim"   "label"

# str of labels
label <- attr(img_rois, 'label')
str(label)
#>  num [1:197690] 0 0 0 0 0 0 0 0 0 0 ...

# unique labels 
unique(label)
#> [1] 0 1 2 3 4 5 6 7
# select ROI and show the results
par(mfrow = c(2,2), mar = rep(1, 4))

img_rois %>%
  roi_show()
```

![](https://i.imgur.com/ifg8UGD.png)

``` r
# Separate ROIs and save it to 7 images

im
#> Image. Width: 746 pix Height: 265 pix Depth: 1 Colour channels: 3

#show images
par(mfrow = c(5,1), mar = rep(1,4))

plot(im, axes = FALSE, main = 'Original')
plot(im0, axes = FALSE, main = 'Grayscale')
plot(im1, axes = FALSE, main = 'Red')
plot(im2, axes = FALSE, main = 'Green')
plot(im2, axes = FALSE, main = 'Blue')
```

![](https://i.imgur.com/cgkLODD.png)

<sup>Created on 2019-03-15 by the [reprex package](https://reprex.tidyverse.org) (v0.2.1)</sup>
