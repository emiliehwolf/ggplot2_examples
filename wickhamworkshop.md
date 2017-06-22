# http://had.co.nz/ggplot2
```r
install.packages("ggplot2")
library(ggplot2)
```

## qplot examples 
```r
qplot(diamonds$cut, diamonds$carat)
```

```r
qplot(carat, price, data = diamonds)
```
```r
qplot(carat, price, data = diamonds, colour=clarity)
```
```r
qplot(carat, price, data = diamonds, geom=c("point", "smooth"), method=lm)
```
```r
qplot(carat, data = diamonds, geom="histogram")
```
```r
qplot(carat, data = diamonds, geom="histogram", binwidth = 1)
```
```r
qplot(carat, data = diamonds, geom="histogram", binwidth = 0.1)
```
```r
qplot(carat, data = diamonds, geom="histogram", binwidth = 0.01)
```

## using ggplot() 
```r
d <- ggplot(diamonds, aes(x=carat, y=price))
```
```r
d + geom_point()
```
```r
d + geom_point(aes(colour = carat))
```
```r
d + geom_point(aes(colour = carat)) + scale_colour_brewer()
```
```r
ggplot(diamonds) + geom_histogram(aes(x=price))
```

## Separation of statistcs and geometric elements
```r
p <- ggplot(diamonds, aes(x=price))
```
```r
p + geom_histogram()
```
```r
p + stat_bin(geom="area")
```
```r
p + stat_bin(geom="point")
```
```r
p + stat_bin(geom="line")
```
```r
p + geom_histogram(aes(fill = clarity))
```
```r
p + geom_histogram(aes(y = ..density..))
```


## Setting vs mapping 
```r
p <- ggplot(diamonds, aes(x=carat,y=price))
```
## What will this do?
```r
p + geom_point(aes(colour = "green"))
```
```r
p + geom_point(colour = "green")
```
```r
p + geom_point(colour = colour)
```

