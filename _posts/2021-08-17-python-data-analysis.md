---
layout: post
title: "Ecommerce Data Analysis"
subtitle: "Looking for insights with Python, Pandas & Matplotlib"
background: '/img/ecommerce/fondo3.png'
output: html_document
date: 2021-08-17 19 -0400
category: Python
tags: [data analysis, python, pandas, seaborn]
comments: true
---


#### ¡Hola! 👋  

Este es un proyecto especial, por primera vez escribire en español. Creo en que (equivocadamente) le di la espalda al español bajo una falsa premisa. Ahora se que puedo contribuir  al ecosistema hispano más de lo que podria en el anglosajon.

Empezare publicando un analisis donde detallare cada uno de mis pasos. Lo hare con datos que tome del canal [A2 Capacitación: Excel](https://www.youtube.com/channel/UCSW-_m4KXiok4Hq2nK97atw) y el cual les recomiendo seguir si quieren aprender Excel.

Dejando de lado lo anterior, hace tiempo escribi un articulo (esta incompleto) sobre [mi proceso para analizar datos](https://joseluistello.github.io/r/2021/07/12/data-analysis-process.html), la idea detras de este approach es abordar el analisis a traves de diferentes etapas. Estas etapas buscan estandarizar la manera en que analizo cualquier tipo de dato.

El outcome de mi proceso consiste en priorizar la legibilidad de mi analisis abordando cada etapa de forma separada (más no aislada).

Al final del día, lo que busco es entender la relacion entre mis variables y encontrar un path entre las observaciones dentro de mis datos. 


Empecemos por cargar nuestras librerias y datos <3


```python
import pandas as pd
import matplotlib as plt
import seaborn as sns
import matplotlib.pyplot as plt
```


```python
df = pd.read_csv(
    'data/Datos.csv',
    dtype={
        "Orden": int,
        "Medio" : str,
        "Vendedor" : str,
        "Plataforma" : str,
        "Tipo_Orden" : str,
        "Tipo_Cliente" : str,
        "Categoría" : str,
        "Producto" : str,
        "Precio" : int,
    },
)
```

La razón del porque esribi el upload del archivo de esta manera se debe a que es más facil editar el tipo de dato antes de, que despues de.

Este es un ejemplo de como tendriamos que modificar cada tipo de dato.

- df["Precio"] = pd.to_numeric(df["Precio"])



Ahora es tiempo de dos cosas:

1. Colocar un limite al maximo de filas que se muestran en cada return
2. Establecer un default para el tamaño de las graficas 

Les sugiero que utilicen este default. Es comodo establecer limites en el display de filas así como aumentar el tamaño de los plots.


```python
pd.set_option("display.max_rows", 12)

%matplotlib inline
plt.rcParams['figure.figsize'] = (12, 10)
```

### ¡Tiempo de entender nuestros datos! 


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 63221 entries, 0 to 63220
    Data columns (total 12 columns):
     #   Column        Non-Null Count  Dtype 
    ---  ------        --------------  ----- 
     0   Orden         63221 non-null  int32 
     1   Fecha         63221 non-null  object
     2   Medio         63221 non-null  object
     3   Vendedor      63221 non-null  object
     4   Plataforma    63221 non-null  object
     5   Comision      63221 non-null  object
     6   Tipo_Orden    63221 non-null  object
     7   Tipo_Cliente  63221 non-null  object
     8   Sexo          63221 non-null  object
     9   Categoría     63221 non-null  object
     10  Producto      63221 non-null  object
     11  Precio        63221 non-null  int32 
    dtypes: int32(2), object(10)
    memory usage: 5.3+ MB
    

❤️ **Le Magnifique**  ❤️

Tenemos variables interesantes pero primero debemos entender a que nos enfrentamos. El hecho de hacer preguntas como:
* ¿Son cualitativas o cuantitativas? 
* ¿Son continuas o categorias? 
Nos ayuda a tener una idea de como abordar un analisis. Empecemos por explicar la ciasificación de las variables.

- Los datos categoricos responden a preguntas como "qué", "quienes", o "donde", y se clasifican en tres grupos:
    - Datos nominales 
        - No tienen un orden (Paises)
    - Datos ordinales 
        - Tienen un orden (Grado de quemadura)
    - Datos binarios (dicotomicos) 
        - Solo tienen dos niveles (Genero)

- Los datos cuantitativos responden a preguntas como "cuántos", "cuánto" o con "qué" frecuencia, y se clasifican en dos grupos:
    - Datos discretos - No tienen decimales
        - Se pueden clasificar
        - Pueden ser ordinales (1ra, 2da, 3ra clase)
        - Pueden ser binarios (Vivo o muerto 1/0)
        - Pueden ser intervalios o ratios (Temperaturas)
    - Datos continuos - Tienen decimales
        - Lo mismo de arriba


Ahora que damos más claro esta parte, es hora de clasificar nuestro dataset.


```python
df.head()
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
      <th>Orden</th>
      <th>Fecha</th>
      <th>Medio</th>
      <th>Vendedor</th>
      <th>Plataforma</th>
      <th>Comision</th>
      <th>Tipo_Orden</th>
      <th>Tipo_Cliente</th>
      <th>Sexo</th>
      <th>Categoría</th>
      <th>Producto</th>
      <th>Precio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>06/08/2017</td>
      <td>Propio</td>
      <td>Directo en Tienda</td>
      <td>Website</td>
      <td>0%</td>
      <td>Compra</td>
      <td>Repetido</td>
      <td>Hombre</td>
      <td>Pantalones</td>
      <td>Pants de Entrenamiento Reactivo</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>06/08/2017</td>
      <td>Propio</td>
      <td>Directo en Tienda</td>
      <td>Website</td>
      <td>0%</td>
      <td>Compra</td>
      <td>Repetido</td>
      <td>Hombre</td>
      <td>Sudaderas y chamarras</td>
      <td>Sudadera sin Costuras</td>
      <td>50</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>06/08/2017</td>
      <td>Propio</td>
      <td>Directo en Tienda</td>
      <td>Website</td>
      <td>0%</td>
      <td>Compra</td>
      <td>Repetido</td>
      <td>Mujeres</td>
      <td>Leggings</td>
      <td>Leggings Ombre</td>
      <td>36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>06/08/2017</td>
      <td>Propio</td>
      <td>Directo en Tienda</td>
      <td>Website</td>
      <td>0%</td>
      <td>Compra</td>
      <td>Repetido</td>
      <td>Mujeres</td>
      <td>Bra deportivo</td>
      <td>Bra Vital sin costuras</td>
      <td>40</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>06/08/2017</td>
      <td>Propio</td>
      <td>Directo en Tienda</td>
      <td>Website</td>
      <td>0%</td>
      <td>Compra</td>
      <td>Repetido</td>
      <td>Hombre</td>
      <td>Camisetas</td>
      <td>Camiseta Heather</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>



- Datos Categoricos
     - Medio
     - Vendedor
     - Plataforma
     - Tipo_Orden
     - Tipo_Cliente
     - Sexo
     - Categoia
     - Producto
- Datos Continuos
     - Fecha
     - Comision
     - Precio
     
¿En que tipo de subgrupo crees que entren? Te lo dejo de tarea 😂 

Una de las cosas que me gusta hacer antes de buscar patrones es aislar variables. 
Este aislamiento me permite generar pistas acerca del dataset. Puedo ver el peso de cada variable, su distribución, sus rangos, las desviaciones que tiene, etc.  


```python
(
df["Sexo"]
    .value_counts()
)
```




    Mujeres    35937
    Hombre     27284
    Name: Sexo, dtype: int64




```python
(
df["Sexo"]
    .value_counts(normalize=True)
    .mul(100)
    .round(1)
    .astype(str) + '%'
)
```




    Mujeres    56.8%
    Hombre     43.2%
    Name: Sexo, dtype: object



Ahora se que existe una mayoría de mujeres dentro de mi set, lo cual me da señales que planeo ir guardando. Pensemoslo de esta manera:
Ir directo a enteder la relacion entre plataformas/ventas/sexo puede salir mal, existe la posibilidad de sesgar mis pensamientos en torno a un resultado. 
Puedo concluir en que se debe invertir dinero en tal plataforma porque esto atraera 'X' clientes hombres. Cuando tal vez, existan mejores lugares para poner el dinero. 

Por cierto, escribo el codigo en vertical debido a que quiero hacer legible mi analisis para su reproducción, al mismo tiempo que emulo los pipelines de R.

Bueno, sigamos marchando!


```python
(
df["Plataforma"]
    .value_counts(normalize=True)
    .mul(100)
    .round(1)
    .astype(str)+ '%'
)
```




    Instagram    53.6%
    Youtube      17.5%
    Facebook     15.4%
    Website      13.5%
    Name: Plataforma, dtype: object



Lo que nos arroja este resultado es el total de observaciones que presento cada plataforma. Esto quiere decir (hasta ahora) que Instagram es la que más unidades vende, pero eso no significa que sea la que más revenue genere.


```python
(
df["Vendedor"]
    .value_counts(normalize=True)
    .mul(100)
    .round(1)
    .astype(str)+ '%'
)
```




    Publicidad Insta      20.0%
    Directo en Tienda     13.5%
    Publicidad Face        9.4%
    Publicidad Youtube     7.9%
    karlagvzcia            4.5%
                          ...  
    geogluisovec           0.5%
    gypseajain             0.5%
    nicole.izuristilo      0.5%
    anacsimdao             0.3%
    andreaheraz            0.3%
    Name: Vendedor, Length: 44, dtype: object




```python
df["Vendedor"].hist(bins=10, color='r')
plt.xticks(rotation='vertical')
plt.grid(False)
plt.show
```


    
![png](/img/ecommerce/output1.png)
    



```python
(
df["Tipo_Cliente"]
    .value_counts()
)
```




    Repetido    32561
    Nuevo       30660
    Name: Tipo_Cliente, dtype: int64




```python
(
df["Tipo_Orden"]
    .value_counts(normalize=True)
    .mul(100)
    .round(1)
    .astype(str)+ '%'
)
```




    Compra        91.0%
    Devolucion     9.0%
    Name: Tipo_Orden, dtype: object




```python
(
df["Comision"]
    .value_counts()
)
```




    0%     32150
    30%    12807
    20%     6702
    10%     5872
    40%     5690
    Name: Comision, dtype: int64




```python
(
df["Medio"]
    .value_counts(normalize=True)
    .mul(100)
    .round(1)
    .astype(str)+ '%'
)
```




    Propio        50.9%
    Influencer    49.1%
    Name: Medio, dtype: object




```python
( 
df["Precio"]
    .describe()
    .round(1)
)
```




    count    63221.0
    mean        40.7
    std         13.6
    min         10.0
    25%         34.0
    50%         40.0
    75%         50.0
    max        100.0
    Name: Precio, dtype: float64




```python
PrecioDist = sns.histplot(
    df, 
    x="Precio",
    bins=10,
    linewidth=3, 
    kde = True)
PrecioDist.set_xlabel("Precio de los productos", fontsize = 15)
PrecioDist.set_ylabel("Volumen de productos", fontsize = 15)
```




    
![png](/img/ecommerce/output2.png)
    


Bueno, ya se puso interesante la cosa. Hasta ahora hemos aprendido:
1. El volumen de ventas es dominado por Instagram, lejos de Youtube, Facebook y el Website
2. Las mujeres representan el 56.8% de las observaciones mientras que los hombres tienen el 43.2%
3. El 55.3% de las ventas se concentra en 5 vendedores y el 42.9% en 3
4. Hay 44 vendedores "afiliados" a la compañia, me parecen muchos. Me causa algo de ruido.
5. Tienen "buena" retencion y lo coloco entre comillas ya que bien puede desplozarme despues de que un repetido compro, o sea que no hubo una tercera vez.
6. Hubo pocas devoluciones comparado a sus compras, 9% comparado con un 91%
7. Existen 5 tipos de comisiones donde la mayoria se concentra entre el 0% y 30%
8. El precio de los productos tiene un de 10 pesos y un maximo 100 pesos donde la mayoria de los productos se concentra entre los 20 y 50 pesos


##### Es tiempo de entender las relaciones entre nuestas variables. 

El aislamiento ya dio muchas pistas así que es tiempo de parar. He llegado al punto donde es necesario contar con un plan de ataque pues de lo contrario terminare perdiendome. Tengo muchas preguntas, desde saber donde se concentran las comisiones y porque, hasta entender de donde viene realmente el crecimiento.

Pensemoslo un poco, si las comisiones del 40% se concentran en un rango de precio elevado (100) , tendriamos un dropeo del revenue del 40 pesos. A los 60 pesos restantes todavía tenemos que agregarle mas costos fijos y variables. 
La empresa puede estar perdiendo dinero sin siquiera notarlo. 

Se que estoy limitado por paradigmas, esquemas y modelos pero en otro contexto esto podría ser cierto. Mucho ojo.

Si no fui muy claro, dejame que te lo explique de esta manera. En este punto debemos comenzar a preguntarnos que es lo que queremos lograr y como una variable depende o se relaciona con la otra, y el como podemos sacar el maximo provecho de eso. Algo así como esto:

![png](/img/ecommerce/dependencies.png)
    

Mmmmm, voy a utilizar un approach top-down. Esto significa que ire desde arriba hacía abajo explorando cada relacion que este en mi cabeza con un rumbo definido. 

Listo pues, ahora que todo quedo claro es tiempo de comenzar.


```python
bx = sns.histplot(df,
                  x="Medio",
                  hue='Sexo',
                  linewidth=2)
bx.set_title("Distribucion por genero", fontsize=18)
bx.set_xlabel("Canal", fontsize = 15)
bx.set_ylabel("Numero de unidades vendidas", fontsize = 15)
```

    
![png](/img/ecommerce/output3.png)



```python
(
df
 .groupby('Sexo')['Precio']
 .sum()
 .reset_index()
 .sort_values('Precio', ascending=False)
)
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
      <th>Sexo</th>
      <th>Precio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Mujeres</td>
      <td>1380627</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Hombre</td>
      <td>1191223</td>
    </tr>
  </tbody>
</table>
</div>




```python
(
df
 .groupby(['Sexo', 'Plataforma'])
 ['Precio']
 .sum()
 .reset_index(level='Sexo')
 .sort_values('Sexo', ascending=False)
)
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
      <th>Sexo</th>
      <th>Precio</th>
    </tr>
    <tr>
      <th>Plataforma</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Facebook</th>
      <td>Mujeres</td>
      <td>213132</td>
    </tr>
    <tr>
      <th>Instagram</th>
      <td>Mujeres</td>
      <td>741824</td>
    </tr>
    <tr>
      <th>Website</th>
      <td>Mujeres</td>
      <td>188001</td>
    </tr>
    <tr>
      <th>Youtube</th>
      <td>Mujeres</td>
      <td>237670</td>
    </tr>
    <tr>
      <th>Facebook</th>
      <td>Hombre</td>
      <td>182941</td>
    </tr>
    <tr>
      <th>Instagram</th>
      <td>Hombre</td>
      <td>637018</td>
    </tr>
    <tr>
      <th>Website</th>
      <td>Hombre</td>
      <td>159314</td>
    </tr>
    <tr>
      <th>Youtube</th>
      <td>Hombre</td>
      <td>211950</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.displot(df, 
            x="Precio", 
            col="Plataforma", 
            row="Sexo", 
            binwidth=6, 
            height=5, 
            facet_kws=dict(margin_titles=True))
```
    
![png](/img/ecommerce/output4.png)
    


Ok, los volumenes de ventas en el punto de aislamiento no estaban fuera de la realidad. 
Es hora de recapitular lo que sabemos:
1. Los dos generos compran más por canal propio, esto quiere decir Website y adveriting de la compañia en las diferentes plataformas
2. Las mujeres compraron 1,380,627 pesos mientras que los hombres compraron 1,191,223 pesos, una diferencia del 14%
3. Las plataformas más revenue genero entre las mujeres (en orden) fueron: 
    - Instagram con 741,824 pesos  
    - Youtube, Facebook y el Website acumularon un revenue de 638,803 pesos
4. Los hombres siguieron el mismo patron de revenue:
    - Instagram con 637,018
    - Youtube, Facebook y el Website acumularon un revenue de 554,205 pesos
5. El histograma de la plataforma pareciese que arroja cosas interesantes pero en realidad, los huecos que vemos en la fila de hombres es simplemente el reflejo de la diferencia en el revenue. Los hombres compraron menos, por ende, no se vendieron los mismos productos que con las mujeres.


```python
sns.displot(df, 
            x="Tipo_Cliente", 
            col='Medio',
            row="Sexo", 
            binwidth=6, 
            height=5, 
            facet_kws=dict(margin_titles=True))
```
    
![png](/img/ecommerce/output5.png)
    


#### Es tiempo de seguir avanzando en nuestro analisis


```python
sns.displot(df, 
            x="Tipo_Orden", 
            col="Plataforma", 
            row="Sexo", 
            binwidth=3, 
            height=4, 
            facet_kws=dict(margin_titles=True))
```


![png](/img/ecommerce/output6.png)
    



