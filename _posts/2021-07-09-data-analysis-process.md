---
layout: post
title: "Data Analysis Process"
subtitle: "A General View To My Approach"
background: '/img/data analysis/tukeyy.png'
output: html_document
date: 2021-07-12 19:50:00 -0400
category: r
tags: [data analysis, machine learning, r, data wrangling]
comments: true
---

## 🚭 UNDER CONSTRUCTION 🚭

**Essay in honor of [John W. Tukey.](https://en.wikipedia.org/wiki/John_Tukey)** 

> *Without his contributions, I could not be writing this post... Hope you enjoy it.* 

There is a [famous letter](https://www.espn.com/pdf/2016/0406/nba_hinkie_redact.pdf) by Samuel Hinkie where he talks about his journey serving the Sixers. He wrote magnificent references, but there is one that I love on Seth Klarman and his approach at Baupost Group:

> **"It isn’t the only way of thinking, but it’s how we approach it."**  

Those words te way I see structures, data analysis, and problem-solving. This is not unique, but it's how I approach it. In the end, the knowledge I have is the result of all the interactions throughout my life.  

#### Thinking about small things

There are different methods to attack a problem, usually called mental models. These models are abstractions of how we see something. Usually, start as an assumption until knowledge and experience transform them into a tool of thinking that humans have made to approach solutions. 

An example could be Elon Musk and the *first-principles*. This mental model consists of breaking a whole problem into small parts. The first principles (and his reductionist nature) [helped Elon](https://www.youtube.com/watch?v=NV3sBlRgzTI) back then in the early years when he creates a cheaper and more accessible rocket. 

> [Reductionism](https://en.wikipedia.org/wiki/Reductionism) is any of several related philosophical ideas regarding the associations between phenomena, which can be described in terms of other simpler or more fundamental phenomena. It is also described as an intellectual and philosophical position that interprets a complex system as the sum of its parts.

In simple words, reductionism maintain that whole (phenomenon) can be understood from the essence of his parts and the relations among them, even if those parts are different from each other.

I'm a big fan of reductionism. This way of thinking can be adopted when we are studying statistical models. It is helpful to see each part of a model and how [it's composed](https://www.youtube.com/watch?v=nk2CQITm_eo). 

![alt text](/img/data%20analysis/linear%20regression.png)

Or even for the purpose to describe three of the four fundamental forces in the universe. [The Standard Model Of Particle Physics.](https://cosmicescapes.com/the-standard-model-of-particle-physics/)

#### Thinking about big things

It's time to see the whole picture. We know that reductionism breaks phenomenons into small things and understands the whole by seen the interaction among them. 

What about Holism?

>[Holism](https://link.springer.com/chapter/10.1007/978-3-030-11636-1_5) maintain the contrary view, that the parts of a whole are internally related, so that the essence of each is partially constituted by the properties of all the others and of the whole. Hence, the whole cannot be understood from its parts and their relations to each other alone; and conversely, the parts cannot be fully understood apart from the whole. 

Business understand this way of thinking. Specially disciplines like growth and product who needs to understand the whole picture.

This is a great example created by [Reforge](https://www.reforge.com/blog/growth-loops)

![Loops](/img/data%20analysis/Loops.png)

#### The union between small and big things

I don't believe that Reductionism and Holism are not mutually exclusive. I think they are great frameworks of thinking, and without fanaticism, we can use them powerfully.

There's a way named systematic thinking. This thinking creates a balance between Reductionism and Holism. 

> [By thinking about the overall system](https://www.intelligentspeculation.com/blog/systems-thinking) at once and how everything fits together, you are more likely to account for nuanced interactions between components that could lead to negative, unintended consequences if left unaccounted for.  

We can say that systemic thinking allows us to unite the two ways of looking at a phenomenon. With systems thinking, we can deconstruct a complex Phenomenon while understanding his context. 

- Can the product team invest in new improvements, or is it better to concentrate on closing deals? 
- Can the engineering team scale up at the same time as user acquisition and retention?


We can stop seeing a problem as monolithic. Instead, we can treat a problem as a series of actions and consequences that are interrelated. With this thinking, we can visualize patterns to attack a problem.

---

At this point you may be wondering how all this is related to data analysis? 

One step for any thinking framework is always analysis (vice versa), and this analysis always contains data. It doesn't matter if it is critical thinking, design thinking, problem-solving, logical thinking, etc. Everything leads to analysis, reductionism, holism, and systems thinking.

Let me show you what I mean with a real example using the [classical titanic dataset.](https://www.kaggle.com/c/titanic) 

![Index](/img/data%20analysis/HD.png)

#### 1️⃣ Understand problem

As we see, the first step is to understand what problem you have and what do you want to accomplish. This is the most important and difficult part of data analysis (in my opinion).

* What exactly is the question? 
* What motivates our efforts? 
* What are the risks?
* What is our goal?

For this example, the problem and the goal is simply. We are going to work with something clean and nicely done. But in most cases, your first question will lead to many other questions.

For example, In my last project (4-3 months ago), I work with a construction holding. The project consists on creates storage tanks with a capacity of 200 thousand liters. The process includes steel plates of 3 tons and inches of various thicknesses, anti-corrosive paint, and sand-blast. 

The final product is something like this:

![Tanks](/img/data%20analysis/tanques-de-almacenamiento.png)

Construction projects are budgeted. If you agreed on a price range for a product, you can't go outside that range. 

The problems come with the painting process. We reached a point where we were at 60% of the final goal (8 tanks), but our warehouse did not have enough paint left in stock to finish the project. Alarm bells began to ring. We had a problem that we didn't know how to define.

As a quality inspector, my job was to find the real problem and propose solutions. I worked hard that week... I stayed in the office until 2:30. I was trying to think about what was going on my way to my home.

So, I design a lot of experiment-based in metrics, observation, and repetition. We work with quantitative metrics like temperature, dew point, relative humidity, pressure, etc.

**The main goal of my experiment was to find my problem.** I wanted to correlate like crazy. Weeks ago (and thanks to our client's request for documentation), I designed a database to capture everything. It was nothing sophisticated, but it was enough to give me data. I subjected to all kinds of analysis my metric of paint expenditure per day... *multivariate regression analysis* was my close friend.  

I could not see anything. Yes, there was the correlation that there should be, but nothing out of the ordinary. The compressor pressure was constant, the temperature didn't affect the flow rate and neither did the anchoring.

All this work just to put me in the context that I need for understand MY PROBLEM.

Do you want to know what the problem was? One of the suppliers made a mistake when he made the financial quotation. It never occurred to us to start from there, especially me. Sounds obvious but believe me, when we face timelines and pressure on our shoulders **the obviousness goes unnoticed.** 

--- 

EDITAR de aqui para abajo 

---

#### 2️⃣ Understand Data

We can classify data into 2 groups: 

* Qualitative data responds questions like **what** and is classify in two groups:
  * Nominal data - Don't have and orden
  * Ordinal data - Have an orden
>
* Quantitative data responds questions like **how many**, **how much**, or **how often** and is classify in two grupus:
  * Discrete data - Don't have decimals
    * Ordinal 
    * Nominal
    * Binary 
  * Continuos data - Have decimals
    * Ratio
    * Interval

 Lets check our data dictionary and variable notes to explain data type based on statistics.

![Notes](/img/data%20analysis/variablesdata.png)

![Notes](/img/data%20analysis/notes.png)

Time to classify this data:

**Qualitative data**:
* Ordinal
  * Survival
  * Sex 
  * Embarked
* Nominal 
  * Cabin
  * Name

**Quantitative data**:
* Discrete
  * Nominal
    * Passanger ID
    * Age
  * Ordinal
    * Survived
    * Pclass
    * Parch
    * Sibsp
* Continuos
    * Fare


#### 3️⃣ Preprocess Data 

FINALLYYYYYYYYYYYYYY, LET'S CODE! 

But, first... why preprocess and analyze are together? 

As you see in the holistic view of my process, this section is a "loop". We can't analysis data in a bad "shape" and we can't understand data if we don't analyzed it. 

WE NEED Exploration and Preparation! Data isn't perfect, our data needs to be prepared, analyzed and crafted for modeling.

1. There are inappropriate data types
2. The are missing values
3. The are values that need to be transform, grouped, etc.

At this point, we know what type of data we have. It's time to upload and fix the data. In R, data is different from the statistics standard. 

We have data types are: 
  * character
  * numeric 
  * integer 
  * complex 
  * logical

And data structures:
  * vector 
  * list
  * matrix 
  * data frame 
  * factors

Sometimes, we need to transform our dat but first we need to check data structure!

```r
str(train)
'data.frame':	891 obs. of  12 variables:
 $ PassengerId: int  1 2 3 4 5 6 7 8 9 10 ...
 $ Survived   : int  0 1 1 1 0 0 0 0 1 1 ...
 $ Pclass     : int  3 1 3 1 3 3 1 3 3 2 ...
 $ Name       : chr  "Braund, Mr. Owen Harris" "Cumings, Mrs. John Bradley (Florence Briggs Thayer)" "Heikkinen, Miss. Laina" "Futrelle, Mrs. Jacques Heath (Lily May Peel)" ...
 $ Sex        : chr  "male" "female" "female" "female" ...
 $ Age        : num  22 38 26 35 35 NA 54 2 27 14 ...
 $ SibSp      : int  1 1 0 1 0 0 0 3 0 1 ...
 $ Parch      : int  0 0 0 0 0 0 0 1 2 0 ...
 $ Ticket     : chr  "A/5 21171" "PC 17599" "STON/O2. 3101282" "113803" ...
 $ Fare       : num  7.25 71.28 7.92 53.1 8.05 ...
 $ Cabin      : chr  "" "C85" "" "C123" ...
 $ Embarked   : chr  "S" "C" "S" "S" ...
```

```r
str(test)
'data.frame':	418 obs. of  11 variables:
 $ PassengerId: int  892 893 894 895 896 897 898 899 900 901 ...
 $ Pclass     : int  3 3 2 3 3 3 3 2 3 3 ...
 $ Name       : chr  "Kelly, Mr. James" "Wilkes, Mrs. James (Ellen Needs)" "Myles, Mr. Thomas Francis" "Wirz, Mr. Albert" ...
 $ Sex        : chr  "male" "female" "male" "male" ...
 $ Age        : num  34.5 47 62 27 22 14 30 26 18 21 ...
 $ SibSp      : int  0 1 0 0 1 0 0 1 0 2 ...
 $ Parch      : int  0 0 0 0 1 0 0 1 0 0 ...
 $ Ticket     : chr  "330911" "363272" "240276" "315154" ...
 $ Fare       : num  7.83 7 9.69 8.66 12.29 ...
 $ Cabin      : chr  "" "" "" "" ...
 $ Embarked   : chr  "Q" "S" "Q" "S" ...
```

**As we see, we need to make some changes. 
Specially in Survived, Sex, Pclass and Embarked variables.** 

```r
train$Survived <- as.factor(train$Survived)
train$Embarked <- as.factor(train$Embarked)
train$Sex <- as.factor(train$Sex)
train$Pclass <- as.factor(train$Pclass)


test$Embarked <- as.factor(test$Embarked)
test$Sex <- as.factor(test$Sex)
test$Pclass <- as.factor(test$Pclass)
```

```r
str(test)
'data.frame':	418 obs. of  11 variables:
 $ PassengerId: int  892 893 894 895 896 897 898 899 900 901 ...
 $ Pclass     : Factor w/ 3 levels "1","2","3": 3 3 2 3 3 3 3 2 3 3 ...
 $ Name       : chr  "Kelly, Mr. James" "Wilkes, Mrs. James (Ellen Needs)" "Myles, Mr. Thomas Francis" "Wirz, Mr. Albert" ...
 $ Sex        : Factor w/ 2 levels "female","male": 2 1 2 2 1 2 1 2 1 2 ...
 $ Age        : num  34.5 47 62 27 22 14 30 26 18 21 ...
 $ SibSp      : int  0 1 0 0 1 0 0 1 0 2 ...
 $ Parch      : int  0 0 0 0 1 0 0 1 0 0 ...
 $ Ticket     : chr  "330911" "363272" "240276" "315154" ...
 $ Fare       : num  7.83 7 9.69 8.66 12.29 ...
 $ Cabin      : chr  "" "" "" "" ...
 $ Embarked   : Factor w/ 3 levels "C","Q","S": 2 3 2 3 3 3 2 3 1 3 ...
 ```

 ```r
str(train)
'data.frame':	891 obs. of  12 variables:
 $ PassengerId: int  1 2 3 4 5 6 7 8 9 10 ...
 $ Survived   : Factor w/ 2 levels "0","1": 1 2 2 2 1 1 1 1 2 2 ...
 $ Pclass     : Factor w/ 3 levels "1","2","3": 3 1 3 1 3 3 1 3 3 2 ...
 $ Name       : chr  "Braund, Mr. Owen Harris" "Cumings, Mrs. John Bradley (Florence Briggs Thayer)" "Heikkinen, Miss. Laina" "Futrelle, Mrs. Jacques Heath (Lily May Peel)" ...
 $ Sex        : Factor w/ 2 levels "female","male": 2 1 1 1 2 2 2 2 1 1 ...
 $ Age        : num  22 38 26 35 35 NA 54 2 27 14 ...
 $ SibSp      : int  1 1 0 1 0 0 0 3 0 1 ...
 $ Parch      : int  0 0 0 0 0 0 0 1 2 0 ...
 $ Ticket     : chr  "A/5 21171" "PC 17599" "STON/O2. 3101282" "113803" ...
 $ Fare       : num  7.25 71.28 7.92 53.1 8.05 ...
 $ Cabin      : chr  "" "C85" "" "C123" ...
 $ Embarked   : Factor w/ 4 levels "","C","Q","S": 4 2 4 4 4 3 4 4 4 2 
 ```

##### Done

Now is time to drop NA values, bind our data and create the file.

``` r
test <- data.frame(test[1], Survived = rep("NA", nrow(test)), test[ , 2:ncol(test)])
```

```r
data <- rbind(train, test)
```

```r
write.csv(data, "./data/interim/data.cvs", row.names = FALSE )
```

##### Structure looks great! 

```r
str(data)
'data.frame':	1309 obs. of  12 variables:
 $ PassengerId: int  1 2 3 4 5 6 7 8 9 10 ...
 $ Survived   : Factor w/ 3 levels "0","1","NA": 1 2 2 2 1 1 1 1 2 2 ...
 $ Pclass     : Factor w/ 3 levels "1","2","3": 3 1 3 1 3 3 1 3 3 2 ...
 $ Name       : chr  "Braund, Mr. Owen Harris" "Cumings, Mrs. John Bradley (Florence Briggs Thayer)" "Heikkinen, Miss. Laina" "Futrelle, Mrs. Jacques Heath (Lily May Peel)" ...
 $ Sex        : Factor w/ 2 levels "female","male": 2 1 1 1 2 2 2 2 1 1 ...
 $ Age        : num  22 38 26 35 35 NA 54 2 27 14 ...
 $ SibSp      : int  1 1 0 1 0 0 0 3 0 1 ...
 $ Parch      : int  0 0 0 0 0 0 0 1 2 0 ...
 $ Ticket     : chr  "A/5 21171" "PC 17599" "STON/O2. 3101282" "113803" ...
 $ Fare       : num  7.25 71.28 7.92 53.1 8.05 ...
 $ Cabin      : chr  "" "C85" "" "C123" ...
 $ Embarked   : Factor w/ 4 levels "","C","Q","S": 4 2 4 4 4 3 4 4 4 2
```

#### 4️⃣ Analyze Data

A tip for analyze data it's so see the path between dependices of variables. 

![Dependencies](img/../../img/data%20analysis/dependencies.png)

For example, we can count our Sex variable for the porpuse of see the proportion of gender.

```r
ggplot(data, 
       aes(x = Sex,
           y = ..count.. / sum(..count..))) + 
  geom_bar(fill = "cornflowerblue", 
           color="black") +
  labs(x = "Gender", 
       y = "Percent", 
       title = "Proportion of gender",
       subtitle = "") +
  scale_y_continuous(labels = scales::percent) +
  theme_base()
```

![Countsex](/img/data%20analysis/count.png)


We can see the proportion of socio-economic class among sex 

```r
ggplot(data, aes(x = Sex, fill = Pclass)) +
  geom_bar(color = "black", 
           position = position_dodge
           (preserve = "single")) +
  labs(x = "Gender",
       y = "Count",
       title = "Passenger socio-economic class",
       subtitle = "Distribution per gender") +
  theme_base()
```

![Countsex](/img/data%20analysis/countpclass.png)




