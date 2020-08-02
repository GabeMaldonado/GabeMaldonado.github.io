---
title: "AI for Medical Diagnosis - Lab 2"
date: 2020-08-01
tags: [AIforMed]
excerpt: "AI for Medical Diagnosis"
mathjax: "True"
---

### Counting Labels

**Class Imbalance** can affect the loss function as it weights the losses different for each class. To choose the weights we must first calculate the class frequencies. 

```python
# Import required libraries

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns


# Read in csv file into a df

train_df = pd.read_csv('/content/train-small.csv')

# Display first 5 elements of the df

train_df.head()
```
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
# Create a new df to count classes and drop non-class columns 

class_counts = train_df.sum().drop(['Image', 'PatientId'])
class_counts
```

```
Atelectasis           106
Cardiomegaly           20
Consolidation          33
Edema                  16
Effusion              128
Emphysema              13
Fibrosis               14
Hernia                  2
Infiltration          175
Mass                   45
Nodule                 54
Pleural_Thickening     21
Pneumonia              10
Pneumothorax           38
dtype: object
```

```python
# Print class counts more descriptively

for c in class_counts.keys():
  print(f"The class {c} has {train_df[c].sum()} samples.\n")
  
print(f"For a total of: {class_counts.values.sum()} samples.")
```

```
The class Atelectasis has 106 samples.

The class Cardiomegaly has 20 samples.

The class Consolidation has 33 samples.

The class Edema has 16 samples.

The class Effusion has 128 samples.

The class Emphysema has 13 samples.

The class Fibrosis has 14 samples.

The class Hernia has 2 samples.

The class Infiltration has 175 samples.

The class Mass has 45 samples.

The class Nodule has 54 samples.

The class Pleural_Thickening has 21 samples.

The class Pneumonia has 10 samples.

The class Pneumothorax has 38 samples.

For a total of: 675 samples.
```

### Data Visualization

Plot the Distribution of Counts

```python
sns.set()
sns.barplot(class_counts.values, class_counts.index, palette="Blues_d")
plt.title("Distribution of Classes for Training Dataset", fontsize=15)
plt.xlabel("Number of Patients", fontsize=15)
plt.ylabel("Diseases", fontsize=15)
plt.show();
```
![Plot Dist of Counts](data:image/png;base64,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xPbt29m4cSNGRkZ4eXkRGBjIhAkTADh//jxbtmzBxMQEDw8PIiMjcXd3L+SjFkIIUVCShItQTsPRL6tRo0YEBwezYMECmjdvTuvWrbOtc+zYMbp164ax8dMr8dzd3Zk3b56yvHXr1piamgLQsGFDrl+/XiixCSGEeDlyn3AJoqenp1Yd6flSg40bNyY8PJz69esTERHBxx9/rHH7z18k9nyZQyGEENohSbgEqVy5MmlpacTExACwY8cOZVlsbCzGxsZ0796dyZMn89dff5GZmam2fcuWLdm9ezeJiYlkZWWxZcsWWrVqVazHIIQQouBkOLoI5VSyMC96enpMmTKFoUOHUrFiRdq3b68s+/333wkODkZHR4fMzExmzpyJjo76d6h27doRFRVFv379AKhfvz6jRo0qvAMSQghRqGTGLKERmaxDiJJrf+DkEj8blcyY9cLylw1KCCGEEK9GesJCCPGakLmji4bMHS1KjNJYT/hN+0+vTaUx7tIYM5TeuIW6Vx6O/vvvv9m7dy+3b98ujHiEEEKIN4ZGPeFp06YBMGvWLAB27drFhAkTyMjIoFy5cqxevZr333+/8KMUJUZewyqvKjkljYT45CJrXwghShqNkvDhw4cZN26c8tjPz4/u3bszYcIEZs+ejZ+fH99//32hBylKjoHz1nH7v6IZAvtl0SgSkCQshHhzaDQcff/+fd566y0Arl27RkxMDJ988gnm5ub07duXixcvFkmQQgghxOtIo55w+fLluXfvHgBHjx6lcuXKytzIWVlZpWoaxNzq/b7zzjuv3PaJEydYsGABYWFhr9yWEEKI15dGSbht27b4+/tz//59Vq9erVYD98qVK1StWrXQAyxKhVlgQQghhNCURsPRkyZNolGjRmzcuJGmTZsyevRoZdkvv/xCmzZtCj3A4mZjY8M333xD79696dixI8eOHcPX1xcXFxd69OjB33//DTzt7fbs2ZOJEyfSvXt33NzcuHr1qtJORkYG06ZNw8nJiZ49eyrbjRgxgt27dyvr7dmzh2HDhgGwfPlyunTpgrOzMy4uLsTHxwPw559/MmjQIFxdXXF1deXgwYPA03rD9vb2SnxdunTh/PnzTJ06FScnJ/r06cPdu3cBiIqK4qOPPqJXr15069ZNKYkohBBCezRKwiYmJvj4+BAZGcmiRYswMTFRloWEhCh1a0uL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%0A)

## Weighted Loss Function

Define a hypothetical set of true labels and then a set of random predictions. These samples can then be used to calculate the weighted loss function.

```python
# Generate an np array of 10 labels
# 7 positive and 3 negative -- then reshape array to a column

y_true = np.array([1, 1, 1, 1, 1, 1, 1, 0, 0, 0]).reshape(10, 1)
print(y_true, y_true.shape)
```
```
[[1]
 [1]
 [1]
 [1]
 [1]
 [1]
 [1]
 [0]
 [0]
 [0]] (10, 1)
```

Define positive and negative weights to be used in the loss function
The positive weight is determined by the number of negative cases over the total number of cases: $$3 / 10$$

The negative weight is determined by the number of positive cases over the total number of cases: $$7 / 10$$

We also need to define the value of *epsilon* which is a small positive value we used to prevent erros when calculating the $$log$$ of zero.

```python
# Define positive and negative weights

positive_weight = 3/10

negative_weight = 7/10

# Define epsilon

epsilon = 1e-7
```

### Weighted Loss Equation
Calculate the loss for the zero-th label (column at index 0)

- The loss is made up of two terms:
    - $loss_{pos}$: we'll use this to refer to the loss where the actual label is positive (the positive examples).
    - $loss_{neg}$: we'll use this to refer to the loss where the actual label is negative (the negative examples).  
- Note that within the $log()$ function, we'll add a tiny positive value, to avoid an error if taking the log of zero.

$$ loss^{(i)} = loss_{pos}^{(i)} + los_{neg}^{(i)} $$

$$loss_{pos}^{(i)} = -1 \times weight_{pos}^{(i)} \times y^{(i)} \times log(\hat{y}^{(i)} + \epsilon)$$

$$loss_{neg}^{(i)} = -1 \times weight_{neg}^{(i)} \times (1- y^{(i)}) \times log(1 - \hat{y}^{(i)} + \epsilon)$$

$$\epsilon = \text{a tiny positive number}$$

```python
# Calculate positive loss

positive_loss = -1 * np.sum(positive_weight * 
                            y_true * 
                            np.log(y_predict + epsilon)
              )

positive_loss
```

`19.436539145242033`

```python
# Calculate negative loss

negative_loss = -1 * np.sum(negative_weight * 
                            (1 - y_true) * 
                            np.log(1 - y_predict + epsilon)
              )

negative_loss
```

`1.611808725096189`

```python
# Calculate total loss 

total_loss = positive_loss + negative_loss
total_loss
```

`21.048347870338223`







