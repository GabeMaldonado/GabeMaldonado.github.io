---
title: "LSTMs para Generar Texto en PyTorch"
date: 2019-01-19
tags: [En Español]
excerpt: "Usando un LSTM para generar texto"
mathjax: "True"
---

# LSTM a Nivel de Cáracteres en PyTorch

### Generación Automática de Texto

En este notebook, construiremos un LSTM (Long Short Term Memory) en PyTorch para generar texto de manera automática.  Esta red utilizará un texto para entrenamiento y  procesará este texto cáracter por cáracter, aprederá de él y como resultado generará texto de la misma manera. Para esto usaremos el Premio Nobel de la Literatura *Cien años de Soledad* del gran **Gabriel García Márquez** para entrenar nuestra red. Para ejecutar este notebook, usé Google Colab -- que es básicamente un Jupyter notebook que puede ser ejecutado en el navegador (Chrome). Colab requiere un poco más de trabajo inicial (set-up) pero ofrece el uso gratuito de un GPU. Algo que realmente vale la pena y recomiendo ser usado.

![alt]({{ site.url }}{{ site.baseurl }}/images/gabo_100.png)


### Importemos los módulos necesarios para cargar los datos y generar nuestro modelo.


```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

import torch
from torch import nn
import torch.nn.functional as F

```


```python
# Cargar el archivo y leerlo como texto
with open ('/content/gabo_soledad.txt', 'r') as f:
    texto = f.read()
```


```python
# Leer los primeros 100 cáracteres
texto[:100]
```




    'Gabriel García Márquez \nCien años de soledad \nMuchos años después, frente al pelotón de fusilamiento'




```python
# Codificar el texto y asignar a cada cáracter un número entero y viceversa

# Crear dos dictionarios
# 1- int2char, que asigna un número entero a un cáracter
# 2- char2int, que asigna un cáracter a un número entero único
chars = tuple(set(texto))
int2char = dict(enumerate(chars))
char2int = {ch: ii for ii, ch in int2char.items()}

# encode the text
codificado = np.array([char2int[ch] for ch in texto])
```


```python
codificado[:100]
```




    array([31, 37, 65, 41, 51, 82, 23, 46, 31, 37, 41, 53, 67, 37, 46, 35, 14,
           41,  2, 55, 82, 42, 46, 84, 45, 51, 82, 66, 46, 37,  7, 19, 64, 46,
           73, 82, 46, 64, 19, 23, 82, 73, 37, 73, 46, 84, 35, 55, 53, 72, 19,
           64, 46, 37,  7, 19, 64, 46, 73, 82, 64, 78, 55, 71, 64, 28, 46, 81,
           41, 82, 66, 75, 82, 46, 37, 23, 46, 78, 82, 23, 19, 75, 10, 66, 46,
           73, 82, 46, 81, 55, 64, 51, 23, 37, 26, 51, 82, 66, 75, 19])




```python
# Pre-procesamiento de Data

def one_hot_encode(arr, n_labels):
    # Iniciar el array codificado
    one_hot = np.zeros((np.multiply(* arr.shape), n_labels), dtype = np.float32)
    
    # Rellenar los elementos apropiados con el número uno
    one_hot[np.arange(one_hot.shape[0]), arr.flatten()] = 1.
    
    # Regresar el array a su forma original
    one_hot = one_hot.reshape((*arr.shape, n_labels))
    
    return one_hot
```


```python
# Poner a prueba la función
test_seq = np.array([[3, 5, 1]])
one_hot = one_hot_encode(test_seq, 8)

print(one_hot)
```

    [[[0. 0. 0. 1. 0. 0. 0. 0.]
      [0. 0. 0. 0. 0. 1. 0. 0.]
      [0. 1. 0. 0. 0. 0. 0. 0.]]]



