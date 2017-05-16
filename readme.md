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

```r
library(ggplot2)
theme_set(theme_bw(base_size = 14))
qplot(x = wt, y = mpg, data = mtcars)
```
![Rplot0.png](https://github.com/emiliehwolf/ggplot2_examples/blob/master/Rplot0.png)
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
```r
basicCarPlot <- qplot(wt, mpg, data = mtcars)
basicCarPlot <- basicCarPlot + ggtitle("Miles per Gallon vs Weight\nAutomobiles (1973-74)")
basicCarPlot
carPlot <- qplot(x = wt, y = mpg, data = mtcars)
setwd("~/Programming/ggplot2_examples")
ggsave(file = "carPlot.png", carPlot)
mtcars$cyl <- factor(mtcars$cyl)
qplot(cyl, mpg, data = mtcars, geom = "boxplot")
grep("^geom", objects("package:ggplot2"), value = TRUE)
qplot(cyl, mpg, data = mtcars) + geom_boxplot()
qplot(wt, mpg, data = mtcars) + geom_smooth(method = "lm")
qplot(wt, mpg, data = mtcars, geom = c("point","smooth"), method = "lm")
str(quakes)
qplot(x = long, y = lat, data = quakes, size = mag, col = -depth) + ggtitle("Locations of Earthquakes off Fiji") + xlab("Longitude") + ylab("Latitude")
qplot(wt, mpg, data = mtcars, color = I("blue"))
qplot(wt, mpg, data = mtcars, color = "blue")
grep("^scale", objects("package:ggplot2"), value = TRUE)
scale_color_gradientn(colors = rainbow(6))
rainbow(6)
carPlot <- qplot(x = wt, y = mpg, data = mtcars, shape = cyl, main = "Miles per Gallon vs Weight\nAutomobiles (1973-74 models)", xlab = "Weight (lb/1000)", ylab = "Miles per US Gallon", xlim = c(1,6), ylim = c(0,40))
carPlot + scale_shape_manual("Number of \nCylinders", values = c(3,5,2))
carPlot <- qplot(x = wt, y = mpg, data = mtcars, shape = cyl, size = disp, main = "Miles per Gallon vs Weight\nAutomobiles (1973-74 models)", xlab = "Weight (lb/1000)", ylab = "Miles per US Gallon", xlim = c(1,6), ylim = c(0,40))
carPlot + scale_shape_discrete("Number of Cylinders") + scale_size_continuous("Displacement (cu.in.)")
carPlot + scale_size_continuous("Displacement (cu.in.)", range = c(4,8))
carPlot + scale_shape_discrete("Number of cylinders") + scale_size_continuous("Displacement (cu.in.)", range = c(4,8), breaks = seq(100, 500, by = 100), limits = c(0,500))
install.packages("mangoTraining")
library(mangoTraining)
head(pkData)
qplot(data = pkData, x = Time, y = Conc, geom = "line")
qplot(data = pkData, x = Time, y = Conc, geom = "path")
qplot(data = pkData, x = Time, y = Conc, geom = "path", group = Subject, ylab = "Concentration")
qplot(data = pkData, x = Time, y = Conc, geom = "path", group = Subject, ylab = "Concentration", col = Subject)
?facet_grid
carPlot + facet_grid(. ~ gear)
carPlot + facet_grid(gear ~ .)
carPlot + facet_grid(cyl ~ gear)
carPlot + facet_grid(. ~ gear + cyl)
carPlot + facet_wrap( ~ carb)
carPlot + facet_wrap( ~ carb + gear)
qplot(wt, mpg, data = mtcars, facets = ~cyl)
savehistory("~/Programming/ggplot2_examples/qplot_practice.Rhistory")
```
