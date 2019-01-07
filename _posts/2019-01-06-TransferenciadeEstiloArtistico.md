---
title: "Transferencia de Estilo Artístico en PyTorch"
date: 2019-01-06
tags: [En Español]
excerpt: "Transferir el estilo artístico de una obra de arte a una imagen cualquiera"
mathjax: "True"
---

## Transferencia de Estilo Artístico en PyTorch

En este notebook, usaremos PyTorch para aplicar la técnica de transferencia de estilo artístico. 
Usaremos una imagen del pintor ecuatoriano Eduardo Kingman para determinar el estilo el cual será aplicado a una segunda imagen. También usaremos la red VGG19 la cual esta pre-entrenada y consituye de 19-capas formadas por series de capas convolucionales y maxpooling y también algunas capas completamente conectadas.




```python
# Importar librerías requeridas

# Comando 'mágico' que permite mostrar las imagenes en las celdas del notebook
%matplotlib inline


import pandas as pd 
import numpy as np
import matplotlib.pyplot as plt
from PIL import Image

import torch
import torch.optim as optim
from torchvision import transforms, models

```

## Cargar red VGG19 (características)

VGG19 esta dividido en dos partes:
    * vgg19.features la cual contiene todos las capas convolucionales y maxpooling
    * vgg19.classifiers que contiene los tres capas de clasificación linear que están al final.
    
Para este ejercicio solo necesitamos las características (vgg19.features)



```python
# Obtener las características de VGG19
vgg = models.vgg19(pretrained = True).features

# Congelar todos los parámetros del VGG19 por que solo estamos optimizando para una sola imagen
for param in vgg.parameters():
    param.requires_grad_(False)
    
```


