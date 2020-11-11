Data Visualization
================
Brady Puckett
8/21/2020

# Data Visualization

### 3.1 Introduction

``` r
# we must load the tidyverse library every session
library(tidyverse) 
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.3     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.1     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

### 3.2 First Steps

question: Do cars with big engines use more gas than cars with small
engines?

##### 3.2.1 The mpg data frame

A data frame is a rectangular collection of variables (in the columns)
and observations (in the rows). mpg contains observations collected by
the US Environmental Protection Agency on 38 models of car.

``` r
mpg
```

    ## # A tibble: 234 x 11
    ##    manufacturer model    displ  year   cyl trans   drv     cty   hwy fl    class
    ##    <chr>        <chr>    <dbl> <int> <int> <chr>   <chr> <int> <int> <chr> <chr>
    ##  1 audi         a4         1.8  1999     4 auto(l… f        18    29 p     comp…
    ##  2 audi         a4         1.8  1999     4 manual… f        21    29 p     comp…
    ##  3 audi         a4         2    2008     4 manual… f        20    31 p     comp…
    ##  4 audi         a4         2    2008     4 auto(a… f        21    30 p     comp…
    ##  5 audi         a4         2.8  1999     6 auto(l… f        16    26 p     comp…
    ##  6 audi         a4         2.8  1999     6 manual… f        18    26 p     comp…
    ##  7 audi         a4         3.1  2008     6 auto(a… f        18    27 p     comp…
    ##  8 audi         a4 quat…   1.8  1999     4 manual… 4        18    26 p     comp…
    ##  9 audi         a4 quat…   1.8  1999     4 auto(l… 4        16    25 p     comp…
    ## 10 audi         a4 quat…   2    2008     4 manual… 4        20    28 p     comp…
    ## # … with 224 more rows

##### 3.2.2 Creating a ggplot

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

##### Exercises

> 1.  Run ggplot(data = mpg). What do you see?

``` r
ggplot(data = mpg) 
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
# I see a blank placeholder 
```

> 2.  How many rows are in mpg? How many columns?

``` r
# 234 rows
# 11 columns 
```

> 3.  What does the drv variable describe? Read the help for ?mpg to
>     find out.

``` r
# drv= drivetrain 
### Front-wheel drive? rear-wheel drive? 4-wheel drive? 
```

> 4.  Make a scatterplot of hwy vs cyl.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = hwy, y = cyl))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

> 5.  What happens if you make a scatterplot of class vs drv? Why is the
>     plot not useful?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = class, y = drv))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

### 3.3 Aesthetic mappings

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = class))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, size = class))
```

    ## Warning: Using size for a discrete variable is not advised.

![](Data-Visualization_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, alpha = class))
```

    ## Warning: Using alpha for a discrete variable is not advised.

![](Data-Visualization_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, shape = class))
```

    ## Warning: The shape palette can deal with a maximum of 6 discrete values because
    ## more than 6 becomes difficult to discriminate; you have 7. Consider
    ## specifying shapes manually if you must have them.

    ## Warning: Removed 62 rows containing missing values (geom_point).

![](Data-Visualization_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy), color = "blue")
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

##### 3.3.1 Exercises

> 1.  What’s gone wrong with this code? Why are the points not blue?

ggplot(data = mpg) + geom\_point(mapping = aes(x = displ, y = hwy, color
= “blue”))

``` r
### The points aren't blue because there is no "blue" variable within the graph 
```

> 2.  Which variables in mpg are categorical? Which variables are
>     continuous? (Hint: type ?mpg to read the documentation for the
>     dataset). How can you see this information when you run mpg?

``` r
### categorical: manufacturer, model, trans, drv, class, fl
### continuous: year, city, hwy, displacement, cyl, 
```

> 3.  Map a continuous variable to color, size, and shape. How do these
>     aesthetics behave differently for categorical vs. continuous
>     variables?

``` r
### ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = cty))
```

``` r
### ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, size = cty))
```

``` r
### ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, shape = cty))
```

> 4.  What happens if you map the same variable to multiple aesthetics?

REDUNDANT

``` r
### ### ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, colow = hwy))
```

> 5.  What does the stroke aesthetic do? What shapes does it work with?
>     (Hint: use ?geom\_point)

> 6.  What happens if you map an aesthetic to something other than a
>     variable name, like aes(colour = displ \< 5)? Note, you’ll also
>     need to specify x and y.

``` r
### ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = displ < 5))
```

### 3.5 Faucets

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_wrap(~ class, nrow = 2)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_grid(drv ~ cyl)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

##### 3.5.1 Exercises

> 1.  What happens if you facet on a continuous variable?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_wrap(~ cty, nrow = 1) 
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

``` r
### The numbers on the x-axis are very close together. This is also the opposite of what the original graph is.  
```

> 2.  What do the empty cells in plot with facet\_grid(drv \~ cyl) mean?
>     How do they relate to this plot?

``` r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = drv, y = cyl))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-25-1.png)<!-- -->

``` r
### because those are categorical,a graph can be made. 
### The empty cells represent areas which no data fits in the given range 
```

> 3.  What plots does the following code make? What does . do?

``` r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(drv ~ .)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->

``` r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(. ~ cyl)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-26-2.png)<!-- -->

``` r
### . creates separate graphs with different displacements per cylinder 
```

> 4.  Take the first faceted plot in this section: What are the
>     advantages to using faceting instead of the colour aesthetic? What
>     are the disadvantages? How might the balance change if you had a
>     larger dataset?

``` r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_wrap(~ class, nrow = 2)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-27-1.png)<!-- -->

