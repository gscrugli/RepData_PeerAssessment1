# Reproducible Research: Peer Assessment 1

## Loading and preprocessing the data
The data relevant for this submission is in a standard csv file.

```r
data <- read.csv("activity.csv")
```
The column names in  the data set are: steps, date, interval.

## What is mean total number of steps taken per day?

```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
## 
## The following object is masked from 'package:stats':
## 
##     filter
## 
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
totalperday <- group_by(data,date)
totalperday <- summarize(totalperday,steps=sum(steps))
cleanup <- !is.na(totalperday$steps)
totalperday_clean <- totalperday[cleanup,]
result <- round(mean(totalperday_clean$steps),0)
print(result)
```

```
## [1] 10766
```

## What is the average daily activity pattern?

```r
library(dplyr)
dailypattern <- group_by(data,interval)
dailypattern <- summarize(dailypattern,steps=mean(steps,na.rm=TRUE))
max <- max(dailypattern$steps)
limit <- max+max(dailypattern$steps)/10
plot(dailypattern$interval/100,dailypattern$steps,type="l",ylim=c(0,limit))
```

![](Report_files/figure-html/unnamed-chunk-3-1.png) 

The average maximum number of steps done in a 5 minute intervall is 206.17.

The average maximum number of steps are done between 8:30 and 8:35 

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
