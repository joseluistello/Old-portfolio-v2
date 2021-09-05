---
layout: post
title: "Working with API Rest and JSON"
subtitle: "Financial analysis x10 faster"
background: '/img/ecommerce/fondo3.png'
output: html_document
date: 2021-09-04 19 -0400
category: Python
tags: [API, financial analysis, python, pandas, matplotlib]
comments: true
---



¡Holaaaaaa! 

En esta ocasión vamos a trabajar con una [API Financiera](https://financialmodelingprep.com/developer/docs)

La razón detras de este proyecto es que quiero mostrarles una manera rapida de analizar empresas desde el lado cuantitativo/descriptivo. He pasado el ultimo año desarrollando modelos financieros, soy un "hobbyista" de las finanzas. Siempre me interesaron las finanzas corporativas y valuaciones de empresas como un mero pasamiento. 


```python
Pero primero, ¿que es una API?

Una API es una interfaz que ofrece un servicio de comunicación. A diferencia de una UI (interfaz de usuario) que conecta a una persona con una computadora, una API conecta computadoras o software entre ellos mismos.

Estan hechas de diferentes partes que actuan como herramientas o servicios. Un programador puede llamar a uno de estos servicios a traves de metodos, requests o endpoints que estan definidas en las espicificaciones de una API. 

Pero la API como tal no es practica de usar, debe diseñarse a través de una arquitectura llamada REST que ayuda a manejar la información. 

REST fue propuesta por Roy Thomas en un paper titulado " Architectural Styles and the Design of Network-based Software Architectures", y una idea basica detras de REST es tratar a los datos como objetos que puedes llamar, crear o destruir y a través de metodos y que son representados en formato JSON, XML o RDF. 

| Metodo | Descripcion |
| ----------- | ----------- |
| GET | Trae informacion  |
| POST | Crea informacion | 
| PUT | Actualiza informacion |
| DELETE | Borra informacion | 

[Como explicarle REST a tu esposa](http://www.looah.com/source/view/2284)


Esto es justo lo que haremos ahora. Imaginemos a una API Rest como un ente que nos ayuda a traer datos desde una base externa. Nuestra computadora necesita comunicarse con otra y REST es la mejor forma de hacerlo.

¡Es hora de empezar!

```


```python
import requests 
import json
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import seaborn as sns
```

Utilizaremos el modulo **requests** para enviar pedimentos HTTP de manera sencilla. 

HTTP o Hypertext Transfer Protocol es un protocolo Request-Response (pedido y respuesta) cuya funcion principal es establecer una comunicación entre sistemas de la Internet que conforman el World Wide Web (WWW).

Fue diseñado y creado para ser un puente entre los clientes y servidores. Este "puente" tiene metodos definidos que indican acciones deseadas por parte de un cliente hacia un recurso especifico. Lo que el recurso represente depende de lo que se implemento en el servidor. 

Basicamente REST es la manera en que HTTP se debe usar.


Hay 3 reglas que se deben seguir para usar una API REST.
      1. Definir el metodo
      2. Definir los parametros
      3. Hacer el request

Definiendo los dos primeros obtienes una respuesta especifica del servidor. Entonces, lo que yo quiero hacer es implementar un metodo GET para OBTENER datos.


```python
# Estos son los parametros que necesita la API para entender lo que quieres
api_key = '27ae1dd809036202bcf78ee64609eb76'
company = "NVDA"
years = 5

# Y estes es el request que se logra hacer de manera sencilla gracias al package Requests.
r = requests.get(f'https://financialmodelingprep.com/api/v3/income-statement/{company}?limit={years}&apikey={api_key}')
data = r.json()
data
# Con esto obtenemos una respuesta con una estructura de tipo LISTA con formato JSON desde el servidor.
```




    [{'date': '2021-01-31',
      'symbol': 'NVDA',
      'reportedCurrency': 'USD',
      'fillingDate': '2021-02-26',
      'acceptedDate': '2021-02-26 17:03:14',
      'period': 'FY',
      'revenue': 16675000000,
      'costOfRevenue': 6279000000,
      'grossProfit': 10396000000,
      'grossProfitRatio': 0.623448275862069,
      'researchAndDevelopmentExpenses': 3924000000,
      'generalAndAdministrativeExpenses': 0.0,
      'sellingAndMarketingExpenses': 0.0,
      'sellingGeneralAndAdministrativeExpenses': 1940000000,
      'otherExpenses': 0.0,
      'operatingExpenses': 5864000000,
      'costAndExpenses': 12143000000,
      'interestExpense': 184000000,
      'depreciationAndAmortization': 1098000000,
      'ebitda': 5691000000,
      'ebitdaratio': 0.34128935532233884,
      'operatingIncome': 4532000000,
      'operatingIncomeRatio': 0.271784107946027,
      'totalOtherIncomeExpensesNet': 123000000,
      'incomeBeforeTax': 4409000000,
      'incomeBeforeTaxRatio': 0.26440779610194903,
      'incomeTaxExpense': 77000000,
      'netIncome': 4332000000,
      'netIncomeRatio': 0.25979010494752625,
      'eps': 1.7245222929936306,
      'epsdiluted': 1.7245222929936306,
      'weightedAverageShsOut': 2468000000,
      'weightedAverageShsOutDil': 2512000000,
      'link': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581021000010/0001045810-21-000010-index.htm',
      'finalLink': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581021000010/nvda-20210131.htm'},
     {'date': '2020-01-26',
      'symbol': 'NVDA',
      'reportedCurrency': 'USD',
      'fillingDate': '2020-02-20 00:00:00',
      'acceptedDate': '2020-02-20 16:38:18',
      'period': 'FY',
      'revenue': 10918000000,
      'costOfRevenue': 4150000000,
      'grossProfit': 6768000000,
      'grossProfitRatio': 0.619893753434695,
      'researchAndDevelopmentExpenses': 2829000000,
      'generalAndAdministrativeExpenses': 1093000000,
      'sellingAndMarketingExpenses': 0.0,
      'sellingGeneralAndAdministrativeExpenses': 1093000000,
      'otherExpenses': 0.0,
      'operatingExpenses': 3922000000,
      'costAndExpenses': 8072000000,
      'interestExpense': 52000000,
      'depreciationAndAmortization': 381000000,
      'ebitda': 3403000000,
      'ebitdaratio': 0.3116871221835501,
      'operatingIncome': 2846000000,
      'operatingIncomeRatio': 0.2606704524638212,
      'totalOtherIncomeExpensesNet': -124000000,
      'incomeBeforeTax': 2970000000,
      'incomeBeforeTaxRatio': 0.27202784392745927,
      'incomeTaxExpense': 174000000,
      'netIncome': 2796000000,
      'netIncomeRatio': 0.2560908591317091,
      'eps': 1.1310679611650485,
      'epsdiluted': 1.1310679611650485,
      'weightedAverageShsOut': 2472000000,
      'weightedAverageShsOutDil': 2472000000,
      'link': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581020000010/0001045810-20-000010-index.html',
      'finalLink': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581020000010/nvda-2020x10k.htm'},
     {'date': '2019-01-27',
      'symbol': 'NVDA',
      'reportedCurrency': 'USD',
      'fillingDate': '2019-02-21 00:00:00',
      'acceptedDate': '2019-02-21 16:37:18',
      'period': 'FY',
      'revenue': 11716000000,
      'costOfRevenue': 4545000000,
      'grossProfit': 7171000000,
      'grossProfitRatio': 0.6120689655172413,
      'researchAndDevelopmentExpenses': 2376000000,
      'generalAndAdministrativeExpenses': 991000000,
      'sellingAndMarketingExpenses': 0.0,
      'sellingGeneralAndAdministrativeExpenses': 991000000,
      'otherExpenses': 0.0,
      'operatingExpenses': 3367000000,
      'costAndExpenses': 7912000000,
      'interestExpense': 58000000,
      'depreciationAndAmortization': 262000000,
      'ebitda': 4584000000,
      'ebitdaratio': 0.39125981563673606,
      'operatingIncome': 3804000000,
      'operatingIncomeRatio': 0.3246841925571868,
      'totalOtherIncomeExpensesNet': -92000000,
      'incomeBeforeTax': 3896000000,
      'incomeBeforeTaxRatio': 0.33253670194605667,
      'incomeTaxExpense': 123000000,
      'netIncome': 4141000000,
      'netIncomeRatio': 0.35344827586206895,
      'eps': 1.6564,
      'epsdiluted': 1.6564,
      'weightedAverageShsOut': 2500000000,
      'weightedAverageShsOutDil': 2500000000,
      'link': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581019000023/0001045810-19-000023-index.html',
      'finalLink': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581019000023/nvda-2019x10k.htm'},
     {'date': '2018-01-28',
      'symbol': 'NVDA',
      'reportedCurrency': 'USD',
      'fillingDate': '2018-02-28 00:00:00',
      'acceptedDate': '2018-02-28 16:31:19',
      'period': 'FY',
      'revenue': 9714000000,
      'costOfRevenue': 3892000000,
      'grossProfit': 5822000000,
      'grossProfitRatio': 0.5993411570928556,
      'researchAndDevelopmentExpenses': 1797000000,
      'generalAndAdministrativeExpenses': 815000000,
      'sellingAndMarketingExpenses': 0.0,
      'sellingGeneralAndAdministrativeExpenses': 815000000,
      'otherExpenses': 0.0,
      'operatingExpenses': 2612000000,
      'costAndExpenses': 6504000000,
      'interestExpense': 61000000,
      'depreciationAndAmortization': 199000000,
      'ebitda': 3589000000,
      'ebitdaratio': 0.3694667490220301,
      'operatingIncome': 3210000000,
      'operatingIncomeRatio': 0.3304508956145769,
      'totalOtherIncomeExpensesNet': 14000000,
      'incomeBeforeTax': 3196000000,
      'incomeBeforeTaxRatio': 0.3290096767551987,
      'incomeTaxExpense': 282000000,
      'netIncome': 3047000000,
      'netIncomeRatio': 0.3136709903232448,
      'eps': 1.2053006329113924,
      'epsdiluted': 1.2053006329113924,
      'weightedAverageShsOut': 2528000000,
      'weightedAverageShsOutDil': 2528000000,
      'link': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581018000010/0001045810-18-000010-index.html',
      'finalLink': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581018000010/nvda-2018x10k.htm'},
     {'date': '2017-01-29',
      'symbol': 'NVDA',
      'reportedCurrency': 'USD',
      'fillingDate': '2017-03-01 00:00:00',
      'acceptedDate': '2017-03-01 17:30:49',
      'period': 'FY',
      'revenue': 6910000000,
      'costOfRevenue': 2847000000,
      'grossProfit': 4063000000,
      'grossProfitRatio': 0.5879884225759768,
      'researchAndDevelopmentExpenses': 1463000000,
      'generalAndAdministrativeExpenses': 663000000,
      'sellingAndMarketingExpenses': 0.0,
      'sellingGeneralAndAdministrativeExpenses': 666000000,
      'otherExpenses': 0.0,
      'operatingExpenses': 2129000000,
      'costAndExpenses': 4976000000,
      'interestExpense': 58000000,
      'depreciationAndAmortization': 187000000,
      'ebitda': 2150000000,
      'ebitdaratio': 0.3111432706222865,
      'operatingIncome': 1934000000,
      'operatingIncomeRatio': 0.27988422575976846,
      'totalOtherIncomeExpensesNet': 29000000,
      'incomeBeforeTax': 1905000000,
      'incomeBeforeTaxRatio': 0.27568740955137483,
      'incomeTaxExpense': 239000000,
      'netIncome': 1666000000,
      'netIncomeRatio': 0.2410998552821997,
      'eps': 0.6417565485362096,
      'epsdiluted': 0.6417565485362096,
      'weightedAverageShsOut': 2596000000,
      'weightedAverageShsOutDil': 2596000000,
      'link': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581017000027/0001045810-17-000027-index.html',
      'finalLink': 'https://www.sec.gov/Archives/edgar/data/1045810/000104581017000027/nvda-2017x10k.htm'}]



### Transformando y limpiando los datos

¡Pandas nos permite transformar JSONs de una manera super sencilla! 


```python
df = pd.DataFrame(data)
pd.DataFrame.from_records(df).head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>symbol</th>
      <th>reportedCurrency</th>
      <th>fillingDate</th>
      <th>acceptedDate</th>
      <th>period</th>
      <th>revenue</th>
      <th>costOfRevenue</th>
      <th>grossProfit</th>
      <th>grossProfitRatio</th>
      <th>...</th>
      <th>incomeBeforeTaxRatio</th>
      <th>incomeTaxExpense</th>
      <th>netIncome</th>
      <th>netIncomeRatio</th>
      <th>eps</th>
      <th>epsdiluted</th>
      <th>weightedAverageShsOut</th>
      <th>weightedAverageShsOutDil</th>
      <th>link</th>
      <th>finalLink</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2021-01-31</td>
      <td>NVDA</td>
      <td>USD</td>
      <td>2021-02-26</td>
      <td>2021-02-26 17:03:14</td>
      <td>FY</td>
      <td>16675000000</td>
      <td>6279000000</td>
      <td>10396000000</td>
      <td>0.623448</td>
      <td>...</td>
      <td>0.264408</td>
      <td>77000000</td>
      <td>4332000000</td>
      <td>0.259790</td>
      <td>1.724522</td>
      <td>1.724522</td>
      <td>2468000000</td>
      <td>2512000000</td>
      <td>https://www.sec.gov/Archives/edgar/data/104581...</td>
      <td>https://www.sec.gov/Archives/edgar/data/104581...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-26</td>
      <td>NVDA</td>
      <td>USD</td>
      <td>2020-02-20 00:00:00</td>
      <td>2020-02-20 16:38:18</td>
      <td>FY</td>
      <td>10918000000</td>
      <td>4150000000</td>
      <td>6768000000</td>
      <td>0.619894</td>
      <td>...</td>
      <td>0.272028</td>
      <td>174000000</td>
      <td>2796000000</td>
      <td>0.256091</td>
      <td>1.131068</td>
      <td>1.131068</td>
      <td>2472000000</td>
      <td>2472000000</td>
      <td>https://www.sec.gov/Archives/edgar/data/104581...</td>
      <td>https://www.sec.gov/Archives/edgar/data/104581...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2019-01-27</td>
      <td>NVDA</td>
      <td>USD</td>
      <td>2019-02-21 00:00:00</td>
      <td>2019-02-21 16:37:18</td>
      <td>FY</td>
      <td>11716000000</td>
      <td>4545000000</td>
      <td>7171000000</td>
      <td>0.612069</td>
      <td>...</td>
      <td>0.332537</td>
      <td>123000000</td>
      <td>4141000000</td>
      <td>0.353448</td>
      <td>1.656400</td>
      <td>1.656400</td>
      <td>2500000000</td>
      <td>2500000000</td>
      <td>https://www.sec.gov/Archives/edgar/data/104581...</td>
      <td>https://www.sec.gov/Archives/edgar/data/104581...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-01-28</td>
      <td>NVDA</td>
      <td>USD</td>
      <td>2018-02-28 00:00:00</td>
      <td>2018-02-28 16:31:19</td>
      <td>FY</td>
      <td>9714000000</td>
      <td>3892000000</td>
      <td>5822000000</td>
      <td>0.599341</td>
      <td>...</td>
      <td>0.329010</td>
      <td>282000000</td>
      <td>3047000000</td>
      <td>0.313671</td>
      <td>1.205301</td>
      <td>1.205301</td>
      <td>2528000000</td>
      <td>2528000000</td>
      <td>https://www.sec.gov/Archives/edgar/data/104581...</td>
      <td>https://www.sec.gov/Archives/edgar/data/104581...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-01-29</td>
      <td>NVDA</td>
      <td>USD</td>
      <td>2017-03-01 00:00:00</td>
      <td>2017-03-01 17:30:49</td>
      <td>FY</td>
      <td>6910000000</td>
      <td>2847000000</td>
      <td>4063000000</td>
      <td>0.587988</td>
      <td>...</td>
      <td>0.275687</td>
      <td>239000000</td>
      <td>1666000000</td>
      <td>0.241100</td>
      <td>0.641757</td>
      <td>0.641757</td>
      <td>2596000000</td>
      <td>2596000000</td>
      <td>https://www.sec.gov/Archives/edgar/data/104581...</td>
      <td>https://www.sec.gov/Archives/edgar/data/104581...</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 35 columns</p>
</div>



Ya tenemos nuestro dataframe. Es hora de quitar algunas columnas y buscar valores nulos.


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


```python
df.isnull().sum()
```




    date                                       0
    revenue                                    0
    costOfRevenue                              0
    grossProfit                                0
    researchAndDevelopmentExpenses             0
    generalAndAdministrativeExpenses           0
    sellingAndMarketingExpenses                0
    sellingGeneralAndAdministrativeExpenses    0
    otherExpenses                              0
    operatingExpenses                          0
    costAndExpenses                            0
    interestExpense                            0
    depreciationAndAmortization                0
    ebitda                                     0
    ebitdaratio                                0
    operatingIncome                            0
    operatingIncomeRatio                       0
    totalOtherIncomeExpensesNet                0
    incomeBeforeTax                            0
    incomeTaxExpense                           0
    netIncome                                  0
    weightedAverageShsOut                      0
    weightedAverageShsOutDil                   0
    dtype: int64




```python
df = df.sort_values("date")
```


```python
df[["revenue", "costOfRevenue"]] = df[["revenue", "costOfRevenue"]] / 1000000000
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>revenue</th>
      <th>costOfRevenue</th>
      <th>grossProfit</th>
      <th>researchAndDevelopmentExpenses</th>
      <th>generalAndAdministrativeExpenses</th>
      <th>sellingAndMarketingExpenses</th>
      <th>sellingGeneralAndAdministrativeExpenses</th>
      <th>otherExpenses</th>
      <th>operatingExpenses</th>
      <th>...</th>
      <th>ebitda</th>
      <th>ebitdaratio</th>
      <th>operatingIncome</th>
      <th>operatingIncomeRatio</th>
      <th>totalOtherIncomeExpensesNet</th>
      <th>incomeBeforeTax</th>
      <th>incomeTaxExpense</th>
      <th>netIncome</th>
      <th>weightedAverageShsOut</th>
      <th>weightedAverageShsOutDil</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>2017-01-29</td>
      <td>6.910</td>
      <td>2.847</td>
      <td>4063000000</td>
      <td>1463000000</td>
      <td>6.630000e+08</td>
      <td>0.0</td>
      <td>666000000</td>
      <td>0.0</td>
      <td>2129000000</td>
      <td>...</td>
      <td>2150000000</td>
      <td>0.311143</td>
      <td>1934000000</td>
      <td>0.279884</td>
      <td>29000000</td>
      <td>1905000000</td>
      <td>239000000</td>
      <td>1666000000</td>
      <td>2596000000</td>
      <td>2596000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-01-28</td>
      <td>9.714</td>
      <td>3.892</td>
      <td>5822000000</td>
      <td>1797000000</td>
      <td>8.150000e+08</td>
      <td>0.0</td>
      <td>815000000</td>
      <td>0.0</td>
      <td>2612000000</td>
      <td>...</td>
      <td>3589000000</td>
      <td>0.369467</td>
      <td>3210000000</td>
      <td>0.330451</td>
      <td>14000000</td>
      <td>3196000000</td>
      <td>282000000</td>
      <td>3047000000</td>
      <td>2528000000</td>
      <td>2528000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2019-01-27</td>
      <td>11.716</td>
      <td>4.545</td>
      <td>7171000000</td>
      <td>2376000000</td>
      <td>9.910000e+08</td>
      <td>0.0</td>
      <td>991000000</td>
      <td>0.0</td>
      <td>3367000000</td>
      <td>...</td>
      <td>4584000000</td>
      <td>0.391260</td>
      <td>3804000000</td>
      <td>0.324684</td>
      <td>-92000000</td>
      <td>3896000000</td>
      <td>123000000</td>
      <td>4141000000</td>
      <td>2500000000</td>
      <td>2500000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-26</td>
      <td>10.918</td>
      <td>4.150</td>
      <td>6768000000</td>
      <td>2829000000</td>
      <td>1.093000e+09</td>
      <td>0.0</td>
      <td>1093000000</td>
      <td>0.0</td>
      <td>3922000000</td>
      <td>...</td>
      <td>3403000000</td>
      <td>0.311687</td>
      <td>2846000000</td>
      <td>0.260670</td>
      <td>-124000000</td>
      <td>2970000000</td>
      <td>174000000</td>
      <td>2796000000</td>
      <td>2472000000</td>
      <td>2472000000</td>
    </tr>
    <tr>
      <th>0</th>
      <td>2021-01-31</td>
      <td>16.675</td>
      <td>6.279</td>
      <td>10396000000</td>
      <td>3924000000</td>
      <td>0.000000e+00</td>
      <td>0.0</td>
      <td>1940000000</td>
      <td>0.0</td>
      <td>5864000000</td>
      <td>...</td>
      <td>5691000000</td>
      <td>0.341289</td>
      <td>4532000000</td>
      <td>0.271784</td>
      <td>123000000</td>
      <td>4409000000</td>
      <td>77000000</td>
      <td>4332000000</td>
      <td>2468000000</td>
      <td>2512000000</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 23 columns</p>
</div>



¡Listo! Veamos a lo que me refiero


```python
plt.bar(df['date'], df['revenue'])
plt.title('Crecimiento en las ventas de NVDA', fontsize=14)
plt.xlabel('Año', fontsize=10)
plt.ylabel('Ventas totales en miles de millones de USD', fontsize=10)
plt.xticks(df['date'],['2017', '2018', '2019', '2020', '2021'])
plt.show()
```


    
![png](output_15_0.png)
    



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


    
![png](output_16_0.png)
    



```python

```
