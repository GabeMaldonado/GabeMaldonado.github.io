---
title: "Importar Datos Financieros (Bolsa de Valores) Desde La Web"
date: 2018-12-17
tags: [En Español]
excerpt: "Importando Datos de la Bolsa de Valores"
mathjax: "True"
---

## En este ejercicio usaremos el 'pandas_datareader' para importar datos financieros del stock de la companía Apple (AAPL) directamente a un 'Data Frame' y también trazaremos un gráfico linear para poder observar la tendencia en el precio del stock.

El uso de 'pandas_datareader' es muy conveniente cuando queremos crear un 'Data Frame' que contiene la información financiera de algun 'stock'.

El proceso es relativamente fácil y no requiere de mucho código en Python. La información finaciera esta disponible de varias fuentes tales como: GoogleFinance, Yahoo!, la Reserva Federal de los EEUU (Federal Reserve), el Bank Mundial, etc. 


```python
# Importar los módulos requeridos
import pandas as pd
import numpy as np
import pandas_datareader as pdr 
from datetime import datetime
#import datetime
import matplotlib.pyplot as plt
import seaborn as sns
sns.set_style('whitegrid')
%matplotlib inline
```


```python
# Definir el período de tiempo que queremos analizar el stock (un año, en este caso)

fecha_final = datetime.now()
print (fecha_final)

fecha_inicial = datetime(fecha_final.year -1, fecha_final.month, fecha_final.day)
print (fecha_inicial)
```

    2018-10-23 21:29:25.592488
    2017-10-23 00:00:00



```python
"""
Usar pandas_datareader para importar datos y crear un nuevo Data Frame llamado 'datos_stock'
pandas_datareader requiere cuatro parámetros:
   1 - el 'tick' o código del stock, en este caso 'AAPL' por Apple
   2 - la fuente de donde vienen los datos, en este caso 'yahoo'
   3 - la fecha de inicio que declaramos arriba
   4 - la fecha de finalización, declarada ariiba también

"""

datos_stock = pdr.DataReader('AAPL', 'yahoo', start, end)

# Imprimir la información básica de nuestro Data Frame usando el método .info()

datos_stock.info()
```

    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 253 entries, 2017-10-23 to 2018-10-23
    Data columns (total 6 columns):
    Open         253 non-null float64
    High         253 non-null float64
    Low          253 non-null float64
    Close        253 non-null float64
    Adj Close    253 non-null float64
    Volume       253 non-null int64
    dtypes: float64(5), int64(1)
    memory usage: 13.8 KB



```python
# Imprimir las primeras 5 filas del Data Frame (la "cabeza") usando el método .head()

datos_stock.head()
```


<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2017-10-23</th>
      <td>156.889999</td>
      <td>157.690002</td>
      <td>155.500000</td>
      <td>156.169998</td>
      <td>153.843857</td>
      <td>21984300</td>
    </tr>
    <tr>
      <th>2017-10-24</th>
      <td>156.289993</td>
      <td>157.419998</td>
      <td>156.199997</td>
      <td>157.100006</td>
      <td>154.760010</td>
      <td>17757200</td>
    </tr>
    <tr>
      <th>2017-10-25</th>
      <td>156.910004</td>
      <td>157.550003</td>
      <td>155.270004</td>
      <td>156.410004</td>
      <td>154.080307</td>
      <td>21207100</td>
    </tr>
    <tr>
      <th>2017-10-26</th>
      <td>157.229996</td>
      <td>157.830002</td>
      <td>156.779999</td>
      <td>157.410004</td>
      <td>155.065399</td>
      <td>17000500</td>
    </tr>
    <tr>
      <th>2017-10-27</th>
      <td>159.289993</td>
      <td>163.600006</td>
      <td>158.699997</td>
      <td>163.050003</td>
      <td>160.621384</td>
      <td>44454200</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Imprimir las últimas 5 filas del Data Frame (la 'cola') usando el método .tail() 
datos_stock.tail()
```


<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-10-17</th>
      <td>222.300003</td>
      <td>222.639999</td>
      <td>219.339996</td>
      <td>221.190002</td>
      <td>221.190002</td>
      <td>22885400</td>
    </tr>
    <tr>
      <th>2018-10-18</th>
      <td>217.860001</td>
      <td>219.740005</td>
      <td>213.000000</td>
      <td>216.020004</td>
      <td>216.020004</td>
      <td>32581300</td>
    </tr>
    <tr>
      <th>2018-10-19</th>
      <td>218.059998</td>
      <td>221.259995</td>
      <td>217.429993</td>
      <td>219.309998</td>
      <td>219.309998</td>
      <td>33078700</td>
    </tr>
    <tr>
      <th>2018-10-22</th>
      <td>219.789993</td>
      <td>223.360001</td>
      <td>218.940002</td>
      <td>220.649994</td>
      <td>220.649994</td>
      <td>28792100</td>
    </tr>
    <tr>
      <th>2018-10-23</th>
      <td>215.830002</td>
      <td>223.250000</td>
      <td>214.699997</td>
      <td>222.729996</td>
      <td>222.729996</td>
      <td>38616200</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Trazar un gráfico del precio del stock en este año. El precio del stock se encuentra la columna 'Adj Close'
# usando el .plot() método del módulo matplotlib

datos_stock['Adj Close'].plot(legend=True, figsize=(10,4))
```

  
![alt]({{ site.url }}{{ site.baseurl }}/images/datareader_appl.png)