```python
def get_batches(arr, batch_size, seq_length):
    """
      Crear un generador que regresa lotes/batches de size
      batch_size x seq_length del arr.

      Argumentos:
      arr -- array del cual vamos a hacer batches
      batch_size -- Batch size, el número de sequencias por batch
      seq_length -- Número de cáracteres codificados en la sequencia
    """
    
    batch_size_total = batch_size * seq_length
    # Número Total de batches que podemos hacer:
    n_batches = len(arr)//batch_size_total
    
    # Mantener solamento los cáracteres que son suficientes para hacer un batch completo
    arr = arr[:n_batches * batch_size_total]
    # Cambiar la forma a batch_size rows
    arr = arr.reshape((batch_size, -1))
    
    # Iterar a través del array, una sequencia a la vez
    for n in range (0, arr.shape[1], seq_length):
        # Cáracteristicas
        x = arr[:, n:n+seq_length]
        # Objetivos desplazados por uno
        y = np.zeros_like(x)
        try:
            y[:, :-1], y[:, -1] = x[:, 1:], arr[:, n+seq_length]
        except IndexError:
            y[:, :-1], y[:, -1] = x[:, 1:], arr[:, 0]
        yield x,y
      
```


```python
# Poner a prueba la implementación
batches = get_batches(codificado, 8, 50)
x, y = next(batches)
```


```python
# Mostrar los primeros 10 elementos de la sequencia
print('x\n', x[:10, :10])
print('\ny\n', y[:10, :10])
```

    x
     [[31 37 65 41 51 82 23 46 31 37]
     [66 51 53 37 46 75 82 10 41 51]
     [64 55 64 46 78 41 19 53 23 37]
     [78 37 64 37 73 19 28 46 77 41]
     [73 19 46 84 78 41 51 26 19 41]
     [66 81 37 66 53 51 37 46 51 66]
     [46 53 51 82 23 19 46 82 66 46]
     [66 73 19 46 55 66 46 66 51  7]]
    
    y
     [[37 65 41 51 82 23 46 31 37 41]
     [51 53 37 46 75 82 10 41 51 53]
     [55 64 46 78 41 19 53 23 37 26]
     [37 64 37 73 19 28 46 77 41 64]
     [19 46 84 78 41 51 26 19 41 19]
     [81 37 66 53 51 37 46 51 66 86]
     [53 51 82 23 19 46 82 66 46 55]
     [73 19 46 55 66 46 66 51  7 19]]



```python
# Verificar si tenemos GPU disponible

entrenar_en_gpu = torch.cuda.is_available()
if (entrenar_en_gpu):
    print ('Entrenando en GPU')
else:
    print('No hay GPU disponible :( -- entrenando en CPU')
```

    Entrenando en GPU



```python
class CharRNN(nn.Module):
    
    def __init__(self, tokens, n_hidden=256, n_layers=2,
                               drop_prob=0.5, lr=0.001):
        super().__init__()
        
        """
          Definir la arquitectura de nuestra red.
          
          Argumentos:
          n_hidden: Número de capas escondidas
          n_layers: Número de capas
          drop_prob: Dropout layer para prevenir overfitting
          lr = Learning Rate/ Velocidad de apredizaje
        """
        
        self.drop_prob = drop_prob
        self.n_layers = n_layers
        self.n_hidden = n_hidden
        self.lr = lr
        
        # creating character dictionaries
        self.chars = tokens
        self.int2char = dict(enumerate(self.chars))
        self.char2int = {ch: ii for ii, ch in self.int2char.items()}
        
        ## TODO: define the LSTM
        self.lstm = nn.LSTM(len(self.chars), n_hidden, n_layers, 
                            dropout=drop_prob, batch_first=True)
        
        ## TODO: define a dropout layer
        self.dropout = nn.Dropout(drop_prob)
        
        ## TODO: define the final, fully-connected output layer
        self.fc = nn.Linear(n_hidden, len(self.chars))
      
    
    def forward(self, x, hidden):
        ''' Avanzar a través de la red
            Los inputs son x, y el estado de hidden/cell `hidden`. '''
                
        # Obtener los outputs del nuevo estado de hidden del LSTM
        r_output, hidden = self.lstm(x, hidden)
        
        # Avanzar a travês del la capa de dropout
        out = self.dropout(r_output)
        
        # Apilar los outputs del LSTM usando 'view'
        # y 'contiguous' para cambiar la forma del output
        out = out.contiguous().view(-1, self.n_hidden)
        
        # Pasar x a travês de la capa fully-connected
        out = self.fc(out)
        
        # Regresar el output final y el estado de hidden
        return out, hidden
    
    
    def init_hidden(self, batch_size):
        ''' Inicia el estado de hidden'''
        # Crear dos Tensors nuevos con los sizes de n_layers x batch_size x n_hidden,
        # iniciar en zero, para el estado de hidden y cell del LSTM
        weight = next(self.parameters()).data
        
        if (entrenar_en_gpu):
            hidden = (weight.new(self.n_layers, batch_size, self.n_hidden).zero_().cuda(),
                      weight.new(self.n_layers, batch_size, self.n_hidden).zero_().cuda())
        else:
            hidden = (weight.new(self.n_layers, batch_size, self.n_hidden).zero_(),
                      weight.new(self.n_layers, batch_size, self.n_hidden).zero_())
        
        return hidden
```

