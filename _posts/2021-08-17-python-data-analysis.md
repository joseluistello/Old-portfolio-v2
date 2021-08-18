---
layout: post
title: "Ecommerce Data Analysis"
subtitle: "Pandas and Seaborn "
background: '/img/data analysis/tukeyy.png'
output: html_document
date: 2021-08-17 19 -0400
category: Python
tags: [data analysis, python, pandas, seaborn]
comments: true
---






```python
import pandas as pd
import matplotlib as plt
import seaborn as sns
import matplotlib.pyplot as plt
```


```python
df = pd.read_csv('data/Datos.csv')
```

Lo primero que me gustaria son dos cosas: 

1. Colocar un limite a la muestra de filas
2. Establecer un default para el tamaño de las graficas 


```python
# Show up 5 rows by default
pd.set_option("display.max_rows", 12)

# Increase plots size
%matplotlib inline
plt.rcParams['figure.figsize'] = (12, 10)
```

Quiero entender que tipo de dato tengo y cual debo cambiar. 


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 63221 entries, 0 to 63220
    Data columns (total 12 columns):
     #   Column        Non-Null Count  Dtype 
    ---  ------        --------------  ----- 
     0   Orden         63221 non-null  int64 
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
     11  Precio        63221 non-null  int64 
    dtypes: int64(2), object(10)
    memory usage: 5.8+ MB
    


```python
### Cambiare precio a un valor numeroc ya que estaba como un tipo objeto.
df["Precio"] = pd.to_numeric(df["Precio"])
```

#### Mi analisis cambia dependiendo el objetivo. 

Por ejemplo, mi objetivo puede ser entender que canales son los mas beneficiosos para la empresa o entender que productos se venden mas. Inclusive puedo mezclar los dos objetivos anteriores y hacer un nuevo objetivo que busque entender cuales son los canales que mas venden y que productos son los que mas venden. 

En este caso no hay un objetivo pero marcare mi ritmo tratando de emular uno.

- Primero, quiero entender las distribuciones de distintas variables.
- Despues, quiero mezclar las variables y hacer un analisis mas profundo.
- Por ultimo, comunicar lo que entendi de todo el analisis. 


```python
df["Precio"].describe()
```




    count    63221.000000
    mean        40.680312
    std         13.574989
    min         10.000000
    25%         34.000000
    50%         40.000000
    75%         50.000000
    max        100.000000
    Name: Precio, dtype: float64




```python
q = sns.histplot(
    df, 
    x="Precio",
    linewidth=3, 
    kde = True)
q.set_xlabel("Precio de los productos", fontsize = 15)
q.set_ylabel("Producto total", fontsize = 15)
```




    Text(0, 0.5, 'Producto total')




    
![png](/img/ecommerce/output1.png))
    


Esto nos dice dos cosas: 
* La primera es que el precio de los productos de la tienda se encuentran entre el rango de 10 y 100 pesos.
* Y la segunda es que la mayoria de los productos se encuentra entre un precio de 20 y 50 pesos.


```python
df["Sexo"].value_counts()
```




    Mujeres    35937
    Hombre     27284
    Name: Sexo, dtype: int64




```python
ax = sns.histplot(df,
                  x="Sexo",
                  linewidth=4)
ax.set_xlabel("Genero", fontsize = 15)
ax.set_ylabel("Numero de personas", fontsize = 15)
```




    Text(0, 0.5, 'Numero de personas')




    
![png](/img/ecommerce/output2.png)
    



```python
df["Medio"].value_counts()
```




    Propio        32150
    Influencer    31071
    Name: Medio, dtype: int64




```python
bx = sns.histplot(df,
                  x="Medio",
                  hue='Sexo',
                  linewidth=2)
bx.set_title("Distribucion por genero", fontsize=18)
bx.set_xlabel("Canal por el que se vendio", fontsize = 15)
bx.set_ylabel("Numero de ventas", fontsize = 15)
```




    Text(0, 0.5, 'Numero de ventas')




    
![png](/img/ecommerce/output3.png)
    



```python
d = sns.histplot(
    df, 
    x="Plataforma",
    hue="Sexo",
    linewidth=2)
d.set_xlabel("Platorma Digital", fontsize = 15)
d.set_ylabel("Numero de ventas", fontsize = 15)
```




    Text(0, 0.5, 'Numero de ventas')




    
![png](/img/ecommerce/output4.png)
    



```python
sns.displot(df, 
            x="Precio", 
            col="Plataforma", 
            row="Sexo", 
            binwidth=3, 
            height=5, 
            facet_kws=dict(margin_titles=True))
```




    <seaborn.axisgrid.FacetGrid at 0x1d3e27f7ac0>




    
