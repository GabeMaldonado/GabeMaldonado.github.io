---
title: "AI for Medical Diagnosis - Lab 1"
date: 2020-08-01
tags: [AIforMed]
excerpt: "AI for Medical Diagnosis"
mathjax: "True"
---


# Notes on AI for Medical Diagnosis --  Lab 1

## Loading and Cleaning up Data

```python

# Import packages

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns
import os

sns.set()

# Read in dataset

train_df = pd.read_csv('/content/train-small.csv')

# Print # of columns and rows

print(f'There are {train_df.shape[0]} rows and {train_df.shape[1]} columns in this dataframe')

# display first 5 elements

train_df.head()

```

<div>

<table border="1" class="dataframe" >
  <thead>
    <tr>
      <th></th>
      <th>Image</th>
      <th>Atelectasis</th>
      <th>Cardiomegaly</th>
      <th>Consolidation</th>
      <th>Edema</th>
      <th>Effusion</th>
      <th>Emphysema</th>
      <th>Fibrosis</th>
      <th>Hernia</th>
      <th>Infiltration</th>
      <th>Mass</th>
      <th>Nodule</th>
      <th>PatientId</th>
      <th>Pleural_Thickening</th>
      <th>Pneumonia</th>
      <th>Pneumothorax</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00008270_015.png</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>8270</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00029855_001.png</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>29855</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00001297_000.png</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1297</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00012359_002.png</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>12359</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00017951_001.png</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>17951</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>

```python
# Get the info for the dataframe

train_df.info()
```
<pre>&lt;class 'pandas.core.frame.DataFrame'&gt;
RangeIndex: 1000 entries, 0 to 999
Data columns (total 16 columns):
 #   Column              Non-Null Count  Dtype 
---  ------              --------------  ----- 
 0   Image               1000 non-null   object
 1   Atelectasis         1000 non-null   int64 
 2   Cardiomegaly        1000 non-null   int64 
 3   Consolidation       1000 non-null   int64 
 4   Edema               1000 non-null   int64 
 5   Effusion            1000 non-null   int64 
 6   Emphysema           1000 non-null   int64 
 7   Fibrosis            1000 non-null   int64 
 8   Hernia              1000 non-null   int64 
 9   Infiltration        1000 non-null   int64 
 10  Mass                1000 non-null   int64 
 11  Nodule              1000 non-null   int64 
 12  PatientId           1000 non-null   int64 
 13  Pleural_Thickening  1000 non-null   int64 
 14  Pneumonia           1000 non-null   int64 
 15  Pneumothorax        1000 non-null   int64 
dtypes: int64(15), object(1)
memory usage: 125.1+ KB
</pre>

## Check for unique IDs

"PatientID" has an ID number for each patient. In this dataset we need to determine if each image corresponds to a unique patient. Duplicate IDs would indicate that a single patient might have multiple images. 

```python

print(f"The total number of patients are {train_df['PatientId'].count()}, 
        from those the unique IDs are {train_df['PatientId'].value_counts().shape[0]}")
```

As we can see the number of unique patien IDs are 928 out of 1000 which indicates that there must be some overlap. For patients with multiple records, we want to make sure that they don't show up in both, the training and test datasets in order to avoid data leakage. 

### Explore data labels. 
```python

columns = train_df.keys()
columns = list(columns)
print(columns)
```

'['Image', 'Atelectasis', 'Cardiomegaly', 'Consolidation', 'Edema', 'Effusion', 'Emphysema', 'Fibrosis', 'Hernia', 
'Infiltration', 'Mass', 'Nodule', 'PatientId', 'Pleural_Thickening', 'Pneumonia', 'Pneumothorax']'

```python

# Remove unnecessary columns

columns.remove('Image')
columns.remove('PatientId')

# Get the total classes

print(f"There are {len(columns)} columns of labels for these conditions: {columns}")
```
There are 14 columns of labels for these conditions: ['Atelectasis', 'Cardiomegaly', 'Consolidation', 'Edema', 
'Effusion', 'Emphysema', 'Fibrosis', 'Hernia', 'Infiltration', 'Mass', 'Nodule', 'Pleural_Thickening', 'Pneumonia', 'Pneumothorax']

```python
# Print out the number of positives labels (1) for each class

for column in columns:
  print(f"The class {column} has {train_df[column].sum()} samples")
```
`
The class Atelectasis has 106 samples
The class Cardiomegaly has 20 samples
The class Consolidation has 33 samples
The class Edema has 16 samples
The class Effusion has 128 samples
The class Emphysema has 13 samples
The class Fibrosis has 14 samples
The class Hernia has 2 samples
The class Infiltration has 175 samples
The class Mass has 45 samples
The class Nodule has 54 samples
The class Pleural_Thickening has 21 samples
The class Pneumonia has 10 samples
The class Pneumothorax has 38 samples
`

## Data Visualization

Now we are going to visualize some of the images in the dataset

```python
images = train_df['Image'].head(10).values
images
```
`array(['00008270_015.png', '00029855_001.png', '00001297_000.png',
       '00012359_002.png', '00017951_001.png', '00001232_002.png',
       '00017135_000.png', '00027235_000.png', '00014197_007.png',
       '00011584_002.png'], dtype=object)`

```python
# Extract numpy values from the 'Image' column of the dataframe



# This is a very larger dataset and I only uploaded a handful of images to colab
# so I'm creating a list to iterate through the images

images = ['00001855_037.png', '00005132_000.png', '00009804_001.png', '00011553_006.png',
          '00012051_001.png', '00012276_018.png', '00013249_033.png', '00013615_007.png',
          '00015007_006.png', '00019967_011.png', '00028341_002.png', '00030061_000.png']


'''
Run below line if you have the whole dataset
images = train_df['Image'].head(10).values 
'''

# Extract 9 random images from df

random_images = [np.random.choice(images) for i in range(9)]

# Define location of the image dir

img_dir = '/content/images-small'

print("Display Random Images")

# Adjust size of the images

plt.figure(figsize=(20, 10))

# Iterate and plot random images

for i in range(9):
  plt.subplot(3, 3, i +1)
  img = plt.imread(os.path.join(img_dir, random_images[i]))
  plt.imshow(img, cmap='gray')
  plt.axis('off')

# Adjust subplot padding

plt.tight_layout()
```