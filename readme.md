More qplot and ggplot examples here: 

http://www.wolf.engineer/the-grammar.html

http://www.wolf.engineer/moreggplot2.html

http://r4ds.had.co.nz/visualize.html



# Examples of qplot(), ggplot(), and pie charts
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
***Notice there is no geom_pie! Pie charts are not recommended in ggplot2.***
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
***Any reference to a variable must be wrapped within a call to the aes() function.***

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

### I() function not needed to edit all points; just put outside the aes() function
```r
ggplot() + geom_point(data = mtcars, aes(x = wt, y = mpg), shape = 17, size = 3)
```
![Rplot31.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot31.png)

### Define data and aesthetics up front when using multiple layers
```r
ggplot(data = mtcars, aes(x = wt, y = mpg)) + 
geom_point(shape = 17, size = 3) + 
geom_smooth(method = "lm", se = FALSE, col = "red")
```
![Rplot32.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot32.png)

### Edit points by variable within call to aes()
```r
ggplot(data = mtcars, aes(x = wt, y = mpg)) + 
geom_point(aes(shape = cyl), size = 3) + 
geom_smooth(method = "lm", se = FALSE, col = "red")
```
![Rplot33.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot33.png)

### Identical plot using qplot()
```r
qplot(data = mtcars, x = wt, y = mpg, shape = cyl, size = I(3)) + 
geom_smooth(method = "lm", se = FALSE, col = "red", aes(shape = NULL))
```
![Rplot34.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot34.png)

### Multiple smoothing lines by variable
```r
qplot(data = mtcars, x = wt, y = mpg, shape = cyl, size = I(3)) + 
geom_smooth(method = "lm", se = FALSE, col = "red", aes(linetype = NULL))
```
OR
```r
ggplot(data = mtcars, aes(x = wt, y = mpg)) + 
geom_point(aes(shape = cyl), size = 3) + 
geom_smooth(method = "lm", se = FALSE, col = "red", aes(shape = cyl))
```
![Rplot35.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot35.png)

## Working with multiple data frames
### "Shadow" plot
```r
## Create a copy of the mtcars data to be used as a "shadow"
library(dplyr) 
carCopy <- mtcars %>% select(-cyl)  ## Select all variables except 'cyl'
## Use layers to control the color of points
ggplot() + 
geom_point(data = carCopy, aes(x = wt, y = mpg), color = "lightgrey") + 
geom_point(data = mtcars, aes(x = wt, y = mpg)) + 
facet_grid( ~ cyl) +   ## Note that 'cyl' only exists in mtcars, not carCopy
ggtitle("MPG vs Weight Automobiles (1973-74 models)\nBy Number of Cylinders") + 
xlab("Weight (lb/1000)") + 
ylab("Miles per US Gallon")
```
![Rplot36.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot36.png)

### Remember this restriction:
***The axes remain on the same scale. It is not possible to use ggplot2 to obtain a plot with two completely different y variables.***

### Coordinate Systems
```r
grep("^coord", objects("package:ggplot2"), value = TRUE)
```
```
[1] "coord_cartesian" "coord_equal"     "coord_fixed"    
[4] "coord_flip"      "coord_map"       "coord_munch"    
[7] "coord_polar"     "coord_quickmap"  "coord_trans"
```
```r
## Extract map coordinates for New Zealand
library(maps)
nz <- map_data("nz") 
str(nz)
```
```
'data.frame':	1552 obs. of  6 variables:
 $ long     : num  173 173 173 173 173 ...
 $ lat      : num  -34.4 -34.5 -34.4 -34.4 -34.4 ...
 $ group    : num  1 1 1 1 1 1 1 1 1 1 ...
 $ order    : int  1 2 3 4 5 6 7 8 9 10 ...
 $ region   : chr  "North.Island " "North.Island " "North.Island " "North.Island " ...
 $ subregion: chr  NA NA NA NA ...
```
```r
## Create plot object
nzmap <- ggplot(nz, aes(x=long, y=lat, group=group)) + 
geom_polygon(fill="white", color="black")

## Now add a projection
library(mapproj)
nzmap + coord_map("cylindrical")
```
![Rplot37.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot37.png)

### A simple pie chart in ggplot2 is not so simple
It's basically a bar chart changed to polar coordinates
```r
mtcars$cyl <- factor(mtcars$cyl) 

basicpie <- ggplot(mtcars, aes(x = factor(1), fill = cyl)) + 
geom_bar(width = 1)

basicpie + coord_polar(theta = "y")
```
![Rplotpie.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplotpie.png)

### A truly simple pie chart
```r
cyl <- table(mtcars$cyl)
pie(cyl, main = "Pie Chart")
```
![Rplotpiechart.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplotpiechart.png)

***Pie charts are not recommended because people are better able to distinguish differences in length than in volume. Histograms and bar charts are better.***

### Rainbow pie chart of 'esoph' dataset with percentages
```r
slices <- table(esoph$agegp)
lbls <- names(slices)
pct <- round(slices/sum(slices)*100)
lbls <- paste(lbls, pct)
lbls <- paste(lbls, "%", sep = "")
pie(slices,labels = lbls, col = rainbow(length(lbls)), 
main = "Pie Chart of Age Groups")
```
![Rplot38.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot38.png)

### 3D Pie using plotrix package
```r
library(plotrix)
pie3D(slices, labels = lbls, explode = 0.1, main = "Age Groups")
```
![Rplot3d.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot3d.png)