## Hora de Entrenar!

La función '*train*' (entrenar) nos da la opción de definir el número de epochs, la velocidad de aprendizaje, y otros parámetros.

Utlizaremos el Adam Optimizer y Cross Entropy Loss. Calcularemos la perdida y haremos retro-propagación.

Algunos detalles a considerar:

*   En el loop del lote, separaremos el estado escondido de su historia y lo modificaremos para que su valor sea igual a una variable en un nuevo *tuple* por que el LSTM tiene un estado escondido que es un tuple con los valores de los estados de escondido en cells.
*   Usaremos `clip_grad_norm` para prevenir que los gradients 'exploten'. 




```python
def train(net, data, epochs=10, batch_size=10, seq_length=50, lr=0.001, clip=5, val_frac=0.1, print_every=10):
    ''' Entrenar la red
    
        Argumentos:
            
        net: Red CharRNN 
        data: Texto usado para entrenar la red
        epochs: Número de epochs a entrenar
        batch_size: Número de mini-sequencias por mini-batch
        seq_length: Número de pasos de cáracter por mini-batch
        lr: Velocidad de aprendizaje
        clip: Recorte de gradient
        val_frac: Fracción de datos que seran separados para usar en validación
        print_every: Número de pasos en los que mostraremos los valores de pérdida en entrnamiento y validación
    
    '''
    net.train()
    
    opt = torch.optim.Adam(net.parameters(), lr=lr)
    criterion = nn.CrossEntropyLoss()
    
    # Crear datos para entranmiento y validación
    val_idx = int(len(data)*(1-val_frac))
    data, val_data = data[:val_idx], data[val_idx:]
    
    if(entrenar_en_gpu):
        net.cuda()
    
    counter = 0
    n_chars = len(net.chars)
    for e in range(epochs):
        # Inicial el estado de hidden
        h = net.init_hidden(batch_size)
        
        for x, y in get_batches(data, batch_size, seq_length):
            counter += 1
            
            # Codificar One-hot los datos y convertirlos en Torch tensors
            x = one_hot_encode(x, n_chars)
            inputs, targets = torch.from_numpy(x), torch.from_numpy(y)
            
            if(entrenar_en_gpu):
                inputs, targets = inputs.cuda(), targets.cuda()

            # Crear nuevas variables para el hidden state, de lo contrario
            # retro-propagaremos toda la historia de entrenamiento
            h = tuple([each.data for each in h])

            # Gradients acumuladas en zero
            net.zero_grad()
            
            # Obtener el output del modelo
            output, h = net(inputs, h)
            
            # Calcular la pérdida y realizar retro-propogación
            loss = criterion(output, targets.view(batch_size*seq_length))
            loss.backward()
            # `clip_grad_norm` nos ayuda a prevenir el problema de 'exploding gradient' típico en RNNs / LSTMs.
            nn.utils.clip_grad_norm_(net.parameters(), clip)
            opt.step()
            
            # Estadísticas en Pérdidas
            if counter % print_every == 0:
                # Obtener la pérdida en validación
                val_h = net.init_hidden(batch_size)
                val_losses = []
                net.eval()
                for x, y in get_batches(val_data, batch_size, seq_length):
                    # Codificar One-hot encode los datos y convertirlos en Torch tensors
                    x = one_hot_encode(x, n_chars)
                    x, y = torch.from_numpy(x), torch.from_numpy(y)
                    
                    # Crear nuevas variables para el hidden state, al contrario
                    # retro-propagaremos toda la historia de entrenamiento
                    val_h = tuple([each.data for each in val_h])
                    
                    inputs, targets = x, y
                    if(entrenar_en_gpu):
                        inputs, targets = inputs.cuda(), targets.cuda()

                    output, val_h = net(inputs, val_h)
                    val_loss = criterion(output, targets.view(batch_size*seq_length))
                
                    val_losses.append(val_loss.item())
                
                net.train() # Cambiar a train mode despues de iterar a través de los datos de  validación                
                print("Epoch: {}/{}...".format(e+1, epochs),
                      "Step: {}...".format(counter),
                      "Loss: {:.4f}...".format(loss.item()),
                      "Val Loss: {:.4f}".format(np.mean(val_losses)))
```


