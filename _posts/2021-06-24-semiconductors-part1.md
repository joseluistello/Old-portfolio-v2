---
layout: post
title: "Semiconductor Market Analysis"
subtitle: "Visualizing the Stock Market With Tidyverse and TidyQuant"
background: '/img/semiconductores/3.png'
output: html_document
date: 2021-06-28 19:50:00 -0400
category: r
tags: [data analysis, forecasting, r, finance]
comments: true
---


We know that Semiconductors industry it's a complex industry. Without this industry, We could not be reading this article. We could not imagine all this progress. But understand this monster it's hard.

--- 
That's why I created this project. **I'm going to divide the project in 2 parts.** 

> The first part is divided into 4 main points:

* A short introduction about the business model that exist in the industry 
* A comparation about some index's with specially focus on FOX Index 
* Select the companies that we will be analyzing throughout the project
* Create models around the data and plot some nice visualizations

> The second part is divided into X points:

* I'm going to talk about one companie in particular 
* Select some financial ratios
* Download and plot the data
* Explain patterns 
* Regression analysis and forecasting modeling
  

---
> **For me**, the goal of this project consists on show you my knowledge on quant financial analysis, statistical learning and writing.

> **For you**, the project consists on understanding how the industry works, his performance over the years and why not, pick the opportunity to invest in the semiconductor industry.

---
Let's begin with the first main point... **the business models.** In order to understand the complexity around the industry, we need an overview of the process for creating an IC'S 

![Index](/img/semiconductores/process.png)

> *As wee see, there are many steps. But we can categorize the whole process in three major business models.*

![Index](/img/semiconductores/HD.png)

### 1.- Foundry

**Foundry companies are concerned only with IC manufacturing.**

> The foundry model is a microelectronics engineering and manufacturing business model consisting of a semiconductor fabrication plant, or foundry, and an integrated circuit design operation, each belonging to separate companies or subsidiaries.

**Foundry Model it's dominated by TSMC.**

### 2.- IDM

**IDMs design and manufacture integrated circuits (ICs).**

> An integrated device manufacturer (IDM) is a semiconductor company which designs, manufactures, and sells integrated circuit (IC) products. As a classification, IDM is often used to differentiate between a company which handles semiconductor manufacturing in-house, and a fabless semiconductor company, which outsources production to a third-party. Due to the dynamic nature of the semiconductor industry, the term IDM has become less accurate than when it was coined.

**Intel and Texas instruments are examples of this model.**

### 3.- Fabless

Fabless companies focus only on IC design.

> Fabless manufacturing is the design and sale of hardware devices and semiconductor chips while outsourcing their fabrication (or fab) to a specialized manufacturer called a semiconductor foundry. Foundries are typically, but not exclusively, located in the United States, People's Republic of China, and Taiwan. Fabless companies can benefit from lower capital costs while concentrating their research and development resources on the end market. Some fabless companies and pure play foundries (like TSMC) may offer integrated-circuit design services to third parties.

**Broadcom, Qualcomm and AMD are examples of this model.**


### Let's begin with an index performance comparation

I'm going to use the **PHLX Semiconductor Sector** Index

> PHLX Semiconductor Sector is a Philadelphia Stock Exchange capitalization-weighted index composed of the 30 largest companies primarily involved in the design, distribution, manufacture, and sale of semiconductors. It was created in 1993 by the Philadelphia Stock Exchange

![Index](/img/semiconductores/performancecomparation.png)


* **Blue_SOX.-** PHLX Semiconductor
* **BlueSky_DJI.-** Dow Jones Industrial 
* **Pink_IXIC.-** NASDAQ COMPOSITE
* **Purple_GSPC.-** S&P 500
* **Orange_DAX.-** German Index
* **Yellow_TSXV.-** S&P/TSX CANADA COMPOSITE INDEX

**If we look closely, the PHLX Index outperforms the NASDAQ COMPOSITE which contains companies like Apple, Amazon, Facebook and Alphabet... not bad, right?** So, for this project i'm going to choose 2 or 3 per model:

* **Foundry:** TSMC and UMC.
* **IDM’s:** Intel, Texas instruments and NPX
* **Fabless:** Broadcomm, Qualcomm and Nvidia.

These are the packages I will use throughout the project:

* **Tidyquant** for finance
* **Tidyverse** for dplyr and ggplot2
* **Fpp3** for forecasting models
* **Ggthemes** for beautiful plots

---

### CODE

#### First, I need to download the data:

```{r}
sc_companies <- c("TSM", "UMC", "INTC", "TXN", "NXP", "NVDA", "AVGO", "QCOM") %>%
  tq_get(get  = "stock.prices",
         from = "2015-01-01",
         to   = "2021-06-27")
```

```{r}
foundry <- c("TSM", "UMC") %>%
  tq_get(get  = "stock.prices",
         from = "2015-01-01",
         to   = "2021-06-27")
```

```{r}
idm <- c("INTC", "TXN", "NXP") %>%
  tq_get(get  = "stock.prices",
         from = "2015-01-01",
         to   = "2021-06-27")
```

```{r}
fabless <- c("NVDA", "AVGO", "QCOM") %>%
  tq_get(get  = "stock.prices",
         from = "2015-01-01",
         to   = "2021-06-27")
```

#### Then, I need to plot the data