![png](/img/ecommerce/output5.png)
    


Ya estamos obteniendo insights.

1. Hay casi 7,000 mujeres mas que hombres dentro de la plataforma.
2. Se vende un poco más por canales propios y los generos siguen esa tendencia. 
3. Las plataformas que más predomina es Instagram, seguido de Youtube, Facebook y el Website del comercio.
4. Las mujeres se mantienen a la cabeza dentro de los 4 canales. 
5. En el ultimo histograma podemos observar distintas cosas.
    - 4.1 Las mujeres compran más articulos que los hombres dentro de cualquier plataforma
    - 4.2 Las mujeres compran articulos del maximo rango en cualquier plataforma.
    - 4.3 La plataforma que más productos de alto valor vende es Instagram.

Podemos englobar el conocimiento que tenemos sobre el data set hasta ahora:
1. Sabemos como se distribuye el precio de los productos y donde se concentra la mayor parte de los productos
2. Sabemos la disparidad del genero
3. Sabemos que canal y plataformas son las que mas venden productos
4. Donde se compran los articulos de alto valor y que genero los compra


#### Es tiempo de seguir avanzando en nuestro analisis


```python
(df
 .groupby('Sexo')['Precio']
 .sum().reset_index()
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
(df
 .groupby(['Plataforma', 'Sexo'])
 ['Precio']
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
      <th>Plataforma</th>
      <th>Sexo</th>
      <th>Precio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Instagram</td>
      <td>Mujeres</td>
      <td>741824</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Instagram</td>
      <td>Hombre</td>
      <td>637018</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Youtube</td>
      <td>Mujeres</td>
      <td>237670</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Facebook</td>
      <td>Mujeres</td>
      <td>213132</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Youtube</td>
      <td>Hombre</td>
      <td>211950</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Website</td>
      <td>Mujeres</td>
      <td>188001</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Facebook</td>
      <td>Hombre</td>
      <td>182941</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Website</td>
      <td>Hombre</td>
      <td>159314</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('Sexo')['Precio'].sum().reset_index().sort_values('Precio', ascending=False)
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
df.groupby(['Sexo', 'Plataforma'])['Precio'].sum().reset_index().sort_values('Precio', ascending=False)
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
      <th>Plataforma</th>
      <th>Precio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>Mujeres</td>
      <td>Instagram</td>
      <td>741824</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Hombre</td>
      <td>Instagram</td>
      <td>637018</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Mujeres</td>
      <td>Youtube</td>
      <td>237670</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Mujeres</td>
      <td>Facebook</td>
      <td>213132</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hombre</td>
      <td>Youtube</td>
      <td>211950</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Mujeres</td>
      <td>Website</td>
      <td>188001</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Hombre</td>
      <td>Facebook</td>
      <td>182941</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Hombre</td>
      <td>Website</td>
      <td>159314</td>
    </tr>
  </tbody>
</table>
</div>




```python
df["Tipo_Orden"].value_counts()
```




    Compra        57540
    Devolucion     5681
    Name: Tipo_Orden, dtype: int64




```python
sns.displot(df, 
            x="Tipo_Orden", 
            col="Plataforma", 
            row="Sexo", 
            binwidth=3, 
            height=4, 
            facet_kws=dict(margin_titles=True))
```




    <seaborn.axisgrid.FacetGrid at 0x182e18a6460>




    
![png](/img/ecommerce/output6.png)
    



```python
df["Tipo_Cliente"].value_counts()
```




    Repetido    32561
    Nuevo       30660
    Name: Tipo_Cliente, dtype: int64




```python
df["Producto"].value_counts()
```




    Leggings Flex             1832
    Tanga sin costuras        1285
    Sudadera Degree           1187
    Leggings Ombre            1182
    Sudadera Cross back       1181
                              ... 
    Top Fit sin costuras       106
    Sudadera Fitness           104
    Camiseta Fitness           102
    Unitardo Deportivo 7/8     102
    Solace Sweater              83
    Name: Producto, Length: 101, dtype: int64




```python
df["Categoría"].value_counts()
```




    Pantalones               8067
    Leggings                 7772
    Chamarras y Sudaderas    7445
    Interior                 7233
    Sudaderas y chamarras    7010
    Camisetas y Tops         6412
    Bra deportivo            5885
    Camisetas                4374
    Shorts                   3656
    Ropa Interior            3127
    Calcetines               2240
    Name: Categoría, dtype: int64




```python
df["Comision"].value_counts()
```




    0%     32150
    30%    12807
    20%     6702
    10%     5872
    40%     5690
    Name: Comision, dtype: int64




```python

```