```python
# Definir y mostrar la red
n_hidden = 512
n_layers = 2

net = CharRNN(chars, n_hidden, n_layers)
print(net)
```

    CharRNN(
      (lstm): LSTM(88, 512, num_layers=2, batch_first=True, dropout=0.5)
      (dropout): Dropout(p=0.5)
      (fc): Linear(in_features=512, out_features=88, bias=True)
    )



```python
batch_size = 128
seq_length = 100
n_epochs = 20 # Empezar con pocos epochs si solo queremos  comprobar el comportamiento de la red 

# Entrenar el modelo
train(net, codificado, epochs=n_epochs, batch_size=batch_size, seq_length=seq_length, lr=0.001, print_every=10)
```

    Epoch: 1/20... Step: 10... Loss: 3.1425... Val Loss: 3.0601
    Epoch: 1/20... Step: 20... Loss: 3.0525... Val Loss: 2.9922
    Epoch: 1/20... Step: 30... Loss: 3.0246... Val Loss: 2.9815
    Epoch: 1/20... Step: 40... Loss: 3.0168... Val Loss: 2.9799
    Epoch: 1/20... Step: 50... Loss: 3.0222... Val Loss: 2.9760
    Epoch: 2/20... Step: 60... Loss: 3.0107... Val Loss: 2.9747
    Epoch: 2/20... Step: 70... Loss: 2.9995... Val Loss: 2.9712
    Epoch: 2/20... Step: 80... Loss: 2.9981... Val Loss: 2.9634
    Epoch: 2/20... Step: 90... Loss: 2.9897... Val Loss: 2.9458
    Epoch: 2/20... Step: 100... Loss: 2.9237... Val Loss: 2.9066
    Epoch: 2/20... Step: 110... Loss: 2.8630... Val Loss: 2.8131
    Epoch: 3/20... Step: 120... Loss: 2.7786... Val Loss: 2.7101
    Epoch: 3/20... Step: 130... Loss: 2.6624... Val Loss: 2.5798
    Epoch: 3/20... Step: 140... Loss: 2.5254... Val Loss: 2.4647
    Epoch: 3/20... Step: 150... Loss: 2.4574... Val Loss: 2.3905
    Epoch: 3/20... Step: 160... Loss: 2.3795... Val Loss: 2.3302
    Epoch: 3/20... Step: 170... Loss: 2.3533... Val Loss: 2.2900
    Epoch: 4/20... Step: 180... Loss: 2.3228... Val Loss: 2.2581
    Epoch: 4/20... Step: 190... Loss: 2.3195... Val Loss: 2.2505
    Epoch: 4/20... Step: 200... Loss: 2.2577... Val Loss: 2.2125
    Epoch: 4/20... Step: 210... Loss: 2.2460... Val Loss: 2.1785
    Epoch: 4/20... Step: 220... Loss: 2.2113... Val Loss: 2.1514
    Epoch: 5/20... Step: 230... Loss: 2.1920... Val Loss: 2.1279
    Epoch: 5/20... Step: 240... Loss: 2.1626... Val Loss: 2.1041
    Epoch: 5/20... Step: 250... Loss: 2.1420... Val Loss: 2.0820
    Epoch: 5/20... Step: 260... Loss: 2.1125... Val Loss: 2.0618
    Epoch: 5/20... Step: 270... Loss: 2.0837... Val Loss: 2.0487
    Epoch: 5/20... Step: 280... Loss: 2.0884... Val Loss: 2.0260
    ...
    ...
    ...
    Epoch: 18/20... Step: 1000... Loss: 1.4956... Val Loss: 1.4810
    Epoch: 18/20... Step: 1010... Loss: 1.5043... Val Loss: 1.4802
    Epoch: 18/20... Step: 1020... Loss: 1.5053... Val Loss: 1.4753
    Epoch: 19/20... Step: 1030... Loss: 1.4914... Val Loss: 1.4740
    Epoch: 19/20... Step: 1040... Loss: 1.5201... Val Loss: 1.4681
    Epoch: 19/20... Step: 1050... Loss: 1.4710... Val Loss: 1.4663
    Epoch: 19/20... Step: 1060... Loss: 1.4651... Val Loss: 1.4623
    Epoch: 19/20... Step: 1070... Loss: 1.4798... Val Loss: 1.4612
    Epoch: 19/20... Step: 1080... Loss: 1.4772... Val Loss: 1.4586
    Epoch: 20/20... Step: 1090... Loss: 1.4229... Val Loss: 1.4561
    Epoch: 20/20... Step: 1100... Loss: 1.4444... Val Loss: 1.4541
    Epoch: 20/20... Step: 1110... Loss: 1.4557... Val Loss: 1.4498
    Epoch: 20/20... Step: 1120... Loss: 1.4478... Val Loss: 1.4476
    Epoch: 20/20... Step: 1130... Loss: 1.4762... Val Loss: 1.4442
    Epoch: 20/20... Step: 1140... Loss: 1.4559... Val Loss: 1.4435