### Themes and layouts
```r
grep("^theme", objects("package:ggplot2"), value = TRUE)
```
```
 [1] "theme"          "theme_bw"       "theme_classic" 
 [4] "theme_dark"     "theme_get"      "theme_gray"    
 [7] "theme_grey"     "theme_light"    "theme_linedraw"
[10] "theme_minimal"  "theme_replace"  "theme_set"     
[13] "theme_update"   "theme_void"    
```
```r
grep("^element", objects("package:ggplot2"), value = TRUE)
```
```
[1] "element_blank" "element_grob"  "element_line" 
[4] "element_rect"  "element_text" 
```

### Remove grid lines and tweak panels of individual plot
```r
carPlot + facet_grid(~ cyl) + 
theme(strip.background = element_rect(color = "blue", fill = NA), 
panel.grid.minor = element_blank(), 
panel.grid.major = element_blank(), 
strip.text = element_text(color = "tomato"))
```
![Rplot39.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot39.png)

### Global themes
```r
theme_set(theme_dark(base_size = 18, base_family = "Courier New"))

ggplot(data = mtcars, aes(x = wt, y = mpg)) + 
geom_point(aes(shape = cyl, color = cyl), size = 3) + 
geom_smooth(method = "lm", se = FALSE, aes(color = cyl))
```
![Rplot40.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot40.png)

### More themes in ggthemes package
```r
library(ggthemes)
grep("^theme_", objects("package:ggthemes"), value = TRUE)
```
```
 [1] "theme_base"            "theme_calc"           
 [3] "theme_economist"       "theme_economist_white"
 [5] "theme_excel"           "theme_few"            
 [7] "theme_fivethirtyeight" "theme_foundation"     
 [9] "theme_gdocs"           "theme_hc"             
[11] "theme_igray"           "theme_map"            
[13] "theme_pander"          "theme_par"            
[15] "theme_solarized"       "theme_solarized_2"    
[17] "theme_solid"           "theme_stata"          
[19] "theme_tufte"           "theme_wsj" 
```
```r
theme_set(theme_wsj())
```
![Rplot41.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot41.png)

```r
theme_set(theme_economist())
```
![Rplot42.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot42.png)

```r
theme_set(theme_map())
```
![Rplotmap.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplotmap.png)

```r
theme_set(theme_solarized_2())
```
![Rplotsol.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplotsol.png)

### Edit legends
```r
states <- map_data("state")
mapOfUSA <- qplot(long, lat, data = states, geom = "polygon", 
group = group, fill = region, col = I("black")) 
mapOfUSA <- mapOfUSA + theme(legend.position = "bottom") 
mapOfUSA + guides(fill = guide_legend(title = "State",
nrow =10, title.position = "top"))
```
![Rplot00.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot00.png)

***In order to get an accurate-looking map, we need a "Mercator" projection. See the last example in this file.***

### Remove legend altogether
```r
mapOfUSA + scale_fill_discrete(guide = FALSE) 
```

# Activities
1. Create a histogram of the Wind column from airquality. Use the binwidth argument to adjust the width of the bins.
```r
theme_set(theme_bw(base_size = 14))
qplot(Wind, data = airquality, binwidth = .25)
```
![Rplot43.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot43.png)

2. Create a boxplot of the Wind values for each Month using airquality.
```r
qplot(Month, Wind, data = airquality, group = Month, geom = "boxplot")
```
![Rplot44.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot44.png)

3. Create a plot of Ozone against Wind from airquality. Ensure that the plot has appropriate titles and axis labels. Ensure that the Wind axis begins at zero. Add a linear smoothing line to the plot, removing the error bars.
```r
qplot(Ozone, Wind, data = airquality, na.rm=TRUE) + 
ggtitle("Ozone versus Wind") + xlim(c(0,200)) + ylim(c(0,25)) + 
geom_smooth(method="lm", se = FALSE, na.rm=TRUE)
```
![Rplot45.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot45.png)

4. Create a scatter plot of Height against Weight using demoData. Use a different color to distinquish between males and females and a different plotting symbol dependant on whether the subject smokes or not. 
```r
theme_set(theme_light(base_size = 14, base_family = "Geneva"))
qplot(Height,Weight,data=demoData, shape = Smokes, col = Sex, 
size = I(4)) + scale_shape_manual(values = c(8,16)) + 
scale_color_manual(values = c("plum","steelblue"))
```
![Rplot46.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot46.png)

5. Re-create the basic plot of Height against Weight using demoData. This time, panel/facet the plot to create a 2x2 grid such that the first column contains data for nonsmokers and the first row contains data for females.
```r
qplot(Height,Weight,data=demoData)+facet_grid(Sex ~ Smokes)
```
![Rplot47.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot47.png)

6. Using the maps and mapproj packages, import the state data using map_data("state") and create a plot of the USA, where each state is represented by a different color. Ensure that there is sufficient space for the legend by moving it to the bottom of the plot. Spread the states across 10 columns. Transform the plot in order to view the country with a Mercator projection.
```r
library(maps)
states <- map_data("state")
mapOfUSA <- qplot(long, lat, data = states, 
geom = "polygon", group = group, fill = region, col = I("black"))
mapOfUSA <- mapOfUSA + theme(legend.position = "bottom")
mapOfUSA <- mapOfUSA + guides(fill = guide_legend(title = "State", 
ncol = 10, title.position = "top"))

library(randomcoloR)
mypalette <- distinctColorPalette(49)
mapOfUSA <- mapOfUSA + scale_fill_manual(values=as.character(mypalette))

library(mapproj)
mapOfUSA + coord_map("mercator")
```
![Rplot48.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/plots/Rplot48.png)

***Not sure how to edit legend margins to prevent chopping***
