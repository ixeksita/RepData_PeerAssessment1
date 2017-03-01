Author: Tania Sanchez Monroy

Data acquisition and pre-processing
-----------------------------------

The first step is to load the data. This was obtained from [the course
website](https://www.coursera.org/learn/reproducible-research/peer/gYyPt/course-project-1)

    # loading the data 
    activity <- read.csv(unz("repdat-data-activity.zip", "activity.csv"), header=T, quote="\"", sep=",")

Dropping NA's and ensuring the dates are datetime class

    #saving a copy of the raw data 
    data_raw <- activity
    data_raw$Dates <- as.Date(data_raw$date, "%Y-%m-%d")
    # dropping NA
    activity <- drop_na(activity)

    # dates as date time class
    activity$Dates <- as.Date(activity$date, "%Y-%m-%d")

What is mean total number of steps taken per day?
-------------------------------------------------

1.  Calculating the total number of steps per day
2.  Plotting the obtained number of steps

<!-- -->

    # getting the total number of steps per day
    steps_day <- summarise(group_by(activity, Dates), total_steps= sum(steps))

    #plotting the data 
    p<-ggplot(data= steps_day, aes(x=Dates, y=total_steps))
    p + geom_bar(width = 1.0, stat ='identity', colour='#68228B', fill='#E6E6FA') +
      xlab('')+ylab('Total number of steps per day') + 
      ggtitle("Total number of steps taken each day") +
      theme(plot.title = element_text(hjust =0.5))

![](Figures/unnamed-chunk-4-1.png) The total number of steps per day
are:

    kable(steps_day[,], caption ='Total steps per date')

<table>
<caption>Total steps per date</caption>
<thead>
<tr class="header">
<th align="left">Dates</th>
<th align="right">total_steps</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">2012-10-02</td>
<td align="right">126</td>
</tr>
<tr class="even">
<td align="left">2012-10-03</td>
<td align="right">11352</td>
</tr>
<tr class="odd">
<td align="left">2012-10-04</td>
<td align="right">12116</td>
</tr>
<tr class="even">
<td align="left">2012-10-05</td>
<td align="right">13294</td>
</tr>
<tr class="odd">
<td align="left">2012-10-06</td>
<td align="right">15420</td>
</tr>
<tr class="even">
<td align="left">2012-10-07</td>
<td align="right">11015</td>
</tr>
<tr class="odd">
<td align="left">2012-10-09</td>
<td align="right">12811</td>
</tr>
<tr class="even">
<td align="left">2012-10-10</td>
<td align="right">9900</td>
</tr>
<tr class="odd">
<td align="left">2012-10-11</td>
<td align="right">10304</td>
</tr>
<tr class="even">
<td align="left">2012-10-12</td>
<td align="right">17382</td>
</tr>
<tr class="odd">
<td align="left">2012-10-13</td>
<td align="right">12426</td>
</tr>
<tr class="even">
<td align="left">2012-10-14</td>
<td align="right">15098</td>
</tr>
<tr class="odd">
<td align="left">2012-10-15</td>
<td align="right">10139</td>
</tr>
<tr class="even">
<td align="left">2012-10-16</td>
<td align="right">15084</td>
</tr>
<tr class="odd">
<td align="left">2012-10-17</td>
<td align="right">13452</td>
</tr>
<tr class="even">
<td align="left">2012-10-18</td>
<td align="right">10056</td>
</tr>
<tr class="odd">
<td align="left">2012-10-19</td>
<td align="right">11829</td>
</tr>
<tr class="even">
<td align="left">2012-10-20</td>
<td align="right">10395</td>
</tr>
<tr class="odd">
<td align="left">2012-10-21</td>
<td align="right">8821</td>
</tr>
<tr class="even">
<td align="left">2012-10-22</td>
<td align="right">13460</td>
</tr>
<tr class="odd">
<td align="left">2012-10-23</td>
<td align="right">8918</td>
</tr>
<tr class="even">
<td align="left">2012-10-24</td>
<td align="right">8355</td>
</tr>
<tr class="odd">
<td align="left">2012-10-25</td>
<td align="right">2492</td>
</tr>
<tr class="even">
<td align="left">2012-10-26</td>
<td align="right">6778</td>
</tr>
<tr class="odd">
<td align="left">2012-10-27</td>
<td align="right">10119</td>
</tr>
<tr class="even">
<td align="left">2012-10-28</td>
<td align="right">11458</td>
</tr>
<tr class="odd">
<td align="left">2012-10-29</td>
<td align="right">5018</td>
</tr>
<tr class="even">
<td align="left">2012-10-30</td>
<td align="right">9819</td>
</tr>
<tr class="odd">
<td align="left">2012-10-31</td>
<td align="right">15414</td>
</tr>
<tr class="even">
<td align="left">2012-11-02</td>
<td align="right">10600</td>
</tr>
<tr class="odd">
<td align="left">2012-11-03</td>
<td align="right">10571</td>
</tr>
<tr class="even">
<td align="left">2012-11-05</td>
<td align="right">10439</td>
</tr>
<tr class="odd">
<td align="left">2012-11-06</td>
<td align="right">8334</td>
</tr>
<tr class="even">
<td align="left">2012-11-07</td>
<td align="right">12883</td>
</tr>
<tr class="odd">
<td align="left">2012-11-08</td>
<td align="right">3219</td>
</tr>
<tr class="even">
<td align="left">2012-11-11</td>
<td align="right">12608</td>
</tr>
<tr class="odd">
<td align="left">2012-11-12</td>
<td align="right">10765</td>
</tr>
<tr class="even">
<td align="left">2012-11-13</td>
<td align="right">7336</td>
</tr>
<tr class="odd">
<td align="left">2012-11-15</td>
<td align="right">41</td>
</tr>
<tr class="even">
<td align="left">2012-11-16</td>
<td align="right">5441</td>
</tr>
<tr class="odd">
<td align="left">2012-11-17</td>
<td align="right">14339</td>
</tr>
<tr class="even">
<td align="left">2012-11-18</td>
<td align="right">15110</td>
</tr>
<tr class="odd">
<td align="left">2012-11-19</td>
<td align="right">8841</td>
</tr>
<tr class="even">
<td align="left">2012-11-20</td>
<td align="right">4472</td>
</tr>
<tr class="odd">
<td align="left">2012-11-21</td>
<td align="right">12787</td>
</tr>
<tr class="even">
<td align="left">2012-11-22</td>
<td align="right">20427</td>
</tr>
<tr class="odd">
<td align="left">2012-11-23</td>
<td align="right">21194</td>
</tr>
<tr class="even">
<td align="left">2012-11-24</td>
<td align="right">14478</td>
</tr>
<tr class="odd">
<td align="left">2012-11-25</td>
<td align="right">11834</td>
</tr>
<tr class="even">
<td align="left">2012-11-26</td>
<td align="right">11162</td>
</tr>
<tr class="odd">
<td align="left">2012-11-27</td>
<td align="right">13646</td>
</tr>
<tr class="even">
<td align="left">2012-11-28</td>
<td align="right">10183</td>
</tr>
<tr class="odd">
<td align="left">2012-11-29</td>
<td align="right">7047</td>
</tr>
</tbody>
</table>

1.  Now we need to calculate the mean and median number of steps per day

<!-- -->

    #computing the mean steps per day 
    mean(steps_day$total_steps)

    ## [1] 10766.19

    median(steps_day$total_steps)

    ## [1] 10765

The mean is *107766* and the median *10765*

What is the average daily activity pattern?
===========================================

1.  Time series plot of the 5 minute interval (x) and the average number
    of steps taken averaged across all days (y)

<!-- -->

    #group  by interval and find the mean steps 
    mean_steps_i <- summarise(group_by(activity, interval), mean_steps= mean(steps))

Plotting the time series

    p2<- ggplot(data = mean_steps_i, aes(x = interval, y = mean_steps)) 
    p2 + geom_line(col= '#68228B') + xlab('Interval') +
      ylab('Mean steps per interval across all dates') +
      ggtitle( " Average number of steps taken across all days") +
      theme(plot.title = element_text(hjust = .5))

![](Figures/unnamed-chunk-8-1.png)

1.  Getting the time intervals with the max number of steps per day

<!-- -->

    # find the interval with the max number of steps
    mean_steps_i[which.max(mean_steps_i$mean_steps),]

    ## # A tibble: 1 × 2
    ##   interval mean_steps
    ##      <int>      <dbl>
    ## 1      835   206.1698

Imputing missing values
-----------------------

Note that there are a number of days/intervals where there are missing
values (coded as 𝙽𝙰). The presence of missing days may introduce bias
into some calculations or summaries of the data.

1.  Calculating the number of NA's

<!-- -->

    # from the raw data 
    nrow(data_raw[!complete.cases(data_raw),])

    ## [1] 2304

The number of rows with NA was found to be *2304*

1.  Devise a strategy to complete the missing values in the dataset.

As the mean data steps per time interval has already been computed
before, we are going to use that data to fill in the missing values.
This is done as follows:

-   Loop over the raw data and find the NA's
-   Then look up the mean for that time interval in the previoulsy
    defined dataframe `mean_steps_i`

<!-- -->

    dataFull <- data_raw

1.  Completing the values in the dataframe, the completed data frame is
    `dataFull`

<!-- -->

    for (i in 1:nrow(dataFull)){
      if (is.na(dataFull$steps[i])){
        interval_val <- dataFull$interval[i]
        row_id <- which(mean_steps_i$interval == interval_val)
        steps_val <- mean_steps_i$mean_steps[row_id]
        dataFull$steps[i] <- steps_val
      }
    }

1.  Create a histogram of the total number of steps taken each day using
    `dataFull`

<!-- -->

    # getting the total number of steps per day
    steps_dayF <- summarise(group_by(dataFull, Dates), total_steps= sum(steps))

    #plotting the data 
    p<-ggplot(data= steps_dayF, aes(x=Dates, y=total_steps))
    p + geom_bar(width = 1.0, stat ='identity', colour='#68228B', fill='#E6E6FA') +
      xlab('')+ylab('Total number of steps per day') + 
      ggtitle("Total number of steps taken each day") +
      theme(plot.title = element_text(hjust =0.5))

![](Figures/unnamed-chunk-13-1.png)

Now computing the mean and median and mean with the filled NA's

    mean(steps_dayF$total_steps)

    ## [1] 10766.19

    median(steps_dayF$total_steps)

    ## [1] 10766.19

The mean and median of the data set with the replaced NA values well
10766, the mean presented no changes after adding the values while the
median went from 10765 to 10766.

However when looking at the two histgrams presented is is evident that
all the days corresponding to the period of time considered have now a
total number of steps. As the values used for filling the NA's was the
mean value for each interval no major changes were expected to be
observed when computing the mean of the steps per time interval.

Are there differences in activity patterns between weekdays and weekends?
=========================================================================

1.  Create a factor variable to identify weekends and weekdays

<!-- -->

    # creating the factor variable 
    dataFull$week<- as.factor(ifelse(weekdays(dataFull$Dates) %in% c("Saturday","Sunday"), "Weekend", "Weekday")) 
    # now finding the mean steps per interval 
    mean_steps_Fi<- aggregate(steps ~ interval + week, data = dataFull, mean)

1.  Making a panel plot of the time series of the 5 minutes intervals
    and the mean steps taken across all wekeend days and weekdays

<!-- -->

    p4<- ggplot(mean_steps_Fi, aes(interval, steps, colour = factor(week))) 
    p4 + geom_line() +facet_grid(.~ week) +
      xlab('Intervals') + ylab('Average number of steps')

![](Figures/unnamed-chunk-16-1.png)