## Obtener el mejor modelo

Si queremos ajustar los híper-parámetros para que nos den una mejor performance, debemos mirar las pérdidas en entrenamiento y validación. Si las pérdidas de entrenamiento son mucho menores a las pérdidas de validación-- estamos *overfitting*. Para rectificar, podemos incrementar regularización (dropout) o usar un red mas pequeña. Al contrario, si las pérdidas de entrenamiento y validación son similares,  estamos *underfitting* entonces podemos incrementar el tamaño de nuestra red.


## Híper-parámetros

Estos son los híper-parámetros de nuestra red.

Cuando definimos  el modelo:

*   `n_hidden` -- número de unidades en las capas escondidas.
*   `n_layers` -- número de capas escondidas de LSTM a usar.

Probabilidades de dropout y velocidad de apredizaje estan en sus valores default.

Cuando entrenamos el modelo:

*   `batch_size` -- número de sequencias que pasan por la red en cada paso.
*   `seq_length` -- número de cáracteres en la sequencia que la red esta siendo entrenada. Típicamente, mientra la red es más grande es mejor. La red aprenderá dependencias de largo rango. Pero tomará mucho mas tiempo entrenarla. Cien es un buen número en este paso.
* `lr` -- velocidad de apredizaje.







## Punto de Control

Después del entrenamiento, es posible guardar el modelo para poder  cargarlo déspues si es necesario. 
En este ejemplo guardaremos los parámetros necesarios para crear la misma arquitectura de nuestra red, los híper-parámetros, capas, y cáracteres.


