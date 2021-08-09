---
layout: post
title: "Data Visualization Olympic Medals 2021"
subtitle: "Visualizing Tokyo with R, Ggplot and Dplyr"
background: '/img/tokyo2021/tokyo3.png'
output: html_document
date: 2021-08-09 19 -0400
category: r
tags: [data visualization, r]
comments: 
---

```r
library(tidyverse)
```

```r
medals <- read.csv("data/raw/tokyo2021.csv", header = TRUE)
```
MMMM… I need to change this col names!

```r
str(medals)

## 'data.frame':    93 obs. of  8 variables:
##  $ Rank         : int  1 2 3 4 5 6 7 8 9 10 ...
##  $ Team.NOC     : chr  "United States of America" "People's Republic of China" "Japan" "Great Britain" ...
##  $ Gold.Medal   : int  39 38 27 22 20 17 10 10 10 10 ...
##  $ Silver.Medal : int  41 32 14 21 28 7 12 12 11 10 ...
##  $ Bronze.Medal : int  33 18 17 22 23 22 14 11 16 20 ...
##  $ Total        : int  113 88 58 65 71 46 36 33 37 40 ...
##  $ Rank.by.Total: int  1 2 5 4 3 6 9 10 8 7 ...
##  $ NOCCode      : chr  "USA" "CHN" "JPN" "GBR" ...
```


## Data Wrangling

1.  Create a frame with new column names

<!-- -->

```r
tokyo2021 <- rename(medals, 
    country = Team.NOC,
    gold = Gold.Medal,
    silver = Silver.Medal,
    bronze = Bronze.Medal,
    rankbytotal = Rank.by.Total,
    ccode = NOCCode
            )
```

```r
tokyo <- as_tibble(tokyo2021)
```

## Data Viz!

```r
tokyo %>% 
group_by(country) %>% 
count(gold) %>% 
filter(gold >= 10) %>% 
ggplot(aes(x = reorder(country, gold), y = gold)) +
geom_bar(stat = 'identity', 
        size=1, 
        fill="darkgoldenrod2",) +
geom_text(aes(label = gold),
        vjust = .5, nudge_y = .90, nudge_x = 0.15) +
labs(x = "Country",
    y = "Gold Medals",
    title = "Countries with the most Gold medals") +
coord_flip() +
theme_classic() +
theme(legend.position = "none")
```

![Gold](/img/tokyo2021/gold.png)

```r
tokyo %>% 
group_by(country) %>% 
count(silver) %>% 
filter(silver >= 10) %>% 
ggplot(aes(x = reorder(country, silver), y = silver)) +
geom_bar(stat = 'identity', 
        size=1,
        fill="azure3") +
geom_text(aes(label = silver),
        vjust = .5, nudge_y = .90, nudge_x = 0.15) +
labs(x = "Country",
    y = "Silver Medals",
    title = "Countries with the most Silver medals") +
coord_flip() +
theme_classic() +
theme(legend.position = "none")
```

![Silver](/img/tokyo2021/silver.png)

```r
tokyo %>% 
group_by(country) %>% 
count(bronze) %>% 
filter(bronze >= 10) %>% 
ggplot(aes(x = reorder(country, bronze), y = bronze)) +
geom_bar(stat = 'identity', 
        size=1,
        fill="chocolate3") +
geom_text(aes(label = bronze),
        vjust = .5, nudge_y = .90, nudge_x = 0.15) +
labs(x = "Country",
    y = "Bronze Medals",
    title = "Countries with the most Bronze medals") +
coord_flip() +
theme_classic() +
theme(legend.position = "none")
```

![Bronze](/img/tokyo2021/bronze.png)

```r
tokyo %>% 
select(country, Total) %>% 
slice_max(Total, n = 10) %>% 
ggplot(aes(x = reorder(country, Total), y = Total)) +
geom_bar(stat = 'identity', 
        size=1,
        fill="chocolate3") +
geom_text(aes(label = Total),
        vjust = .70, nudge_y = 3, nudge_x = 0.15) +
labs(x = "Country",
    y = "Medals",
    title = "Countries ranked by total medals") +
coord_flip() +
theme_classic() +
theme(legend.position = "none")
```

![Total_Medals](/img/tokyo2021/totalrank.png)


```r
ggplot(tokyo, aes(x = Total,
                y= ..count.. / sum(..count..))) +
geom_histogram(fill = "cornflowerblue",
                color = "black",
                binwidth = 9) +
scale_y_continuous(labels = percent) +
labs(x = "Medals",
    y = "Count Percent",
    title = "Medals distribution"
    ) +
theme_classic() 
```

![Distribution](/img/tokyo2021/histograms.png)
