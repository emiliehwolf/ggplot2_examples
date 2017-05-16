### Tidy data within R
```r
library(help = "datasets")
str(mtcars)
```
```
'data.frame':	32 obs. of  11 variables:
 $ mpg : num  21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
 $ cyl : num  6 6 4 6 8 6 8 4 4 6 ...
 $ disp: num  160 160 108 258 360 ...
 $ hp  : num  110 110 93 110 175 105 245 62 95 123 ...
 $ drat: num  3.9 3.9 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 ...
 $ wt  : num  2.62 2.88 2.32 3.21 3.44 ...
 $ qsec: num  16.5 17 18.6 19.4 17 ...
 $ vs  : num  0 0 1 1 0 1 0 1 1 1 ...
 $ am  : num  1 1 1 0 0 0 0 0 0 0 ...
 $ gear: num  4 4 4 3 3 3 3 4 4 4 ...
 $ carb: num  4 4 1 1 2 1 4 2 2 4 ...
```
### Pass data frame to qplot()
```r
library(ggplot2)
theme_set(theme_bw(base_size = 14))
qplot(x = wt, y = mpg, data = mtcars)
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

### Quick 'data.frame':	1000 obs. of  5 variables:
 $ lat     : num  -20.4 -20.6 -26 -18 -20.4 ...
 $ long    : num  182 181 184 182 182 ...
 $ depth   : int  562 650 42 626 649 195 82 194 211 622 ...
 $ mag     : num  4.8 4.2 5.4 4.1 4 4 4.8 4.4 4.7 4.3 ...
 $ stations: int  41 15 43 19 11 12 43 15 35 19 ...plot of vectors
```r
qplot(1:10,rnorm(10))
```
![Rplot1.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot1.png)

### Single call to qplot() with multiple arguments
```r
qplot(x = wt, y = mpg, data = mtcars, 
main = "Miles per Gallon vs Weight\nAutomobiles (1973-74 models)", 
xlab = "Weight (lb/1000)", ylab = "Miles per US Gallon", 
xlim = c(1,6), ylim = c(0,40))
```
![Rplot2.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot2.png)

### Identical quick plot with additional layers
```r
qplot(x = wt, y = mpg, data = mtcars) + 
ggtitle("Miles per Gallon vs Weight\nAutomobiles (1973-74 models)") + 
xlab("Weight (lb/1000)") + ylab("Miles per US Gallon") + 
xlim(c(1,6)) + ylim(c(0,40))
```
![Rplot3.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot3.png)

### Plots as objects
```r
basicCarPlot <- qplot(wt, mpg, data = mtcars)
basicCarPlot <- basicCarPlot + ggtitle("Miles per Gallon vs Weight\nAutomobiles (1973-74)")
basicCarPlot
```
![Rplot4.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot4.png)

### ggsave()
```r
carPlot <- qplot(x = wt, y = mpg, data = mtcars)
ggsave(file = "carPlot.png", carPlot)
```
![carPlot.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/carPlot.png)

### Boxplot with geom argument
```r
mtcars$cyl <- factor(mtcars$cyl)
qplot(cyl, mpg, data = mtcars, geom = "boxplot")
```
![Rplot5.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot5.png)

### Plot types
```r
grep("^geom", objects("package:ggplot2"), value = TRUE)
```
```
 [1] "geom_abline"     "geom_area"       "geom_bar"       
 [4] "geom_bin2d"      "geom_blank"      "geom_boxplot"   
 [7] "geom_col"        "geom_contour"    "geom_count"     
