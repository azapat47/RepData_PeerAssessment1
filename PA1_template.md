---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---



## Loading and preprocessing the data


```r
unzip('activity.zip')
data <- read.csv('activity.csv')
```


## What is mean total number of steps taken per day?



1. Make a histogram of the total number of steps taken each day


```r
steps <- tapply(data$steps, data$date, FUN=sum, na.rm=TRUE)
qplot(steps, binwidth=1000, xlab="N° Steps per day")
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

2. Calculate and report the mean and median total number of steps taken per day


```r
mean(steps, na.rm=TRUE)
```

```
## [1] 9354.23
```

```r
median(steps, na.rm=TRUE)
```

```
## [1] 10395
```

## What is the average daily activity pattern?

1. Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)


```r
averages <- aggregate(x=list(meanSteps=data$steps), by=list(interval=data$interval),FUN=mean, na.rm=TRUE)
ggplot(data=averages , aes(x=interval, y=meanSteps)) + geom_line() + xlab("5-minutes interval") + ylab("Avg n° steps")
```

![](PA1_template_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

2. Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?


```r
averages[which.max(averages$meanSteps),]
```

```
##     interval meanSteps
## 104      835  206.1698
```

## Imputing missing values

1. Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)


```r
numberNA <- length(which(is.na(data$steps)))
```

* There are 2304 missing values.



4. Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?


```r
qplot(stepsCleaned, xlab='Steps per day', ylab='Frecuency', binwidth=500)
```

![](PA1_template_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

## Are there differences in activity patterns between weekdays and weekends?

![](PA1_template_files/figure-html/unnamed-chunk-10-1.png)<!-- -->