```python
# Cambiar el nombre, para guardar multiples archivos
model_name = 'rnn_20_epoch.net'
checkpoint = {'n_hidden':net.n_hidden,
              'n_layers':net.n_layers,
              'state_dict':net.state_dict(),
              'tokens':net.chars}

with open(model_name, 'wb') as f:
    torch.save(checkpoint, f)
```

## Predicciones

Ahora que tenemos el modelo entrenado, podemos usarlo para hacer predicciones. Para hacer esto, pasamos un cáracter a la red para que esta haga la predicción del siguiente cáracter. Repetimos este proceso hasta generar una buena cantidad de texto.


```python
def predict(net, char, h=None, top_k=None):
    '''
      Dado un cáracter, predecir el siguiente cáracter
      Regresa el predicho cáracter y el hidden state
      '''
    
    # Tensor inputs
    x = np.array([[net.char2int[char]]])
    x = one_hot_encode(x, len(net.chars))
    inputs = torch.from_numpy(x)
    
    if (entrenar_en_gpu):
        inputs = inputs.cuda()
        
        # Separar el hidden state de su historia
        h = tuple(each.data for each in h)
        # Obtener el output del modelo
        out, h = net(inputs, h)
        
        # Obtener las probabilidades del cáracter
        p = F.softmax(out, dim = 1).data
        if (entrenar_en_gpu):
            p = p.cpu() # pasar al CPU
            
        # Obtener top cáracters
        if top_k is None:
            top_ch = np.arange(len(net.chars))
        else:
            p, top_ch = p.topk(top_k)
            top_ch = top_ch.numpy().squeeze()
        
        # Obtener el siguiente cáracter mas probable con ago de aleatoriedad
        p = p.numpy().squeeze()
        char = np.random.choice(top_ch, p = p/p.sum())
        
        # Regresar el valor codificado del cáracter predicho y el hidden state 
        return net.int2char[char], h
        
            
    
```

## Crear una muestra y generar texto

Idealmente, debemos crear una muestra en la red para crear el 'hidden state'. De otra manera, la red comenzará a generar cáracteres de manera aleatoria.  
Usualmente, los primeros cáracteres son un poco torpes por que la red todavía no a construido una larga lista de cáracteres de la cual pueda predecir. 


```python
def sample(net, size, prime = 'El', top_k = None):
    if (entrenar_en_gpu):
        net.cuda()
    else:
        net.cpu()
        
    net.eval() # poner la red in modo de evaluación
    
    # Primero, pasar a través del cáracter preparado
    chars = [ch for ch in prime]
    h = net.init_hidden(1)
    for ch in prime:
        char, h = predict(net, ch, h, top_k = top_k)
    
    chars.append(char)
    
    # Ahora,  pasar el cáracter previo y obtener un nuevo
    for ii in range(size):
        char, h = predict(net, chars[-1], h, top_k = top_k)
        chars.append(char)
        
    return ''.join(chars)   
    
```


```python
print(sample(net, 1000, prime='Anthony', top_k=5))
```

    Anthony el cieno a los cretolas de la casa eran el acostorno, y los cuantos en la caleza de paladas, porque soporado por el mundo de su padre. Al preginto y luego de concura de la mana de su mujer, su esconte se desprocharan la palabre, el ciero..
    El 
    tamano, y sabía en el carato con sun derenciante, y se entaban en lar asindos de la 
    pusa a todo las manos año desde la 
    acuerde. Las consenciantas de sue 
    compaño con la ciana 
    pertaban de la mado con el calávir. Lo encontraba a el compañororo. 
    -No para la mañana dentro de caba dos distamentes de la pasa, para el patio de la carado, y la mano, pero no hubiera decidioron las compres del contraño y la 
    parede con un pramos de sus hordas de cullurada en una porembiendo, como el mando ero un caso de su halga excantar las amanes, y la pronte con las patoles que no estaban años antes de las canacersa de las mismos para el coronel Aureliano Buendía lo dejo al 
    momendo a lechas por el díse de luegros 
    de la mujer, pero encontró el domario que no era pr


