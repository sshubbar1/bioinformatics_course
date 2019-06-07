---
title: "RStudio Advanced Bioinformatics 2019 Assessment"
author: '9519'
date: "05/06/2019"
output: 
   html_document:
     keep_md: yes
---



## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:


```r
summary(cars)
```

```
##      speed           dist       
##  Min.   : 4.0   Min.   :  2.00  
##  1st Qu.:12.0   1st Qu.: 26.00  
##  Median :15.0   Median : 36.00  
##  Mean   :15.4   Mean   : 42.98  
##  3rd Qu.:19.0   3rd Qu.: 56.00  
##  Max.   :25.0   Max.   :120.00
```

## Including Plots

You can also embed plots, for example:

![](RStudio_Advanced_Bioinformatics_2019_assessment_files/figure-html/pressure-1.png)<!-- -->

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.


## Task 1

```r
sum(5:55)
```

```
[1] 1530
```


## Task 2

```r
sumfun <- function(n) {sum(5:n)}
sumfun(10)
```

```
[1] 45
```

```r
sumfun(20)
```

```
[1] 200
```

```r
sumfun(100)
```

```
[1] 5040
```


## Task 3

```r
Fibonacci <-numeric(12)
Fibonacci[1] <- Fibonacci[2] <- 1
for(i in 3:12) {Fibonacci[i] <- Fibonacci[i-2] + Fibonacci[i-1]}
print(Fibonacci)
```

```
 [1]   1   1   2   3   5   8  13  21  34  55  89 144
```


## Task 4

```r
library(ggplot2)
data <- mtcars
data$gear <- as.factor(data$gear)
ggplot(mtcars, aes(x = factor(gear), y = mpg, fill=gear)) + geom_boxplot()
```

![](https://github.com/sshubbar1/bioinformatics_course/blob/master/RStudio_Advanced_Bioinformatics_2019_assessment_9519_graph_for_Task_4.png)


## Task 5

```r
distance <- lm(formula = dist ~ speed, data =cars)
summary(distance)
```

```

Call:
lm(formula = dist ~ speed, data = cars)

Residuals:
    Min      1Q  Median      3Q     Max 
-29.069  -9.525  -2.272   9.215  43.201 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept) -17.5791     6.7584  -2.601   0.0123 *  
speed         3.9324     0.4155   9.464 1.49e-12 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 15.38 on 48 degrees of freedom
Multiple R-squared:  0.6511,	Adjusted R-squared:  0.6438 
F-statistic: 89.57 on 1 and 48 DF,  p-value: 1.49e-12
```
Answers for task 5:

Fitted slope is 3.9324

Intercept of the line is -17.5791

Standard deviation for distance is 6.7584 and 

Standard deviation for speed is 0.4155


## Task 6

```r
ggplot(cars, aes(x=speed, y=dist)) + 
geom_point(color='#7F0000', size = 2) + xlim(c(0, 25)) + 
geom_smooth(method=lm, se=FALSE, fullrange=TRUE, color='#2C3E50') + 
labs(title='Linear Relationship between speed and breaking distance', x='Speed (mph)', y='Breaking Distance (ft)')
```

![](https://github.com/sshubbar1/bioinformatics_course/blob/master/unnamed-chunk-6-1.png)


## Task 7

```r
library(ggplot2)
data("cars")
car_speed <- cars$speed + (5280/3600)
lm_l <- lm(dist ~  0 + car_speed + I(car_speed^2), cars)
summary(lm_l) 
```

```

Call:
lm(formula = dist ~ 0 + car_speed + I(car_speed^2), data = cars)

Residuals:
    Min      1Q  Median      3Q     Max 
-28.771  -9.279  -3.151   4.574  45.069 

Coefficients:
               Estimate Std. Error t value Pr(>|t|)    
car_speed       0.78282    0.53790   1.455 0.152084    
I(car_speed^2)  0.09541    0.02651   3.599 0.000754 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 15.02 on 48 degrees of freedom
Multiple R-squared:  0.9133,	Adjusted R-squared:  0.9097 
F-statistic: 252.9 on 2 and 48 DF,  p-value: < 2.2e-16
```

```r
y <- cars$dist
x <- cars$car_speed
ggplot(cars, aes(car_speed, dist)) + geom_point() + geom_smooth(method='lm', formula="y~0+x+I(x^2)") + labs(title = "The average reaction time for driver to start breaking", x="Car Speed in seconds", y="Distance (ft)")
```

![](https://github.com/sshubbar1/bioinformatics_course/blob/master/unnamed-chunk-7-1.png)
The formula: y~0+x+I(x^2) gives a linear graph model but it also provides the line with the best fit of the line (due to the 0 added in the formula).

Answer task 7: According to the results given, the slop of the graph is 0.78282 (car_speed). It is relatively close to 1.0 and is therefore a reasonable time for the driver to start breaking his car.
