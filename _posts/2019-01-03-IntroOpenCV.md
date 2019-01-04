---
title: "Intro a OpenCV"
date: 2019-01-03
tags: [En Español]
excerpt: "Cargar imagenes y aplicar filtros"
mathjax: "True"
---


## Cargando imagenes, aplicando filtros usando OpenCv

En este notebook, usaremos la librería CV2 de OpenCV con la interface en python para cargar y manipular imagenes. Cambiaremos las imágenes de color a blanco y negro y aplicaremos filtros que nos ayudaran a detectar bordes. Esto es muy importante cuando trabajamos en detección y clasificación de objectos.

### Un  poco de información sobre OpenCv
OpenCV (Open Source Computer Vision) es una librería de Visión Computarizada y Apredizaje Automático (Machine Learning.)
De acuerdo a su pagina web, esta librería tiene más de 2500 algoritmos optimizados los cuales pueden ser utilizados para detectar y reconocer rostros, identificar objetos, identificar movimientos y acciones humanas, rastrear objetos en movimiento, extraer modelos 3D de objetos, entre otros. 
Para más información visita: https://opencv.org/

Si no tienes OpenCv y tienes instalado 'pip' en tu entorno de python, corre el siguiente comando en al consola/cmd:
pip install opencv-python



```python
# Importar librerías necesarias

import matplotlib.pyplot as plt
import matplotlib.image as mpimg

import cv2
import numpy as np

# Este comando nos permite mostrar la imagen en la celda
%matplotlib inline

# Cargar la imagen -- pasa la dirección donde se encuentra tu imagen como argumento a .imread()
imagen = mpimg.imread('Jupyter Notebooks/data/tech_tower.jpg')

plt.imshow(imagen)
```




    <matplotlib.image.AxesImage at 0x128f31400>




![alt]({{ site.url }}{{ site.baseurl }}/images/DeepLearning/output_1_1.png)




```python
# Cargar una seguando imagen
imagen_2 = mpimg.imread('Jupyter Notebooks/data/nazare.jpg')

plt.imshow(imagen_2)
```




    <matplotlib.image.AxesImage at 0x12a517cf8>




![alt]({{ site.url }}{{ site.baseurl }}/images/DeepLearning/output_2_1.png)


## Convertir las imagenes de color a blanco y negro


```python
# Cambiar imagen a blaco y negro (gris) para después aplicar filtros
# Pasa el nombre de la variable que contiene la imagen como primer argumento,
# cv2.COLOR_RGB2GRAY como segundo argumento
# -- cv2.COLOR_RGB esto es la imagen a color (Red - Green - Blue) 2 (a) GRAY (Gris)

imagen_1_gris = cv2.cvtColor(imagen, cv2.COLOR_RGB2GRAY)

plt.imshow(imagen_1_gris, cmap = 'gray')
```




    <matplotlib.image.AxesImage at 0x12abd02b0>



![alt]({{ site.url }}{{ site.baseurl }}/images/DeepLearning/output_4_1.png)


```python
# Cambiar imagen a blaco y negro (gris) para después aplicar filtros
# Hacemos lo mismo que anteriormente para esta segunda imagen

imagen_2_gris = cv2.cvtColor(imagen_2, cv2.COLOR_RGB2GRAY)

plt.imshow(imagen_2_gris, cmap = 'gray')
```




    <matplotlib.image.AxesImage at 0x12ac11b70>



![alt]({{ site.url }}{{ site.baseurl }}/images/DeepLearning/output_5_1.png)


## Crear un Kernel Costumizado

Aquí veremos un tipo de Kernel Costumizado que se usa como filtro de detección de bordes: el filtro Sobel.

Este filtro de Sobel es comúnmente utilizado en detección de bordes ya que encuentra patrones de intensidad de la imagen. Cuando aplicamos un filtro de Sobel, básicamento lo que hacemos es tomar una approximación del derivado de la imagen con respecto a la dirección en x or y, separadamente. 

Puedes jugar a modificar los valores en el array del filtro para ver sus distintos efectos. 



```python
# Crear un kernel costumizado para la imagen_1_gris
# array de 3x3 para identificar bordes
sobel_y = np.array([[ -1, -2, -1], 
                   [ -1, 1, 1], 
                   [ 1, 2, 1]])

#Create and apply a Sobel x operator
sobel_x = np.array([[-1, 0, 1],
                   [-2, 0, 1],
                   [-1, 0, 1]])

# Applcar el filtro a la imagen con los argumentos: imagen_en_gris, profundidad, kernel/filtro_sobel
imagen_filtrada = cv2.filter2D(imagen_1_gris, -1, sobel_y)

plt.imshow(imagen_filtrada, cmap='gray')
```




    <matplotlib.image.AxesImage at 0x12ad410b8>



![alt]({{ site.url }}{{ site.baseurl }}/images/DeepLearning/output_8_1.png)



```python
# Crear un kernel costumizado para la imagen_2_gris
# array de 3x3 para identificar bordes
sobel_y = np.array([[ -1, -2, -1], 
                   [ -1, 1, 1], 
                   [ 1, 2, 1]])

#Create and apply a Sobel x operator
sobel_x = np.array([[-1, 0, 1],
                   [-2, 0, 1],
                   [-1, 0, 1]])

# Applcar el filtro a la imagen con los argumentos: imagen_en_gris, profundidad, kernel/filtro_sobel
imagen_filtrada_2 = cv2.filter2D(imagen_2_gris, -1, sobel_y)

plt.imshow(imagen_filtrada_2, cmap='gray')
```




    <matplotlib.image.AxesImage at 0x13d55b860>



![alt]({{ site.url }}{{ site.baseurl }}/images/DeepLearning/output_9_1_sobel.png)
![png](output_9_1.png)



```python

```
