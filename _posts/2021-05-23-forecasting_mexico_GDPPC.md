---
layout: post
title: "An Introduction to Forecasting Modeling"
subtitle: "Time Series Linear Model and Averages Method"
background: '/img/forecasting/future.png'
output: html_document
date: 2021-05-22 19:50:00 -0400
category: r
tags: [data analysis, forecasting, r]
comments: true
---
 

> Rob J. Hyndman: "Forecasting it's required in many situations: deciding whether to build another power generation plant in the next ten years requires forecasts of future demand; scheduling staff in a call centre next week requires forecasts of call volumes; stocking an inventory requires forecasts of stock requirements."

#### Forecasting is divided into two categories

![](/img/forecasting/HD.png) 




**For example, this is a Financial Model that I have been doing**


![](/img/forecasting/financeexample.png)<!-- -->

> This model include a forecasting method based on averages. This method is commonly used in this type of financial models for the purpose of determining the Value of a Business. Remember: *Forecasting is the process of making predictions based on past and present data*.


#### Let's continue.

For this project, I'm going to  **forecasting Mexico GDPPC for the next 3 years** with a *time series linear model*


>Gross Domestic Product Per Person (GDPPC) is a metric that breaks down a country’s economic output per person and is calculated by dividing the GDP of a country by the population.


##### I’ll use **fpp3** package. Created by **Rob J Hyndman and George Athanasopoulos.**

You can install and load the package with this code:

``` r
install.packages(‘fpp3’, dependencies = TRUE)
```

``` r
library(fpp3)
```

### Manipulating data

By default, we have a data set named global_economy. This data set contains 9 variables:

> Country, Code, Year, GDP, Growth, CPI, Imports, Exports, Population.

**We only need Country, GDP and Population.**

I'm going to start creating a new column. This code divide GPD and Population and creates GPDPC.

``` r
percapita <- global_economy %>%
  mutate(GDP_per_capita = GDP / Population)
```

Then, we filter and plot.

``` r
percapita %>% 
  filter(Country == "Mexico") %>% 
  ggplot(aes(x = Year, y = GDP_per_capita))  +
  geom_line(color = "indianred3", 
            size=2 ) +
  geom_smooth() +
  labs(y = "$US",
       x = "Year",
       title = "GPD Per Capita for Mexico") +
  theme_minimal() +
  scale_color_brewer(palette = "Dark2")
```

![](/img/forecasting/chunknuevo.png)<!-- -->

**Now we can define and *train* time series linear model**

``` r
TSLM(GDP_per_capita ~ trend())
```
``` r
fit <- percapita %>%
  model(trend_model = TSLM(GDP_per_capita ~ trend()))
```


**We can see the model by writing fit.**

``` r
fit
```

    ## # A mable: 263 x 2
    ## # Key:     Country [263]
    ##    Country             trend_model
    ##    <fct>                   <model>
    ##  1 Afghanistan              <TSLM>
    ##  2 Albania                  <TSLM>
    ##  3 Algeria                  <TSLM>
    ##  4 American Samoa           <TSLM>
    ##  5 Andorra                  <TSLM>
    ##  6 Angola                   <TSLM>
    ##  7 Antigua and Barbuda      <TSLM>
    ##  8 Arab World               <TSLM>
    ##  9 Argentina                <TSLM>
    ## 10 Armenia                  <TSLM>
    ## # ... with 253 more rows


**Producing forecasting**


``` r
fit %>% forecast(h = "3 years")
```

    ## # A fable: 789 x 5 [1Y]
    ## # Key:     Country, .model [263]
    ##    Country        .model       Year   GDP_per_capita  .mean
    ##    <fct>          <chr>       <dbl>           <dist>  <dbl>
    ##  1 Afghanistan    trend_model  2018     N(526, 9653)   526.
    ##  2 Afghanistan    trend_model  2019     N(534, 9689)   534.
    ##  3 Afghanistan    trend_model  2020     N(542, 9727)   542.
    ##  4 Albania        trend_model  2018  N(4716, 476419)  4716.
    ##  5 Albania        trend_model  2019  N(4867, 481086)  4867.
    ##  6 Albania        trend_model  2020  N(5018, 486012)  5018.
    ##  7 Algeria        trend_model  2018  N(4410, 643094)  4410.
    ##  8 Algeria        trend_model  2019  N(4489, 645311)  4489.
    ##  9 Algeria        trend_model  2020  N(4568, 647602)  4568.
    ## 10 American Samoa trend_model  2018 N(12491, 652926) 12491.
    ## # ... with 779 more rows

``` r
fit %>%
  forecast(h = "3 years") %>%
  filter(Country == "Mexico") %>%
  autoplot(percapita) +
  labs(y = "$USD", title = "GPD Per Capita for Mexico")
```

![](/img/forecasting/forecastmexico.png)<!-- -->


### Nice, right?

---

#### Connect with me:

### [🔥 Substack ](https://joseluistello.substack.com/)
### [✔️ Twitter](https://twitter.com/jotaele_tello)
### [😊 Linkedin](https://www.linkedin.com/in/joseluistello/)
### [📈 Resume](https://www.notion.so/joseluistello/resume-908176d50910492f82bb0c2c50150406)
### [❤️ DataBase](https://www.notion.so/joseluistello/resources-3b96a11183d342b889c95e9bcb1e0c7f)
---