**Let's see an overview**

```{r}
  ggplot(sc_companies, 
         aes(x = date, y = close, color = symbol)) + 
    geom_line(size=1) +
    labs(title = "Semiconductor Stock Price",
         subtitle = 'A comparation between companies',
         x = 'Date',
         y =  "Close Price") +
    theme_minimal() +
    scale_color_brewer(palette = "Dark2") 
```

![Index](/img/semiconductores/semiconductorstockprice.png)



**Let's wrap for a better view.**

```{r}
  ggplot(sc_companies, 
         aes(x = date, y = close, color = symbol)) + 
    geom_line(size=1) +
    labs(title = "Semiconductor Stock Price Growth",
         subtitle = '',
         x = 'Date',
         y =  "Close Price") +
    theme_minimal() +
    scale_color_brewer(palette = "Dark2") +
    facet_wrap(~ symbol, ncol = 2, scale = "free_y")
```

![Index](/img/semiconductores/semiconductorwrap.png)



### It's time to see between business models.


```{r}
  ggplot(foundry, 
         aes(x = date, y = close, color = symbol)) + 
    geom_line(size=1) +
    labs(title = "Semiconductor Stock Price",
         subtitle = 'Foundry business model',
         x = 'Date',
         y =  "Close Price") +
    theme_minimal() +
    scale_color_brewer(palette = "Dark2") 
```

![Index](/img/semiconductores/foundrystock.png)

```{r}
  ggplot(fabless, 
         aes(x = date, y = close, color = symbol)) + 
    geom_line(size=1) +
    labs(title = "Semiconductor Stock Price",
         subtitle = 'Fabless business model',
         x = 'Date',
         y =  "Close Price") +
    theme_minimal() +
    scale_color_brewer(palette = "Dark2") 
```

![Index](/img/semiconductores/fablessstock.png)

```{r}
  ggplot(idm, 
         aes(x = date, y = close, color = symbol)) + 
    geom_line(size=1) +
    labs(title = "Semiconductor Stock Price",
         subtitle = 'IDM business model',
         x = 'Date',
         y =  "Close Price") +
    theme_minimal() +
    scale_color_brewer(palette = "Dark2") 
```

![Index](/img/semiconductores/idmstock.png)

### The trend it's kinda obvious but remember... I have my personal goals for this project

```{r}
  sc_companies %>% 
    filter(symbol == "QCOM") %>% 
   ggplot(aes(x = date, y = close, color = symbol))  +
  geom_line(color = "indianred3", 
            size=1 ) +
  geom_smooth() +
  labs(title = "Semiconductor Stock ",
         subtitle = 'Qualcomm Trend',
         x = 'Date',
         y =  "Close Price") +
  theme_minimal() +
  scale_color_brewer(palette = "Dark2") +
    facet_wrap(~ symbol, ncol = 2, scale = "free_y")
```

![Index](/img/semiconductores/qualcomtrend.png)

### Let's see the anual returns for each companie categorize by model

```{r}
semicompanies_return_yearly_idm <-  idm %>%
    group_by(symbol) %>%
    tq_transmute(select     = adjusted, 
                 mutate_fun = periodReturn, 
                 period     = "yearly", 
                 col_rename = "yearly.returns") 
```

```{r}
semicompanies_return_yearly_idm %>%
    ggplot(aes(x = year(date), y = yearly.returns, fill = symbol)) +
    geom_bar(position = "dodge", stat = "identity") +
    labs(title = "Anual Returns", 
         subtitle = "IDM Business Model",
         y = "Returns", x = "", color = "") +
    scale_y_continuous(labels = scales::percent) +
    coord_flip() +
    theme_tq() +
    scale_fill_tq()
```

![Index](/img/semiconductores/idmreturns.png)

```{r}
semicompanies_return_yearly_fabless <- fabless %>%
    group_by(symbol) %>%
    tq_transmute(select     = adjusted, 
                 mutate_fun = periodReturn, 
                 period     = "yearly", 
                 col_rename = "yearly.returns")
```


```{r}
semicompanies_return_yearly_fabless %>%
    ggplot(aes(x = year(date), y = yearly.returns, fill = symbol)) +
    geom_bar(position = "dodge", stat = "identity") +
    labs(title = "Anual Returns", 
         subtitle = "Fabless Business Model",
         y = "Returns", x = "", color = "") +
    scale_y_continuous(labels = scales::percent) +
    coord_flip() +
    theme_tq() +
    scale_fill_tq()
```

![Index](/img/semiconductores/fablessreturn.png)

```{r}
semicompanies_return_yearly_foundry <- foundry %>%
    group_by(symbol) %>%
    tq_transmute(select     = adjusted, 
                 mutate_fun = periodReturn, 
                 period     = "yearly", 
                 col_rename = "yearly.returns")
```

```{r}
semicompanies_return_yearly_foundry %>%
    ggplot(aes(x = year(date), y = yearly.returns, fill = symbol)) +
    geom_bar(position = "dodge", stat = "identity") +
    labs(title = "Anual Returns", 
         subtitle = "Foundry Business Model",
         y = "Returns", x = "", color = "") +
    scale_y_continuous(labels = scales::percent) +
    coord_flip() +
    theme_tq() +
    scale_fill_tq()
```

![Index](/img/semiconductores/foundryreturn.png)