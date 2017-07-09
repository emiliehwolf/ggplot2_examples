# The Grammar

# http://had.co.nz/ggplot2
### This HTML page and its graphics were created using knitr by taking a simple demo R script by Hadley Wickham and adding some R markdown.

```r
library(ggplot2)
```

## qplot examples 

```r
qplot(diamonds$cut, diamonds$carat)
```

![](the-grammar_files/figure-html/unnamed-chunk-2-1.png)<!-- -->


```r
qplot(carat, price, data = diamonds)
```

![](the-grammar_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

```r
qplot(carat, price, data = diamonds, colour=clarity)
```

![](the-grammar_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

```r
qplot(carat, price, data = diamonds, geom=c("point", "smooth"), method=lm)
```

```
## Warning: Ignoring unknown parameters: method
```

![](the-grammar_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

```r
qplot(carat, data = diamonds, geom="histogram")
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](the-grammar_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

```r
qplot(carat, data = diamonds, geom="histogram", binwidth = 1)
```

![](the-grammar_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

```r
qplot(carat, data = diamonds, geom="histogram", binwidth = 0.1)
```

![](the-grammar_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

```r
qplot(carat, data = diamonds, geom="histogram", binwidth = 0.01)
```

![](the-grammar_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

## using ggplot() 

```r
d <- ggplot(diamonds, aes(x=carat, y=price))
```

```r
d + geom_point()
```

![](the-grammar_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

```r
d + geom_point(aes(colour = carat))
```

![](the-grammar_files/figure-html/unnamed-chunk-12-1.png)<!-- -->


```r
ggplot(diamonds) + geom_histogram(aes(x=price))
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](the-grammar_files/figure-html/unnamed-chunk-13-1.png)<!-- -->

## Separation of statistcs and geometric elements

```r
p <- ggplot(diamonds, aes(x=price))
```

```r
p + geom_histogram()
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](the-grammar_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

```r
p + stat_bin(geom="area")
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](the-grammar_files/figure-html/unnamed-chunk-16-1.png)<!-- -->

```r
p + stat_bin(geom="point")
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](the-grammar_files/figure-html/unnamed-chunk-17-1.png)<!-- -->

```r
p + stat_bin(geom="line")
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](the-grammar_files/figure-html/unnamed-chunk-18-1.png)<!-- -->

```r
p + geom_histogram(aes(fill = clarity))
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](the-grammar_files/figure-html/unnamed-chunk-19-1.png)<!-- -->

```r
p + geom_histogram(aes(y = ..density..))
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](the-grammar_files/figure-html/unnamed-chunk-20-1.png)<!-- -->


## Setting vs mapping 

```r
p <- ggplot(diamonds, aes(x=carat,y=price))
```
## What will this do?

```r
p + geom_point(aes(colour = "green"))
```

![](the-grammar_files/figure-html/unnamed-chunk-22-1.png)<!-- -->

```r
p + geom_point(colour = "green")
```

![](the-grammar_files/figure-html/unnamed-chunk-23-1.png)<!-- -->


