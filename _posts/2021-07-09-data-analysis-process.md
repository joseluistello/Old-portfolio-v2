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

#### Understand problem

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

#### Understand Data

> “The combination of some data and an aching desire for an answer does not ensure that a reasonable answer can be extracted from a given body of data.” **John Tukey**


| Variable | Definition | Key |
|-----------|----------|-----------|
|Survival|Survival |0 = No, 1 = Yes|
|Pclass|Ticket class |	1 = 1st, 2 = 2nd, 3 = 3rd |
|Sex    |	Sex| 	
|Age    |	Age in years| 	
|Sibsp  |	# of siblings / spouses aboard the Titanic| 	
|Parch  |# of parents / children aboard the Titanic |
|Ticket |	Ticket number 	|
|Fare   |	Passenger fare 	|
|Cabin  |	Cabin number |
|Embarked   |	Port of Embarkation |   C = Cherbourg, Q = Queenstown, S = Southampton  |

![Notes](/img/data%20analysis/notes.png)





##### 💡 Remember 💡 

👉🏼 *Use this process as a framework* 👈🏼 

#### If you want to see more of my work, check this out:

#### 📕 Latest Blog Posts and Projects

<!-- BLOG-POST-LIST:START -->
- [Definiendo el valor y la estructura de precios](https://joseluistello.substack.com/p/valor-y-estructura-de-precios)
- [Estructura de costos](https://joseluistello.substack.com/p/estructura-de-costos)
- [Fijación de precios](https://joseluistello.substack.com/p/fijacin-de-precios)
- [An Introduction to Forecasting Modeling](https://joseluistello.github.io/r/forecasting_mexico_GDPPC/)
- [Semiconductor Market Analysis](https://joseluistello.github.io/r/semiconductors-part1/)

<!-- BLOG-POST-LIST:END -->

#### Connect with me:

#### [🔥 Substack ](https://joseluistello.substack.com/)
#### [✔️ Twitter](https://twitter.com/jotaele_tello)
#### [😊 Linkedin](https://www.linkedin.com/in/joseluistello/)
#### [📈 Resume](https://www.notion.so/joseluistello/resume-908176d50910492f82bb0c2c50150406)
#### [❤️ DataBase](https://www.notion.so/joseluistello/resources-3b96a11183d342b889c95e9bcb1e0c7f)

---
