---
title       : ARIMA?!
subtitle    : When a forecasting project is not one
author      : Reza Hosseini
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {selfcontained, standalone, draft}
knit        : slidify::knit2slides
---
## Outline



```
## Error in as.Date.numeric(new_date): 'origin' must be supplied
```
 * The problem
 
 * Is it a forecast problem?
 
 * Weakly seasonality
 
 * Multiseasonal time series
 
 * Machine learning approach


---

## The problem

### Forecasting the number of visitors to Nettebad Osnabrück. Using
* Visitors to the pool from 2005-03-20
* Some variables about the pool such as events, classes, availability of certain facilities etc.
* Weather data

https://inclass.kaggle.com/c/swimming-pool-visitor-forecasting
<img src="assets/fig/unnamed-chunk-3-1.png" title="plot of chunk unnamed-chunk-3" alt="plot of chunk unnamed-chunk-3" style="display: block; margin: auto;" />

---
<!-- Timo, Thomas,  -->


## Is it a forecast problem?
* It seems so, but looking at the lag plots ...

<img src="assets/fig/unnamed-chunk-4-1.png" title="plot of chunk unnamed-chunk-4" alt="plot of chunk unnamed-chunk-4" style="display: block; margin: auto;" />

---

## Is it a forecast problem?
* It seems so, but looking at the lag plots ...

<img src="assets/fig/unnamed-chunk-5-1.png" title="plot of chunk unnamed-chunk-5" alt="plot of chunk unnamed-chunk-5" style="display: block; margin: auto;" />

---

## Is it a forecast problem?
* It seems so, but looking at the lag plots ...

<img src="assets/fig/unnamed-chunk-6-1.png" title="plot of chunk unnamed-chunk-6" alt="plot of chunk unnamed-chunk-6" style="display: block; margin: auto;" />

---
## Is it a forecast problem?
* It seems so, but looking at the lag plots ...

<img src="assets/fig/unnamed-chunk-7-1.png" title="plot of chunk unnamed-chunk-7" alt="plot of chunk unnamed-chunk-7" style="display: block; margin: auto;" />

---

## Is it a forecast problem
* And the autocorrelation plot

<img src="assets/fig/unnamed-chunk-8-1.png" title="plot of chunk unnamed-chunk-8" alt="plot of chunk unnamed-chunk-8" style="display: block; margin: auto;" />

---
## Weekly seasonality
- Autocorrelation plot suggested weekly seasonality in the data 
- The missing days is imputed and the time series is decomposed
<img src="assets/fig/unnamed-chunk-9-1.png" title="plot of chunk unnamed-chunk-9" alt="plot of chunk unnamed-chunk-9" style="display: block; margin: auto;" />

---

## Accuracy of the seasonality

```
## Error in data.frame(weekday = we, Total.Visitors = visitors, Seasonality.Removed = rem): arguments imply differing number of rows: 2820, 2837
```

```
## Error in melt(d, id.vars = "weekday"): object 'd' not found
```

```
## Error in ggplot(data, aesthetics, environment = env): object 'melted' not found
```

---

## Forecasting via decomposition
<img src="assets/fig/unnamed-chunk-11-1.png" title="plot of chunk unnamed-chunk-11" alt="plot of chunk unnamed-chunk-11" style="display: block; margin: auto;" />

<img src="assets/fig/unnamed-chunk-12-1.png" title="plot of chunk unnamed-chunk-12" alt="plot of chunk unnamed-chunk-12" style="display: block; margin: auto;" />

---


## Last three years
<img src="assets/fig/unnamed-chunk-13-1.png" title="plot of chunk unnamed-chunk-13" alt="plot of chunk unnamed-chunk-13" style="display: block; margin: auto;" />

---

## Last three years
<img src="assets/fig/unnamed-chunk-14-1.png" title="plot of chunk unnamed-chunk-14" alt="plot of chunk unnamed-chunk-14" style="display: block; margin: auto;" />

- One could remove seasonality and do the prediction on the remainder, then add seasonality

- The best RMSE I could get with this approach was 330.15

---
## Multiseasonality approach
* As there are two kinds of sesonality, one can use multiseasonal time series and TBATS

<img src="assets/fig/unnamed-chunk-16-1.png" title="plot of chunk unnamed-chunk-16" alt="plot of chunk unnamed-chunk-16" style="display: block; margin: auto;" />

---
## Forecast by TBATS
* Reached RMSE of 376
<img src="assets/fig/unnamed-chunk-17-1.png" title="plot of chunk unnamed-chunk-17" alt="plot of chunk unnamed-chunk-17" style="display: block; margin: auto;" />

---

## Machine learning approach

- School and bank holidays
- Weekday and month name to  consider seasonality
- Weather data (temprature, wind, preception,...)
- New features
    * Monthly average temprature
    * Warmer than monthly average
    * Warmer than the previous day
    * Heat index
- Adjust prices by consumer price index (CPI)

---

## Machine learning approach

- Train a random forest to get feature importance
- Use the most important feature (99% cumulative importance)
- Use gradient boosting (XGboost) for the final prediction
- Adjust christmas and new years manually to the previous year value

* The final rmse is 247.33 (269.89 without manuall adjusment)

---

## Machine learning approach
<img src="assets/fig/unnamed-chunk-18-1.png" title="plot of chunk unnamed-chunk-18" alt="plot of chunk unnamed-chunk-18" style="display: block; margin: auto;" />

---

## Machine learning approach
<img src="assets/fig/unnamed-chunk-19-1.png" title="plot of chunk unnamed-chunk-19" alt="plot of chunk unnamed-chunk-19" style="display: block; margin: auto;" />

---



## Thank you for your patience

---

## With confidence interval
<img src="assets/fig/unnamed-chunk-20-1.png" title="plot of chunk unnamed-chunk-20" alt="plot of chunk unnamed-chunk-20" style="display: block; margin: auto;" />
---