## Cargar el Punto de Control




```python
# Cargar el modelo que entrenamos y gurdamos previamente: `rnn_20_epoch.net`
with open('rnn_20_epoch.net', 'rb') as f:
    checkpoint = torch.load(f)
    
loaded = CharRNN(checkpoint['tokens'], n_hidden=checkpoint['n_hidden'], n_layers=checkpoint['n_layers'])
loaded.load_state_dict(checkpoint['state_dict'])
```


```python
# Generar texto
print(sample(loaded, 3000, top_k=5, prime="Y el dijo: "))
```

    Y el dijo: 
    -No se le pesió, por entoreles que el padre 
    Amaranta los humado en que la calle el padie 
    su hurmiero. Pera ella los heranes sin ponos con como dincurar en el 
    cualtito. Pentra Coter la mierta del calabro, y le procurió en la casa de calle en la marra de liger 
    a la patra de las pruelas con sus maricias de 
    los mandolos de la conversión, presondía en la casa de 
    los cuerros de la cuerda y cuando se los pueron, y en 
    contentrarle a la muerte, y lo decierdo de las cosas de sus pellites y sin embarios, peso a la mano. 
    Sólo, y las pantales, el calor y el día en la pierna. En los desegrados encendado, pero el palor. Los 
    alguios de 
    la pendar. Amaranta a los carajos de 
    cama de acabillas. El pueblo decorios en la 
    aludancia y almanzó en su carta, y llevaba a la premonidad de amaneras de convanel, para si minicas 
    en la muerte y estaba, sientra de cuardo en sus puebros de labre. Aulescon se le dijo, sabieron en la casta, 
    por una mujo que le había premundo el amor la partera comersa que había parecido a su misiario, lo 
    muerte, conseguró las preseras, y sen entontes en su procosaria. La cina de las cortualles, y la 
    cinción de la prameda casa de la mano a cuando el mienterio de sus procos pesos de los compros desdeles al conterto del albanto, y se escambaba la pullir de su paricientos y los mismos descuando en las maridas de cuerre. 
    -Así qui esticira en un poco sin muy concuerdo, y los 
    alimperes a cantarlo a sabal desprevillidos. Es encontraro la ciera de la cuella y estaba encontró el cisto de acordar las 
    pareciados desde que nadie la mujer de 
    la puerta del cartito, y le había de cuadra la paleca del damino de las cosas dinabres, lo había de sus mujureros, y le decoritaron a 
    la pendia, y ella entendiendo con los meses. En la casa, y lo dijo que no estaba en el dormitorio. La misma decía a sus comprendos. En ela de la pariel y se sentía en un cina 
    esta dos mediores y con el cargano ellos, sel ponque en un coronel 
    Meme sin 
    muerte en solo de la cual de amar llevó con su humiento. Pon 
    pare que lo había dispulido a llagurla a cercas de si se este apreventiral desdu sus aposas y las malas 
    después. Estaba pristo de caballes, contrabieron. 
    El coronel Aureliano, en las presegantes. Era un calor a su 
    coronel Grincedo 
    de 
    su cuarto. Aureliano Segundo en la 
    colla de la puerta de la muerda, por la casa de acardarse, y los hijos, sino propesas de asu abrento en un trandimiento de cerra del muerto, las almigrates, porque la consuguir de la vencidad y 
    explicaban la ver a la pertinidad, pero solo en la mana, y su parre del pordero de 
    la ver en las 
    calles y como del discertido de 
    cuande estaba la casa. El cuarto y antes compariós de su pasa de las para del convillaroror de la casa de la misma cuenda de su hermano y cuando se era 
    cuenta de que llevaba los mardes armanos en la mano de los precosos para que le 
    semana en la cuerta, el prando en la cinco de calonas por el coronel Aureliano Buendía en la casa de la casa. El coronel Aureliano Buendia. 