[10] "geom_crossbar"   "geom_curve"      "geom_density"   
[13] "geom_density_2d" "geom_density2d"  "geom_dotplot"   
[16] "geom_errorbar"   "geom_errorbarh"  "geom_freqpoly"  
[19] "geom_hex"        "geom_histogram"  "geom_hline"     
[22] "geom_jitter"     "geom_label"      "geom_line"      
[25] "geom_linerange"  "geom_map"        "geom_path"      
[28] "geom_point"      "geom_pointrange" "geom_polygon"   
[31] "geom_qq"         "geom_quantile"   "geom_raster"    
[34] "geom_rect"       "geom_ribbon"     "geom_rug"       
[37] "geom_segment"    "geom_smooth"     "geom_spoke"     
[40] "geom_step"       "geom_text"       "geom_tile"      
[43] "geom_violin"     "geom_vline"
```

### Scatterplot + boxplot (layers overlap)
```r
qplot(cyl, mpg, data = mtcars) + geom_boxplot()
```
![Rplot6.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot6.png)

### Scatterplot + linear smoothing line
```r
qplot(wt, mpg, data = mtcars) + geom_smooth(method = "lm")
```
![Rplot7.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot7.png)

### Use geom argument to add linear smoothing line
```r
qplot(wt, mpg, data = mtcars, geom = c("point","smooth"), method = "lm")
```
![Rplot8.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot8.png)

### Tidy data within R
```r
str(quakes)
```
```
'data.frame':	1000 obs. of  5 variables:
 $ lat     : num  -20.4 -20.6 -26 -18 -20.4 ...
 $ long    : num  182 181 184 182 182 ...
 $ depth   : int  562 650 42 626 649 195 82 194 211 622 ...
 $ mag     : num  4.8 4.2 5.4 4.1 4 4 4.8 4.4 4.7 4.3 ...
 $ stations: int  41 15 43 19 11 12 43 15 35 19 ...
```

### Aesthetics
```r
qplot(x = long, y = lat, data = quakes, size = mag, col = -depth) + 
ggtitle("Locations of Earthquakes off Fiji") + xlab("Longitude") + 
ylab("Latitude")
```
![Rplot9.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot9.png)
### Enlarged to show detail
![bigfijiplot.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/bigfijiplot.png)

### Make everything one color with I()
```r
qplot(wt, mpg, data = mtcars, color = I("blue"))
```
![Rplot10.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot10.png)

### Color as a variable (undesired)
```r
qplot(wt, mpg, data = mtcars, color = "blue")
```
![Rplot11.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot11.png)

###
```r
grep("^scale", objects("package:ggplot2"), value = TRUE)
```


###
```r
scale_color_gradientn(colors = rainbow(6))
rainbow(6)
```


###
```r
carPlot <- qplot(x = wt, y = mpg, data = mtcars, shape = cyl, main = "Miles per Gallon vs Weight\nAutomobiles (1973-74 models)", xlab = "Weight (lb/1000)", ylab = "Miles per US Gallon", xlim = c(1,6), ylim = c(0,40))
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

###
```r
carPlot + scale_shape_manual("Number of \nCylinders", values = c(3,5,2))
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

###
```r
carPlot <- qplot(x = wt, y = mpg, data = mtcars, shape = cyl, size = disp, main = "Miles per Gallon vs Weight\nAutomobiles (1973-74 models)", xlab = "Weight (lb/1000)", ylab = "Miles per US Gallon", xlim = c(1,6), ylim = c(0,40))
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

###
```r
carPlot + scale_shape_discrete("Number of Cylinders") + scale_size_continuous("Displacement (cu.in.)")
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

###
```r
carPlot + scale_size_continuous("Displacement (cu.in.)", range = c(4,8))
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

###
```r
carPlot + scale_shape_discrete("Number of cylinders") + scale_size_continuous("Displacement (cu.in.)", range = c(4,8), breaks = seq(100, 500, by = 100), limits = c(0,500))
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

###
```r
install.packages("mangoTraining")
library(mangoTraining)
head(pkData)
qplot(data = pkData, x = Time, y = Conc, geom = "line")
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

###
```r
qplot(data = pkData, x = Time, y = Conc, geom = "path")
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

###
```r
qplot(data = pkData, x = Time, y = Conc, geom = "path", group = Subject, ylab = "Concentration")
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

###
```r
qplot(data = pkData, x = Time, y = Conc, geom = "path", group = Subject, ylab = "Concentration", col = Subject)
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

###
```r
?facet_grid
carPlot + facet_grid(. ~ gear)
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

###
```r
carPlot + facet_grid(gear ~ .)
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

###
```r
carPlot + facet_grid(cyl ~ gear)
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

###
```r
carPlot + facet_grid(. ~ gear + cyl)
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

###
```r
carPlot + facet_wrap( ~ carb)
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

###
```r
carPlot + facet_wrap( ~ carb + gear)
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)

###
```r
qplot(wt, mpg, data = mtcars, facets = ~cyl)
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)
