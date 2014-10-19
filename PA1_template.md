---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---


## Loading and preprocessing the data

```r
df <- read.csv("activity.csv")
```
## What is mean total number of steps taken per day?

```r
hist(df$steps)
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2-1.png) 

```r
mean(df$steps,na.rm=TRUE)
```

```
## [1] 37.3826
```

```r
median(df$steps,na.rm=TRUE)
```

```
## [1] 0
```
## What is the average daily activity pattern?

```r
activity <- aggregate(df[c("steps")],by=df[c("interval")],FUN=mean,na.rm=TRUE)
plot(activity,type="l")
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3-1.png) 
## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
