Reproducible Research: Peer Assessment 1
========================================
  
## Loading and preprocessing the data
We're going to load the data and store it in *rawdata* data.frame:

```r
rawdata <- read.csv(unzip("activity.zip"))
```

## What is mean total number of steps taken per day?
For this question we're going to ignore the missing values in the dataset:

```r
data <- na.omit(rawdata)
```

Now, lets see the total number of steps taken each day so we need to aggregate data:

```r
stepsxday <- aggregate(steps ~ date, data, sum)
```

Then print an histogram of the total number of steps taken each day:

```r
hist(stepsxday$steps)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4.png) 

Let's see how about **mean** and **median** of total numbers of steps taken per day:


```r
mean(stepsxday$steps)
```

```
## [1] 10766
```

```r
median(stepsxday$steps)
```

```
## [1] 10765
```

## What is the average daily activity pattern?

First of all, we're going to aggregate data by steps and interval:


```r
stepsxinterval <- aggregate(steps ~ interval, data, mean)
```

Let's see if there's a pattern with a time series plot:


```r
plot(stepsxinterval, type = "l")
```

![plot of chunk unnamed-chunk-7](figure/unnamed-chunk-7.png) 

As you can see, there is a 5-minute interval with maximum value, which is:


```r
maxval <- subset(stepsxinterval, steps == max(stepsxinterval$steps))
maxval$interval
```

```
## [1] 835
```

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?

## BONUS: what is mean total number of steps taken per day (taking NA as 0)?

I reproduce the first question changig NA values as 0. This is done because of some confussing posts in the forum.


```r
data2 <- rawdata
data2[is.na(data2)] <- 0
stepsxday2 <- aggregate(steps ~ date, data2, sum)
hist(stepsxday2$steps)
```

![plot of chunk unnamed-chunk-9](figure/unnamed-chunk-9.png) 

```r
mean(stepsxday2$steps)
```

```
## [1] 9354
```

```r
median(stepsxday2$steps)
```

```
## [1] 10395
```