```python
# Mover el modelo al GPU, si hay uno disponible si no en el CPU
# Mi máquina no tiene GPU :(

device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
vgg.to(device)
```


    Sequential(
      (0): Conv2d(3, 64, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (1): ReLU(inplace)
      (2): Conv2d(64, 64, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (3): ReLU(inplace)
      (4): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
      (5): Conv2d(64, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (6): ReLU(inplace)
      (7): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (8): ReLU(inplace)
      (9): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
      (10): Conv2d(128, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (11): ReLU(inplace)
      (12): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (13): ReLU(inplace)
      (14): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (15): ReLU(inplace)
      (16): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (17): ReLU(inplace)
      (18): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
      (19): Conv2d(256, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (20): ReLU(inplace)
      (21): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (22): ReLU(inplace)
      (23): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (24): ReLU(inplace)
      (25): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (26): ReLU(inplace)
      (27): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
      (28): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (29): ReLU(inplace)
      (30): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (31): ReLU(inplace)
      (32): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (33): ReLU(inplace)
      (34): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (35): ReLU(inplace)
      (36): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
    )



## Cargar las imagenes de contenido y estilo

La imagen de estilo es la del pintor y la del contenido puede ser cualquier imagen a la cual queremos aplicar el estilo artistico.


```python
# Función que carga las imagenes
def cargar_imagen(directorio_imagen, tamaño_maximo = 400, shape = None ):
    '''Cargar y transformar una imagen aegurando que su tamanño sea menor =400 pixeles
    en la dimensión x, y'''
    imagen = Image.open(directorio_imagen).convert('RGB')
    # transformar las imagenes -- imagenes grandes disminuyen velocidad de procesamiento
    if max(imagen.size) > tamaño_maximo:
        tamaño = tamaño_maximo
    else:
        tamaño = max(imagen.size)
        
    if shape is not None:
        tamaño = shape
        
    en_transform = transforms.Compose([
                        transforms.Resize(tamaño),
                        transforms.ToTensor(),
                        transforms.Normalize((0.485, 0.456, 0.406),
                                             (0.229, 0.224, 0.225))])
    
    # descartar el transparente canal alpha y anadir la dimensión del lote
    imagen = en_transform(imagen)[:3,:,:].unsqueeze(0)
    return imagen
        
```

Cargar las imagenes usando el nombre del archivo y forzar la imagen de estilo a tener el mismo tamaño de la imagen de contenido


```python
# Cargar la imagen de contenido y estilo
contenido = cargar_imagen('/Jupyter Notebooks/data/san_franciso.jpg').to(device)
# Redimenzionar la imagen de estilo para que sea igual a la de contenido
estilo = cargar_imagen('/Jupyter Notebooks/data/obra_lugar_natal_kingman.jpg', 
                     shape = contenido.shape[-2:]).to(device)
```


```python
# Función de ayuda para de-normalizar una imagen y convertirla
# de una imagen Tensor a una imagen Numpy para poder presentarla
def im_convert(tensor):
    ''' Presentar imagen como Tensor'''
    imagen = tensor.to('cpu').clone().detach()
    imagen = imagen.numpy().squeeze()
    imagen = imagen.transpose(1, 2, 0)
    imagen = imagen * np.array((0.029, 0.224, 0.225)) + np.array((0.485, 0.456, 0.406))
    imagen = imagen.clip(0, 1)
    
    return imagen

```


```python
# Presentar las imagenes
fig, (ax1, ax2) = plt.subplots(1, 2, figsize = (20, 10))
# Poner imagenes de contenido y estilo lado a lado
ax1.imshow(im_convert(contenido))
ax2.imshow(im_convert(estilo))
```




![alt]({{ site.url }}{{ site.baseurl }}/images/DeepLearning/input_images.png)




## Capas de VGG19
Para obtener el estilo y contenido de cada imagen debemos pasarlas a travez de las capas del la red VGG19 hasta obtener la capa(s) deseada y el output de aquella capa.


```python
# Mostrar la estructura de la red VGG19 para mirar sus varias capas
print (vgg)
```

    Sequential(
      (0): Conv2d(3, 64, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (1): ReLU(inplace)
      (2): Conv2d(64, 64, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (3): ReLU(inplace)
      (4): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
      (5): Conv2d(64, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (6): ReLU(inplace)
      (7): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (8): ReLU(inplace)
      (9): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
      (10): Conv2d(128, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (11): ReLU(inplace)
      (12): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (13): ReLU(inplace)
      (14): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (15): ReLU(inplace)
      (16): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (17): ReLU(inplace)
      (18): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
      (19): Conv2d(256, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (20): ReLU(inplace)
      (21): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (22): ReLU(inplace)
      (23): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (24): ReLU(inplace)
      (25): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (26): ReLU(inplace)
      (27): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
      (28): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (29): ReLU(inplace)
      (30): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (31): ReLU(inplace)
      (32): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (33): ReLU(inplace)
      (34): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (35): ReLU(inplace)
      (36): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
    )


## Características de Contenido y Estilo



```python
def obtener_carac(imagen, modelo, capas=None):
    ''' Pasar la imagen a travez del modelo y obtener las características para un grupo de capas
        Capas de defecto del VGNet so iguales a las Gatys et al. (2016)'''
    # mapa de los nombres de las capas de PyTorch VGGNet 
    if capas is None:
        capas = {'0'  : 'conv1_1',
                 '5'  : 'conv2_1', 
                 '10' : 'conv3_1',
                 '19' : 'conv4_1',
                 '21' : 'conv4_2',
                 '28' : 'conv5_1'}
        
    características = {}
    x = imagen
        # model.module es un diccionary que contiene todos los módulos en el model
    for nombre, capa, in modelo._modules.items():
        x = capa(x)
        if nombre in capas:
            características[capas[nombre]] = x
    return características
```

## Matriz de Gram
El output de cada capa convolucional es un Tensor con las dimensiones asociadas al batch_size (tamaño del lote), profundidad (d), altura (h) y acnchura (w). La matriz de Gram de capa convolucional se calcula de la siguiente manera:
    * Obtiene la profundidad (d), altura (h), y anchura (w) del tensor usando batch_size, d, h, w = tensor.size
    * Remodela el tensor para que las dimensiones espaciales este planas -- aplana el tensor
    * Calcula la matriz de Gram multiplicando el tensor remodelado por su transpuesto
        * Para multiplicar matrices en PyTorch: torch.mm(matriz1, matriz2)
        


```python
def matriz_Gram(tensor):
    ''' Calcula la Matriz Gram
        https://es.wikipedia.org/wiki/Matriz_de_Gram
    '''
    # Obtener tamaño de lote (batch_size), profundidad (d),altura (h), y anchura (w) del Tensor
    _, d, h, w = tensor.size()
    
    # Remodelar el Tensor para multiplicar sus características por cada canal
    tensor = tensor.view(d, h * w)
    
    # Calcular la Matriz de Gram
    gram = torch.mm(tensor, tensor.t())
    
    return gram
    
    
```

## Armando el rompecabezas...
Ahora que ya tenemos funciones para extraer características y calcular la matriz de Gram para dada capa convolucional, es hora de juntar las piezas.


```python
# Obtener características de contenido y estilo -- solo una vez antes de entrenar a la red
características_contenido = obtener_carac(contenido, vgg)
características_estilo    = obtener_carac(estilo, vgg)

# Calcular la matriz de Gram para cada capa de la representación de estilo
grams_estilo = {capa: matriz_Gram(características_estilo[capa]) for capa in características_estilo}

# Crear una tercera imagen 'objetivo' y prepararla para cambios
objetivo = contenido.clone().requires_grad_(True).to(device)
```

## Pesos y Pérdidas

### Pesos individuales de la capa de estilos

Tenemos la opcioón de añadir peso a la representación del estilo en cada capa relevante. Es sugerido usar un range de 0-1 cuando añadimos peso a estas capas. Cuando añadimos mas pesos a las primeras capas (conv1_1, conv2_1), podemos esperar una mayor aplicación del estilo a la imagen final. Si decidimos añadir mas peso a las capas finales, obtendremos un mayor énfasis en pequeñas características. Esto se debe a que cada capa es de diferente tamaño y cuando se juntan crean una representación del estilo a multi-escala.


```python
# Pesos por cada capa del estilo
pesos_estilo = {'conv1_1' : 1.,
              'conv2_1' : 0.75,
              'conv3_1' : 0.2,
              'conv4_1' : 0.2,
              'conv5_1' : 0.2}

peso_contenido = 1 #alpha
peso_estilo = 1e6  #beta
```

## Actualizando Objetivo y Calculando Pérdidas
El número de veces que el objetivo (imagen final) debe ser actualizada es de gusto personal. Esto es similar al número de 'epochs' que usamos para entrenar otras redes neuronales. Los expertos recomiendan actualizar por lo menos 2000 veces para obtener buenos resultados. 
Dentro de cada iteración, se calcular la pérdida de contenido y estilo y se actualizará el objetivo.

### Pérdida de Contenido
La pérdida del contenido sera el promedio al cuadrado de la resta del objetivo y características del contenido en la capa `conv4_2`. Y se calcula de la siguiente manera:
  * pérdida_contenido = torch.mean((características_objetivo['conv4_2'] - características_contenido['conv4_2'])**2)
    
### Pérdida de Estilo
La pérdida de estilo se calcula de una manera similar, solamente que debes iterar a travez del número de capas especificado por nombre en el diccionario peso_estilo.

### Pérdida total
Finalmente crearemos la pêrdida total suamando la pérdida de contenido y la pérdida de estilo y añdiendo peso con, las previamente definidas, alpha y beta


```python
# Presentar el objetivo (imagen final) cada cierto número de veces
presentar_cada = 10

# Iterar por los híper-parámetros
optimizer = optim.Adam([objetivo], lr = 0.003)
pasos = 100

for ii in range(1, pasos+1):
    # obtener características de la imagen objetivo
    características_objetivo = obtener_carac(objetivo, vgg)
    
    # pérdida en contenido
    pérdida_contenido = torch.mean((características_objetivo['conv4_2'] - características_contenido['conv4_2'])**2)
    
    # pérdida en estilo
    # iniciar la pérdida en estilo en zero
    pérdida_estilo = 0 
    # añadir la pérdida de la matriz de Gram por cada capa
    for capa in pesos_estilo:
        # obtener el estilo de representración del objetivo en cada capa
        característica_objetivo = características_objetivo[capa]
        gram_objetivo = matriz_Gram(característica_objetivo)
        _, d, h, w = característica_objetivo.shape
        # Obtener el 'estilo' en la representación de estilo
        gram_estilo = grams_estilo[capa]
        
        # Pérdida de estilo por capa -- añadiendo peso apropiadamente
        pérdida_capa_estilo = pesos_estilo[capa] * torch.mean((gram_objetivo - gram_estilo)**2)
        # Añadir perdida en estilo
        pérdida_estilo += pérdida_capa_estilo / (d * h* w)
        
    # Calcular pérdida total
    pérdida_total = peso_contenido * pérdida_contenido + peso_estilo * pérdida_estilo
    
    # Actualizar la imagen objetivo
    optimizer.zero_grad()
    pérdida_total.backward()
    optimizer.step()
    
    # Presentar las imagenes intermedias para ver como van cambiando y mostrar la pérdida
    if ii % presentar_cada == 0:
        print("Pérdida Total: ", pérdida_total.item())
        plt.imshow(im_convert(objetivo))
        plt.show()
        
```

    Pérdida Total:  15695283.0


![alt]({{ site.url }}{{ site.baseurl }}/images/DeepLearning/output_22_1.png)

   


## Presentar la imagen de contenido y la imagen final 


```python
fig, (ax1, ax2) = plt.subplots(1, 2, figsize = (20, 10))
ax1.imshow(im_convert(contenido))
ax2.imshow(im_convert(objetivo))

```



![alt]({{ site.url }}{{ site.baseurl }}/images/DeepLearning/output_images.png)



```python

```

-- Contenido basado en el curso Deep Learning with PyTorch de Udacity -- 