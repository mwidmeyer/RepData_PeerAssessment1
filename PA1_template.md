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

```r
activity[activity$steps==max(activity$steps),"interval"]
```

```
## [1] 835
```
## Imputing missing values

```r
length(which(is.na(df$steps)))
```

```
## [1] 2304
```

```r
df2 <- df
df2$steps <- ifelse(is.na(df2$steps),activity$steps[match(df2$interval, activity$interval)], df2$steps)
hist(df2$steps)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4-1.png) 

```r
mean(df2$steps)
```

```
## [1] 37.3826
```

```r
median(df2$steps)
```

```
## [1] 0
```
## Are there differences in activity patterns between weekdays and weekends?

```r
df2$wd <- as.factor(ifelse(weekdays(as.Date(df2$date)) %in% c("Saturday","Sunday"), "Weekend", "Weekday"))
plot(df2[df2$wd=="Weekend",c("interval","steps")],type="l")
title("Weekend")
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5-1.png) 

```r
plot(df2[df2$wd=="Weekday",c("interval","steps")],type="l")
title("Weekday")
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5-2.png) 
