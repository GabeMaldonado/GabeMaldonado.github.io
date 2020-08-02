---
title: "AI for Medical Diagnosis - Lab 4"
date: 2020-08-02
tags: [AIforMed]
excerpt: "AI for Medical Diagnosis"
mathjax: "True"
---

## Patient Overlap and Data Leakage

We saw in the *Concepts* post that having mulitple records of the same patient in the training, validation and/or test  datasets can affect our model's performance. In Machine Learning this issue is called ***Data Leakage***

In this notebook we will identify and remove the patient overlap records from the training and validation datasets. 

```python

# Import required libraries

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
import os
import seaborn as sns
sns.set()

# Load training .csv file

train_df = pd.read_csv("/content/train-small.csv")

# Show number of columns and rows in the df (shape)

print(f"The number of rows: {train_df.shape[0]} and number of columns: {train_df.shape[1]}\n")

# print first 5 rows (head)

train_df.head()

```
`The number of rows: 1000 and number of columns: 16`

<table border="1" class="dataframe">
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

```python
# Load validation .csv file

valid_df = pd.read_csv("/content/valid-small.csv")

# Show number of rows and columns

print(f"Number of rows: {valid_df.shape[0]} and number of columns: {valid_df.shape[1]}. \n")

# print df's head

valid_df.head()
```
`Number of rows: 109 and number of columns: 16. `

<table border="1" class="dataframe">
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
      <td>00027623_007.png</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>27623</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00028214_000.png</td>
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
      <td>28214</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00022764_014.png</td>
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
      <td>22764</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00020649_001.png</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>20649</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00022283_023.png</td>
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
      <td>22283</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>

## Extract and compare the PatientIDs from both datasets. 

To do: 

*   Extract the PatientID from train_df and valid_df
*   Convert these arrays into ```set()``` datatypes
*   Identify patient overlap where the two dfs intersect

```python
# Extract PatientIDs from train_df

ids_train = train_df.PatientId.values

# Extract PatientIDs from valid_df

ids_valid = valid_df.PatientId.values
```
```python
# Create a set() data structure for the two PatientID's

ids_train_set = set(ids_train)

# Print number of unique IDs for train_df

print(f"The number of unique IDs in the train_df are: {len(ids_train_set)}. \n")

ids_valid_set = set(ids_valid)

# Print number of unique IDs for valid_df

print(f"The number of unique IDs in the valid_df are: {len(ids_valid_set)}")
```
`The number of unique IDs in the train_df are: 928. `

`The number of unique IDs in the valid_df are: 97`

```python
# Identify the overlapping records by looking at the intersection of both sets

patient_overlap = list(ids_train_set.intersection(ids_valid_set))

# Get number of overlapping records

n_overlap = len(patient_overlap)

print(f"The number of overlapping records are: {n_overlap}\n")
print(f"These PatientIDs are present in both sets: {patient_overlap}")
```

`The number of overlapping records are: 11`
`These PatientIDs are present in both sets: [20290, 27618, 9925, 10888, 22764, 19981, 18253, 4461, 28208, 8760, 7482]`

Alright! Now that we identified how many and which records are present in both, the training and validation sets, we can proceed to:

*   Find the indices of the overlapping IDs and store them in a list
*   Drop the overlapping records from either set

```python
# Create empty lists

train_overlap_idx = []
valid_overlap_idx = []

# Find indices of overlapping records

for idx in range(n_overlap): # We need to find 11 indices
  train_overlap_idx.extend(train_df.index[train_df['PatientId'] == patient_overlap[idx]].tolist())
  valid_overlap_idx.extend(valid_df.index[valid_df['PatientId'] == patient_overlap[idx]].tolist())

# print info about indices

print(f"Indices of the overlapping PatientIDs in the train_df: \n{train_overlap_idx}\n")
print(f"Indices of the overlapping PatientIDs in the valid_df: \n{valid_overlap_idx}\n")

```

```
Indices of the overlapping PatientIDs in the train_df: 
[306, 186, 797, 98, 408, 917, 327, 913, 10, 51, 276]
```

```
Indices of the overlapping PatientIDs in the valid_df: 
[104, 88, 65, 13, 2, 41, 56, 70, 26, 75, 20, 52, 55]
```

```python

# Drop overlapping rows/records from either one of the sets, validation in this case

valid_df.drop(valid_overlap_idx, inplace = True)
```

We can ensure that things were done correctly by re-running the PatientID comparison between the two datasets. If everything executed above went well:
*  We should now see less records in the valid_df
*  We should see 0 overlaps as both dfs no longer intersect each other

```python
# Extract PatientsIDs from the valid_df

ids_valid_check = valid_df.PatientId.values

# Create a set datatype 

ids_valid_check_set = set(ids_valid_check)

# print number of unique ID's

print(f"Number of unique PatientIds in valid_df: {len(ids_valid_check_set)}")
```

```python
# Identify overlap by comparing the two dfs

patient_overlap_check = list(ids_train_set.intersection(ids_valid_check_set))

# Get number of overlapped records

n_overlap_check = len(patient_overlap_check)

print(f"The number of overlapped PatientIDs in both datasets are: {n_overlap_check}")
```

`The number of overlapped PatientIDs in both datasets are: 0`