``` r
### Advantages: we are able to see how the hwy mpg differs from each type of car (class)
### Disadvantages: We are not able to compare the points to others from different classes and all the points are bunched up. Having different colors helps with the visualization of the viewer. Colors allow the viwer to see the trend much easier
```

> 5.  Read ?facet\_wrap. What does nrow do? What does ncol do? What
>     other options control the layout of the individual panels? Why
>     doesn’t facet\_grid() have nrow and ncol arguments?

``` r
### nrow and ncol allow the coder to determine the number of columns and rows included within a faucet set. 
### Faucet_grid doesn't have nrow or ncol because the number of unique values of the variables specified in the function determines the number of rows and columns.
### Faucet_wrap has nrow and ncol arguments because it only facets on one variable; therefore, its necessary for nrow and ncol to be inserted
```

> 6.  When using facet\_grid() you should usually put the variable with
>     more unique levels in the columns. Why?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_grid(cty ~ cyl)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-29-1.png)<!-- -->

### 3.6 Geometric Objects

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ, y = hwy))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-30-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ, y = hwy, linetype = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-31-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ, y = hwy, group = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-32-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ, y = hwy, color = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-33-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + geom_smooth(mapping = aes(x = displ, y = hwy))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-34-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = drv)) + geom_smooth(mapping = aes(x = displ, y = hwy, color = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-35-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + geom_point() + geom_smooth()
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-36-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + geom_smooth() + geom_point(mapping = aes(color = class))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-37-1.png)<!-- -->

##### 3.6.1 Exercizes

> 1.  What geom would you use to draw a line chart? A boxplot? A
>     histogram? An area chart?

``` r
### geom_smooth; geom_boxplot; geom_histogram; geom_area 
```

> 2.  Run this code in your head and predict what the output will look
>     like. Then, run the code in R and check your predictions.

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
  geom_point() + 
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-39-1.png)<!-- -->

> 3.  What does show.legend = FALSE do? What happens if you remove it?
>     Why do you think I used it earlier in the chapter?

``` r
### show.legend = FALSE --> makes the scale not have any legend for the aesthetic 
```

> 4.  What does the se argument to geom\_smooth() do?

``` r
### It adds standard error bands to the lines.
```

> 5.  Will these two graphs look different? Why/why not?

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point() + 
  geom_smooth()
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-42-1.png)<!-- -->

``` r
ggplot() + 
  geom_point(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-42-2.png)<!-- -->

``` r
### These graphs will looks the same because the "mapping = aes" is included for everything included behind the ggplot
```

### 3.7 Statistical transformations

``` r
diamonds
```

    ## # A tibble: 53,940 x 10
    ##    carat cut       color clarity depth table price     x     y     z
    ##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ##  1 0.23  Ideal     E     SI2      61.5    55   326  3.95  3.98  2.43
    ##  2 0.21  Premium   E     SI1      59.8    61   326  3.89  3.84  2.31
    ##  3 0.23  Good      E     VS1      56.9    65   327  4.05  4.07  2.31
    ##  4 0.290 Premium   I     VS2      62.4    58   334  4.2   4.23  2.63
    ##  5 0.31  Good      J     SI2      63.3    58   335  4.34  4.35  2.75
    ##  6 0.24  Very Good J     VVS2     62.8    57   336  3.94  3.96  2.48
    ##  7 0.24  Very Good I     VVS1     62.3    57   336  3.95  3.98  2.47
    ##  8 0.26  Very Good H     SI1      61.9    55   337  4.07  4.11  2.53
    ##  9 0.22  Fair      E     VS2      65.1    61   337  3.87  3.78  2.49
    ## 10 0.23  Very Good H     VS1      59.4    61   338  4     4.05  2.39
    ## # … with 53,930 more rows

``` r
ggplot(data = diamonds) + geom_bar(mapping = aes(x = cut))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-44-1.png)<!-- -->

### 3.8 position adjustments

``` r
ggplot(data = diamonds) + geom_bar(mapping = aes(x = cut, color = cut))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-45-1.png)<!-- -->

``` r
ggplot(data = diamonds) + geom_bar(mapping = aes(x = cut, fill = cut))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-46-1.png)<!-- -->

``` r
ggplot(data = diamonds) + geom_bar(mapping = aes(x = cut, fill = clarity))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-47-1.png)<!-- -->

``` r
ggplot(data = diamonds, mapping = aes(x = cut, fill = clarity)) + geom_bar(alpha = 0.2, position = "identity")
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-48-1.png)<!-- -->

``` r
ggplot(data = diamonds, mapping = aes(x = cut, fill = clarity)) + geom_bar(position = "fill")
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-49-1.png)<!-- -->

``` r
ggplot(data = diamonds, mapping = aes(x = cut, fill = clarity)) + geom_bar(position = "dodge")
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-50-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + geom_point()
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-51-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + geom_point(position = "jitter")
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-52-1.png)<!-- -->

##### 3.8.1 Exercises

> 1.  What is the problem with this plot? How could you improve it?

``` r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + geom_point()
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-53-1.png)<!-- -->

``` r
### the problem is that it's comaparing hwy to cty. This is only showing the cars hwy and cty, but it doesn't show any diplacemnt or type of car
```

> 2.  What parameters to geom\_jitter() control the amount of jittering?

``` r
### arguments: stat, position, width, and heigh
### amount of vertical and hortizontal jitter in the positive and negative direction 
```

> 3.  Compare and contrast geom\_jitter() with geom\_count().

``` r
?geom_jitter
?geom_count
### the count is what the original function made (put them together), but the jitter moved the points 
```

> 4.  What’s the default position adjustment for geom\_boxplot()? Create
>     a visualisation of the mpg dataset that demonstrates it.

``` r
?geom_boxplot
### the default position is "dodge2"
```
