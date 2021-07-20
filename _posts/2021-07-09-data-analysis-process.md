---
layout: post
title: "Data Analysis Process"
description: "A General View To My Approach"
output: html_document
date: 2021-07-12 19:50:00 -0400
category: r
tags: [data analysis, machine learning, r, data wrangling]
comments: true
---


### Hi there 👋

#### This project it's special. I'll write about thinking, data analysis, and how to approach problems and solve them systematically. 

This is how I see structures and *what I hope to accomplish here is to give you MY way of thinking about data analysis.* 
 
##### As Sam Hinkie [wrote](https://www.espn.com/pdf/2016/0406/nba_hinkie_redact.pdf) on Seth Klarman and his approach at Baupost Group: 
> **It isn’t the only way of thinking, but it’s how we approach it.**  

#### Thinking about thinking

There are different methods to attack a problem, usually called mental models. These tools are frameworks of thinking that humans have made to approach solutions.

#### Reductionism 💡

For example, Elon Musk has his favorite framework of thinking: *the first principles*. This model can be classified as a reductionist method. 

> First Principles consist in break a whole problem into small parts. This approach helps Elon back then in the early years when he wanted to create a cheaper and more accessible rocket compared to the Russians. Yes, this was the story behind SpaceX.

I'm a big fan of reductionist thinking. We can adopt it when we are study statistical models. It is helpful to see each part of a linear regression and how [it's composed](https://www.youtube.com/watch?v=nk2CQITm_eo). 

![alt text](/img/data%20analysis/linear%20regression.png)

*Or even for the purpose to describe three of the four fundamental forces in the universe, as well as classifying elementary particles we know today.*

[The Standard Model Of Particle Physics](https://cosmicescapes.com/the-standard-model-of-particle-physics/)


![alt text](/img/data%20analysis/structure-of-std-mdl.png)


#### What is the opposite way of thinking 


##### 💡 Remember 💡 




The Analysis Data Process depends on the context in which you find yourself. 
- 👉🏼 Use this process as a framework 👈🏼 
  
If you are in the stage of Analyze, you can back to the Problem Stage. In the real world it's normal to go back to the problem stage and understand that the quality of our data is not optimal. Specially when you are helping to grow a company! 


##### A holistic way to see the process

![Index](/img/data%20analysis/HD.png)


#### Step 1.- Understand the problem and ask the right questions


. 
















#### Step 2.-  Understand Data





#### Step 2.- Preprocess And Analyze Data





#### Step 3.- Model Data

#### Step 4.- Analyze Data 






#### Step 6.- Report And Communicate










---

```{r}
library(tidyverse)
library(ggthemes)
```
```{r}
train <- read.csv("data/train.csv", header = TRUE)
test <- read.csv("data/test.csv", header = TRUE)
```

```{r}
str(train)
```

```{r}
str(test)
```
##### Drop NA values from test set
```{r}
test <- data.frame(test[1], Survived = rep("NA", nrow(test)), test[ , 2:ncol(test)])
```

##### Merge train and test for visualization and analysis

```{r}
data <- rbind(train, test)
```

##### Create file from rbind product
```{r}
write.csv(data, "./data/data.cvs", row.names = FALSE )
```

```{r}
length(data$PassengerId)
```

```{r}
length(unique(data$PassengerId))
```

```{r}
data$Survived <- as.factor(data$Survived)
table(data$Survived, dnn = "Number of Survived in Data Frame")
```

```{r}
prop.table(table(as.factor(train$Survived), dnn = "Survive and death ratio in Train Data"))
```

##### Time to change type of data

```{r}
data$Pclass <- as.factor(data$Pclass)
```


```{r}
table(data$Pclass, dnn = "Pclass values in Data")
```
















---

### Hi! this project it's under construction.


### If you want to see more of my work, check this out:

### 📕 Latest Blog Posts and Projects

<!-- BLOG-POST-LIST:START -->
- [Definiendo el valor y la estructura de precios](https://joseluistello.substack.com/p/valor-y-estructura-de-precios)
- [Estructura de costos](https://joseluistello.substack.com/p/estructura-de-costos)
- [Fijación de precios](https://joseluistello.substack.com/p/fijacin-de-precios)
- [An Introduction to Forecasting Modeling](https://joseluistello.github.io/r/forecasting_mexico_GDPPC/)
- [Semiconductor Market Analysis](https://joseluistello.github.io/r/semiconductors-part1/)

<!-- BLOG-POST-LIST:END -->

## Connect with me:

### [🔥 Substack ](https://joseluistello.substack.com/)
### [✔️ Twitter](https://twitter.com/jotaele_tello)
### [😊 Linkedin](https://www.linkedin.com/in/joseluistello/)
### [📈 Resume](https://www.notion.so/joseluistello/resume-908176d50910492f82bb0c2c50150406)
### [❤️ DataBase](https://www.notion.so/joseluistello/resources-3b96a11183d342b889c95e9bcb1e0c7f)
---

---