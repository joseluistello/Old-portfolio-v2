---
layout: post
title: "Working with API Rest and JSON"
subtitle: "Financial Analysis x10 Faster"
background: '/img/financial_api/fondo2.png'
output: html_document
date: 2021-09-04 19 -0400
category: Python
tags: [API, financial analysis, python, pandas, matplotlib]
comments: true
---

#### ¡Bienvenido de nuevo! 👋  


En esta ocasión vamos a trabajar con una [API Financiera](https://financialmodelingprep.com/developer/docs)

Hice este proyecto para enseñar una manera rapida de analizar cuantitativamente a las empresas. El ultimo año estuve aprendiendo finanzas y desarrollando modelos financieros, podria decirse que soy un "hobbyista" de las finanzas.

![png](/img/financial_api/modelo1.png)

![png](/img/financial_api/modelo2.png)

![png](/img/financial_api/modelo3.png)

![png](/img/financial_api/modelo4.png)

Se el dolor y el amor que podemos experimentar al crear modelos financieros. Buscar dentro de un reporte anual K10  y pasar datos a mano es un proceso lento y lleno de fricciones. Por eso hice este proyecto, esta es mi propuesta para agilizar la recolección de datos financieros. 

En este proyecto aprenderas sobre:

1. Que son las API 
2. Que es REST
3. Que es HTTP
4. Como extraer datos de una API
5. Transformar los datos de JSON de una API a un dataframe de Pandas
6. Como graficar los datos con Matplotlib y Numpy
7. Como guardar los datos dentro de un CSV para que los manipules con en Excel, R u otra herramienta de tu agrado

--- 

#### ¿Que es una API?

Una API es una interfaz que ofrece un servicio de comunicación. A diferencia de una UI (interfaz de usuario) que conecta a una persona con una computadora, una API conecta computadoras o software entre ellos mismos.

Estan hechas de diferentes partes que actuan como herramientas o servicios. Un programador puede llamar a uno de estos servicios a traves de metodos, requests o endpoints los cuales estan definidos en las espicificaciones de una API. 

#### ¿Que es REST? 

REST fue propuesto por Roy Thomas en un paper titulado " Architectural Styles and the Design of Network-based Software Architectures". REST es un tipo de diseño/arquitectura al que se puede someter una API. Una de las ideas detras de REST es ver a los datos como objetos que puedes llamar, crear o destruir a través de metodos y que son representados en formato JSON, XML o RDF. 

| Metodo | Descripcion |
| ----------- | ----------- |
| GET | Trae informacion  |
| POST | Crea informacion | 
| PUT | Actualiza informacion |
| DELETE | Borra informacion | 

[Como explicarle REST a tu esposa](http://www.looah.com/source/view/2284)

Esto es justo lo que haremos ahora. Imaginemos a una API de arquitectura tipo REST como un ente que nos ayuda a traer datos desde una base externa. Nuestra computadora necesita comunicarse con otra y una API REST es la mejor forma de hacerlo. Para ello, utilizaremos el modulo **requests** de Python donde podemos enviar pedimentos HTTP de manera sencilla. 

Pero, ¿que es HTTP?

HTTP o Hypertext Transfer Protocol es un protocolo Request-Response (pedido y respuesta) cuya funcion principal es establecer una comunicación entre sistemas de la Internet que conforman el World Wide Web (WWW).

Fue creado para actuar como un puente entre los clientes y servidores. Este "puente" tiene metodos definidos que indican acciones *deseadas* por parte de un cliente hacia un recurso especifico. Lo que el recurso represente depende de lo que se implemento en el servidor. Basicamente REST es la manera en que HTTP se debe usar.

#### Extrayendo datos de una API

Hay 3 reglas que se deben seguir para usar una API REST.
1. Definir el metodo
2. Definir los parametros
3. Hacer el request

Nuestro metodo sera de tipo GET que es lo mismo que pedir informacion de la API.

Nuestros parametros seran:
1. La llave de la API (la puedes conseguir [creando una cuenta](https://financialmodelingprep.com/register) en el portal de la API) 
2. El ticket en la bolsa de la empresa de nuestro interes
3. Los años

En esta ocasion haremos un request de datos financieros del Income Statement de NVDA. 

```python
import requests 
import json
```

```python
# DEFINIENDO PARAMETROS #
api_key = 'Ingresa_tu_apikey_aqui'
company = "NVDA"
years = 5
```

Si lo que quieres es su Balance Sheet o Cash Flow solo cambia esto la parte de income-statement en la URL por balance-sheet o cash-flow

```python
# REQUEST GET  con el package Requests.
r = requests.get(f'https://financialmodelingprep.com/api/v3/income-statement/{company}?limit={years}&apikey={api_key}')
data = r.json()
print(data)
# CON ESTO CREAMOS UN OBJETO de datos tipo lista.
```

    [{'date': '2021-01-31', 'symbol': 'NVDA', 'reportedCurrency': 'USD', 'fillingDate': '2021-02-26', 'acceptedDate': '2021-02-26 17:03:14', 'period': 'FY', 'revenue': 16675000000, 'costOfRevenue': 6279000000, 'grossProfit': 10396000000, 'grossProfitRatio': 0.623448275862069, 'researchAndDevelopmentExpenses': 3924000000, 'generalAndAdministrativeExpenses': 0.0, 'sellingAndMarketingExpenses': 0.0, 'sellingGeneralAndAdministrativeExpenses': 1940000000, 'otherExpenses': 0.0, 'operatingExpenses': 5864000000, 'costAndExpenses': 12143000000, 'interestExpense': 184000000, 'depreciationAndAmortization': 1098000000, 'ebitda': 5691000000, 'ebitdaratio': 0.34128935532233884, 'operatingIncome': 4532000000, 'operatingIncomeRatio': 0.271784107946027, 'totalOtherIncomeExpensesNet': 123000000, 'incomeBeforeTax': 4409000000, 'incomeBeforeTaxRatio': 0.26440779610194903, 'incomeTaxExpense': 77000000, 'netIncome': 4332000000, 'netIncomeRatio': 0.25979010494752625, 'eps': 1.7245222929936306, 'epsdiluted': 1.7245222929936306, 'weightedAverageShsOut': 2468000000, 'weightedAverageShsOutDil': 2512000000, 'link': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581021000010/0001045810-21-000010-index.htm', 'finalLink': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581021000010/nvda-20210131.htm'}, {'date': '2020-01-26', 'symbol': 'NVDA', 'reportedCurrency': 'USD', 'fillingDate': '2020-02-20 00:00:00', 'acceptedDate': '2020-02-20 16:38:18', 'period': 'FY', 'revenue': 10918000000, 'costOfRevenue': 4150000000, 'grossProfit': 6768000000, 'grossProfitRatio': 0.619893753434695, 'researchAndDevelopmentExpenses': 2829000000, 'generalAndAdministrativeExpenses': 1093000000, 'sellingAndMarketingExpenses': 0.0, 'sellingGeneralAndAdministrativeExpenses': 1093000000, 'otherExpenses': 0.0, 'operatingExpenses': 3922000000, 'costAndExpenses': 8072000000, 'interestExpense': 52000000, 'depreciationAndAmortization': 381000000, 'ebitda': 3403000000, 'ebitdaratio': 0.3116871221835501, 'operatingIncome': 2846000000, 'operatingIncomeRatio': 0.2606704524638212, 'totalOtherIncomeExpensesNet': -124000000, 'incomeBeforeTax': 2970000000, 'incomeBeforeTaxRatio': 0.27202784392745927, 'incomeTaxExpense': 174000000, 'netIncome': 2796000000, 'netIncomeRatio': 0.2560908591317091, 'eps': 1.1310679611650485, 'epsdiluted': 1.1310679611650485, 'weightedAverageShsOut': 2472000000, 'weightedAverageShsOutDil': 2472000000, 'link': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581020000010/0001045810-20-000010-index.html', 'finalLink': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581020000010/nvda-2020x10k.htm'}, {'date': '2019-01-27', 'symbol': 'NVDA', 'reportedCurrency': 'USD', 'fillingDate': '2019-02-21 00:00:00', 'acceptedDate': '2019-02-21 16:37:18', 'period': 'FY', 'revenue': 11716000000, 'costOfRevenue': 4545000000, 'grossProfit': 7171000000, 'grossProfitRatio': 0.6120689655172413, 'researchAndDevelopmentExpenses': 2376000000, 'generalAndAdministrativeExpenses': 991000000, 'sellingAndMarketingExpenses': 0.0, 'sellingGeneralAndAdministrativeExpenses': 991000000, 'otherExpenses': 0.0, 'operatingExpenses': 3367000000, 'costAndExpenses': 7912000000, 'interestExpense': 58000000, 'depreciationAndAmortization': 262000000, 'ebitda': 4584000000, 'ebitdaratio': 0.39125981563673606, 'operatingIncome': 3804000000, 'operatingIncomeRatio': 0.3246841925571868, 'totalOtherIncomeExpensesNet': -92000000, 'incomeBeforeTax': 3896000000, 'incomeBeforeTaxRatio': 0.33253670194605667, 'incomeTaxExpense': 123000000, 'netIncome': 4141000000, 'netIncomeRatio': 0.35344827586206895, 'eps': 1.6564, 'epsdiluted': 1.6564, 'weightedAverageShsOut': 2500000000, 'weightedAverageShsOutDil': 2500000000, 'link': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581019000023/0001045810-19-000023-index.html', 'finalLink': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581019000023/nvda-2019x10k.htm'}, {'date': '2018-01-28', 'symbol': 'NVDA', 'reportedCurrency': 'USD', 'fillingDate': '2018-02-28 00:00:00', 'acceptedDate': '2018-02-28 16:31:19', 'period': 'FY', 'revenue': 9714000000, 'costOfRevenue': 3892000000, 'grossProfit': 5822000000, 'grossProfitRatio': 0.5993411570928556, 'researchAndDevelopmentExpenses': 1797000000, 'generalAndAdministrativeExpenses': 815000000, 'sellingAndMarketingExpenses': 0.0, 'sellingGeneralAndAdministrativeExpenses': 815000000, 'otherExpenses': 0.0, 'operatingExpenses': 2612000000, 'costAndExpenses': 6504000000, 'interestExpense': 61000000, 'depreciationAndAmortization': 199000000, 'ebitda': 3589000000, 'ebitdaratio': 0.3694667490220301, 'operatingIncome': 3210000000, 'operatingIncomeRatio': 0.3304508956145769, 'totalOtherIncomeExpensesNet': 14000000, 'incomeBeforeTax': 3196000000, 'incomeBeforeTaxRatio': 0.3290096767551987, 'incomeTaxExpense': 282000000, 'netIncome': 3047000000, 'netIncomeRatio': 0.3136709903232448, 'eps': 1.2053006329113924, 'epsdiluted': 1.2053006329113924, 'weightedAverageShsOut': 2528000000, 'weightedAverageShsOutDil': 2528000000, 'link': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581018000010/0001045810-18-000010-index.html', 'finalLink': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581018000010/nvda-2018x10k.htm'}, {'date': '2017-01-29', 'symbol': 'NVDA', 'reportedCurrency': 'USD', 'fillingDate': '2017-03-01 00:00:00', 'acceptedDate': '2017-03-01 17:30:49', 'period': 'FY', 'revenue': 6910000000, 'costOfRevenue': 2847000000, 'grossProfit': 4063000000, 'grossProfitRatio': 0.5879884225759768, 'researchAndDevelopmentExpenses': 1463000000, 'generalAndAdministrativeExpenses': 663000000, 'sellingAndMarketingExpenses': 0.0, 'sellingGeneralAndAdministrativeExpenses': 666000000, 'otherExpenses': 0.0, 'operatingExpenses': 2129000000, 'costAndExpenses': 4976000000, 'interestExpense': 58000000, 'depreciationAndAmortization': 187000000, 'ebitda': 2150000000, 'ebitdaratio': 0.3111432706222865, 'operatingIncome': 1934000000, 'operatingIncomeRatio': 0.27988422575976846, 'totalOtherIncomeExpensesNet': 29000000, 'incomeBeforeTax': 1905000000, 'incomeBeforeTaxRatio': 0.27568740955137483, 'incomeTaxExpense': 239000000, 'netIncome': 1666000000, 'netIncomeRatio': 0.2410998552821997, 'eps': 0.6417565485362096, 'epsdiluted': 0.6417565485362096, 'weightedAverageShsOut': 2596000000, 'weightedAverageShsOutDil': 2596000000, 'link': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581017000027/0001045810-17-000027-index.html', 'finalLink': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581017000027/nvda-2017x10k.htm'}]
    

#### Transformando los datos JSON a un DF

Trabajar con un JSON no es recomendable pues es dificil manipularlo, al final del día fueron creados para enviar y recibir información entre servidores pero no para ser analizados. Contrario a esto, Pandas nos permite transformarlos de una manera super sencilla a un Dataframe con el siguiente codigo.

Primero importamos pandas. 

```python
import pandas as pd
```

Y despues escribimos este pedazo de codigo.

```python
df = pd.DataFrame(data)
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 5 entries, 0 to 4
    Data columns (total 35 columns):
     #   Column                                   Non-Null Count  Dtype  
    ---  ------                                   --------------  -----  
     0   date                                     5 non-null      object 
     1   symbol                                   5 non-null      object 
     2   reportedCurrency                         5 non-null      object 
     3   fillingDate                              5 non-null      object 
     4   acceptedDate                             5 non-null      object 
     5   period                                   5 non-null      object 
     6   revenue                                  5 non-null      int64  
     7   costOfRevenue                            5 non-null      int64  
     8   grossProfit                              5 non-null      int64  
     9   grossProfitRatio                         5 non-null      float64
     10  researchAndDevelopmentExpenses           5 non-null      int64  
     11  generalAndAdministrativeExpenses         5 non-null      float64
     12  sellingAndMarketingExpenses              5 non-null      float64
     13  sellingGeneralAndAdministrativeExpenses  5 non-null      int64  
     14  otherExpenses                            5 non-null      float64
     15  operatingExpenses                        5 non-null      int64  
     16  costAndExpenses                          5 non-null      int64  
     17  interestExpense                          5 non-null      int64  
     18  depreciationAndAmortization              5 non-null      int64  
     19  ebitda                                   5 non-null      int64  
     20  ebitdaratio                              5 non-null      float64
     21  operatingIncome                          5 non-null      int64  
     22  operatingIncomeRatio                     5 non-null      float64
     23  totalOtherIncomeExpensesNet              5 non-null      int64  
     24  incomeBeforeTax                          5 non-null      int64  
     25  incomeBeforeTaxRatio                     5 non-null      float64
     26  incomeTaxExpense                         5 non-null      int64  
     27  netIncome                                5 non-null      int64  
     28  netIncomeRatio                           5 non-null      float64
     29  eps                                      5 non-null      float64
     30  epsdiluted                               5 non-null      float64
     31  weightedAverageShsOut                    5 non-null      int64  
     32  weightedAverageShsOutDil                 5 non-null      int64  
     33  link                                     5 non-null      object 
     34  finalLink                                5 non-null      object 
    dtypes: float64(10), int64(17), object(8)
    memory usage: 1.5+ KB
    

Listo. Los datos vienen sin valores nulos y estan en buen estado así que podemos analizarlos a partir de ahora. 
Lo unico que hare es quitar quitar algunas columnas como los ratios, pero no es necesario que tu lo hagas si no quieres. 

Lo que si es necesario es que apliques un SORT. Esto te permite cambiar el orden del frame a partir de sus fechas, pues si lo graficos de esta manera los plots te saldran invertidos.

Con esto dropeamos o eliminalos las columnas.

```python
df = df.drop(columns=['reportedCurrency', 
                      'fillingDate', 
                      'acceptedDate', 
                      'period', 
                      'link', 
                      'finalLink', 
                      'symbol', 
                      'grossProfitRatio', 
                      'incomeBeforeTaxRatio', 
                      'netIncomeRatio', 
                      'eps', 
                      'epsdiluted'])
```

Y con esto volteamos el frame.

```python
df = df.sort_values("date")
```

#### Graficando los datos

Ahora que transformamos y limpiamos los datos, es hora de hacer algunos plots para mostrarte lo facil que es graficar el frame.

1. Primero cargare las librerias 
2. Despues aplicare una configuración para el tamaño de los plots
3. Por ultimo dividire las columnas de mi interes para que el axis de Y no arroje visualizaciones raras jaja.


```python
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns
```

```python
### Este codigo establece la anchura y la altura de los plots (bastante util) 
%matplotlib inline
plt.rcParams['figure.figsize'] = (12, 10)
```

Utilizare las ventas de la compañia y los costes de las ventas como comparación a través de los 5 años. 


```python
## Este codigo te permite seleccionar las columnas de tu interes con el proposito
## de dividirlas y mejorar la visualización del plot
df[["revenue", "costOfRevenue"]] = df[["revenue", "costOfRevenue"]] / 1000000000
```


```python
plt.bar(df['date'], df['revenue'])
plt.title('Crecimiento en las ventas de NVDA', fontsize=14)
plt.xlabel('Año', fontsize=14)
plt.ylabel('Ventas totales en miles de millones de USD', fontsize=14)
plt.xticks(df['date'],['2017', '2018', '2019', '2020', '2021'])
plt.show()
```


    
![png](/img/financial_api/output1.png)
    



```python
### Localizando los datos

descripcion = ['2017', '2018', '2019', '2020', '2021']
revenue = df["revenue"]
costOfRevenue = df["costOfRevenue"]

### Recorriendo la descripcion

x = np.arange(len(descripcion)) 
width = 0.35  

### Configurando los plots

fig, ax = plt.subplots()
plot1 = ax.bar(x - width/2, revenue, width, label='Ventas')
plot2 = ax.bar(x + width/2, costOfRevenue, width, label='Costo de ventas')

### Añadiendo la descripcion
ax.set_ylabel('Miles de millones de USD')
ax.set_title('Revenue vs CostOfRevenue')
ax.set_xticks(x)
ax.set_xticklabels(descripcion)
ax.legend()


plt.show()
```


    
![png](/img/financial_api/output2.png)
    


#### Creando un csv

Si lo anterior te parecio dificil, no te preocupes. Siempre existen soluciones y de hecho me parece que utilizar Python para este tipo de cosas (visualizar frames tan pequeños) es innecesario. Para eso tenemos Excel.

Con el siguiente pedazo de codigo vas a poder crear un csv con los datos que sacaste del API. 


```python
### Al indicar index = False eliminas las enumeraciones de cada fila. 
df.to_csv('NVDA.csv', index = False)
```

 

Bueno, esto es todo! Espero que este proyecto te ayude con tus objetivos profesionales y no profesionales. Si necesitas ayuda siempre puedes mandarme un mensaje a joluistello@gmail.com. 

Un abrazo!


```python

```


