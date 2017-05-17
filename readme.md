# Examples of qplot() and ggplot() 
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
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot0.png)

### Quick plot of vectors
```r
qplot(1:10,rnorm(10))
```
![Rplot1.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot1.png)

### Single call to qplot() with multiple arguments
```r
qplot(x = wt, y = mpg, data = mtcars, 
main = "Miles per Gallon vs Weight\nAutomobiles (1973-74 models)", 
xlab = "Weight (lb/1000)", ylab = "Miles per US Gallon", 
xlim = c(1,6), ylim = c(0,40))
```
![Rplot2.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot2.png)

### Identical quick plot using layers (instead of arguments)
```r
qplot(x = wt, y = mpg, data = mtcars) + 
ggtitle("Miles per Gallon vs Weight\nAutomobiles (1973-74 models)") + 
xlab("Weight (lb/1000)") + ylab("Miles per US Gallon") + 
xlim(c(1,6)) + ylim(c(0,40))
```
![Rplot3.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot3.png)

### Plots as objects
```r
basicCarPlot <- qplot(wt, mpg, data = mtcars)
basicCarPlot <- basicCarPlot + ggtitle("Miles per Gallon vs Weight\nAutomobiles (1973-74)")
basicCarPlot
```
![Rplot4.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot4.png)

### ggsave() (opens and closes graphics device for you)
```r
carPlot <- qplot(x = wt, y = mpg, data = mtcars)
ggsave(file = "carPlot.png", carPlot)
```
![carPlot.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/carPlot.png)

### Boxplot with geom argument
```r
mtcars$cyl <- factor(mtcars$cyl)
qplot(cyl, mpg, data = mtcars, geom = "boxplot")
```
![Rplot5.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot5.png)

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
![Rplot6.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot6.png)

### Scatterplot + linear smoothing line layer
```r
qplot(wt, mpg, data = mtcars) + geom_smooth(method = "lm")
```
![Rplot7.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot7.png)

### Or use geom argument to add linear smoothing line
```r
qplot(wt, mpg, data = mtcars, geom = c("point","smooth"), method = "lm")
```
![Rplot8.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot8.png)

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

### Aesthetics (color, shape, size, alpha, fill, linetype, and x and y axes)
```r
qplot(x = long, y = lat, data = quakes, size = mag, col = -depth) + 
ggtitle("Locations of Earthquakes off Fiji") + xlab("Longitude") + 
ylab("Latitude")
```
![Rplot9.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot9.png)
### Enlarged to show detail
![bigfijiplot.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/bigfijiplot.png)

### Make everything one color with I()
```r
qplot(wt, mpg, data = mtcars, color = I("blue"))
```
![Rplot10.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot10.png)

### Color as a variable (not desired result!)
```r
qplot(wt, mpg, data = mtcars, color = "blue")
```
![Rplot11.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot11.png)

### Use alpha to change transparency to show density
```r
qplot(x = long, y = lat, data = quakes, size = mag, col = -depth, 
alpha = I(.33)) + ggtitle("Locations of Earthquakes off Fiji") + 
xlab("Longitude") + ylab("Latitude") + scale_size_continuous(range = c(1,5))
```
![Rplot28.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot28.png)

### Scaling layers that control aesthetics
```r
grep("^scale", objects("package:ggplot2"), value = TRUE)
```
```
 [1] "scale_alpha"               "scale_alpha_continuous"   
 [3] "scale_alpha_discrete"      "scale_alpha_identity"     
 [5] "scale_alpha_manual"        "scale_color_brewer"       
 [7] "scale_color_continuous"    "scale_color_discrete"     
 [9] "scale_color_distiller"     "scale_color_gradient"     
[11] "scale_color_gradient2"     "scale_color_gradientn"    
[13] "scale_color_grey"          "scale_color_hue"          
[15] "scale_color_identity"      "scale_color_manual"       
[17] "scale_colour_brewer"       "scale_colour_continuous"  
[19] "scale_colour_date"         "scale_colour_datetime"    
[21] "scale_colour_discrete"     "scale_colour_distiller"   
[23] "scale_colour_gradient"     "scale_colour_gradient2"   
[25] "scale_colour_gradientn"    "scale_colour_grey"        
[27] "scale_colour_hue"          "scale_colour_identity"    
[29] "scale_colour_manual"       "scale_fill_brewer"        
[31] "scale_fill_continuous"     "scale_fill_date"          
[33] "scale_fill_datetime"       "scale_fill_discrete"      
[35] "scale_fill_distiller"      "scale_fill_gradient"      
[37] "scale_fill_gradient2"      "scale_fill_gradientn"     
[39] "scale_fill_grey"           "scale_fill_hue"           
[41] "scale_fill_identity"       "scale_fill_manual"        
[43] "scale_linetype"            "scale_linetype_continuous"
[45] "scale_linetype_discrete"   "scale_linetype_identity"  
[47] "scale_linetype_manual"     "scale_radius"             
[49] "scale_shape"               "scale_shape_continuous"   
[51] "scale_shape_discrete"      "scale_shape_identity"     
[53] "scale_shape_manual"        "scale_size"               
[55] "scale_size_area"           "scale_size_continuous"    
[57] "scale_size_date"           "scale_size_datetime"      
[59] "scale_size_discrete"       "scale_size_identity"      
[61] "scale_size_manual"         "scale_x_continuous"       
[63] "scale_x_date"              "scale_x_datetime"         
[65] "scale_x_discrete"          "scale_x_log10"            
[67] "scale_x_reverse"           "scale_x_sqrt"             
[69] "scale_x_time"              "scale_y_continuous"       
[71] "scale_y_date"              "scale_y_datetime"         
[73] "scale_y_discrete"          "scale_y_log10"            
[75] "scale_y_reverse"           "scale_y_sqrt"             
[77] "scale_y_time"             
```

### Add layer to edit shapes manually
```r
carPlot <- qplot(x = wt, y = mpg, data = mtcars, shape = cyl, 
main = "Miles per Gallon vs Weight\nAutomobiles (1973-74 models)", 
xlab = "Weight (lb/1000)", ylab = "Miles per US Gallon", 
xlim = c(1,6), ylim = c(0,40))
carPlot + scale_shape_manual("Number of \nCylinders", values = c(3,5,2))
```
![Rplot12.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot12.png)

### Another example of adding layers to edit legends
```r
carPlot <- qplot(x = wt, y = mpg, data = mtcars, 
shape = cyl, size = disp, 
main = "Miles per Gallon vs Weight\nAutomobiles (1973-74 models)", 
xlab = "Weight (lb/1000)", ylab = "Miles per US Gallon", 
xlim = c(1,6), ylim = c(0,40))

carPlot + scale_shape_discrete("Number of Cylinders") + 
scale_size_continuous("Displacement (cu.in.)")
```
![Rplot13.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot13.png)

### Edit the min and max sizes
```r
carPlot + scale_size_continuous("Displacement (cu.in.)", range = c(4,8))
```
![Rplot14.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot14.png)

### Breaks and limits
```r
carPlot + scale_shape_discrete("Number of cylinders") + 
scale_size_continuous("Displacement (cu.in.)", range = c(4,8), 
breaks = seq(100, 500, by = 100), limits = c(0,500))
```
![Rplot15.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot15.png)

### Tidy data in mangoTraining package with repeating times
```r
install.packages("mangoTraining")
library(mangoTraining)
head(pkData)
```
```
  Subject Dose Time   Conc
1       1   25    0   0.00
2       1   25    1 660.13
3       1   25    6 178.92
4       1   25   12  88.99
5       1   25   24  42.71
6       2   25    0   0.00
```

### Not the desired result!
```r
qplot(data = pkData, x = Time, y = Conc, geom = "line")
```
![Rplot16.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot16.png)

### Not the desired result!
```r
qplot(data = pkData, x = Time, y = Conc, geom = "path")
```
![Rplot17.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot17.png)

### Grouping produces with desired result!
```r
qplot(data = pkData, x = Time, y = Conc, geom = "path", 
group = Subject, ylab = "Concentration")
```
![Rplot18.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot18.png)

### With color 
```r
qplot(data = pkData, x = Time, y = Conc, geom = "path", 
group = Subject, ylab = "Concentration", col = Subject)
```
![Rplot19.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot19.png)

### Rainbow color
```r
qplot(data = pkData, x = Time, y = Conc, geom = "path", 
group = Subject, ylab = "Concentration", col = Subject) + 
scale_color_gradientn(colors = rainbow(16))
```
![Rplot27.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot27.png)

### Faceting (paneling) with 1 row and multiple columns
```r
carPlot + facet_grid(. ~ gear)
```
![Rplot20.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot20.png)

### Faceting with multiple rows and 1 column
```r
carPlot + facet_grid(gear ~ .)
```
![Rplot21.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot21.png)

### Intersection of variables in a 3 x 3 plot
```r
carPlot + facet_grid(cyl ~ gear)
```
![Rplot22.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot22.png)

### Combinations of variables side by side in a 1 x 8 plot (empty panel not displayed)
```r
carPlot + facet_grid(. ~ gear + cyl)
```
![Rplot23.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot23.png)

### facet_wrap() great for many panels
```r
carPlot + facet_wrap( ~ carb)
```
![Rplot24.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot24.png)

### Combination of variables wrapped
```r
carPlot + facet_wrap( ~ carb + gear)
```
![Rplot25.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot25.png)

### Alternative: use facets argument
```r
qplot(wt, mpg, data = mtcars, facets = ~ cyl)
```
![Rplot26.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot26.png)


# Remember this ggplot() rule:
***Any reference to a variable must be wrapped within a call to the aes() function.

### Pass a data frame to ggplot() (look familiar?)
```r
ggplot() + geom_point(data = mtcars, aes(x = wt, y = mpg))
```
![Rplot29.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot29.png)

### Change plotting character/shape
```r
ggplot() + geom_point(data = mtcars, aes(x = wt, y = mpg, shape = cyl))
```
![Rplot30.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot30.png)

### I() function not needed to edit all points; just keep outside the aes() function
```r
ggplot() + geom_point(data = mtcars, aes(x = wt, y = mpg), shape = 17, size = 3)
```
![Rplot31.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot31.png)

