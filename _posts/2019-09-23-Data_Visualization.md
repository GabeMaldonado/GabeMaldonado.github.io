---
title: "Examples of Visualization"
date: 2019-09-23
tags: [Data Visualization]
excerpt: "Data Vis"
mathjax: "True"
---


## Jointplots Hex

```python
	sns.jointplot(data1,data2,kind='hex')

```

<img src="/images/jointplot.png" style="width:70%">

## KDE Plots

```python
	sns.kdeplot(dframe.X,dframe.Y,shade=True)
```

<img src="/images/kdeplot.png" style="width:70%">

## KDE & Histogram Plot

```python
	
	sns.distplot(dataset,bins=25, 
            kde_kws={'color':'indianred','label':'KDE Plot'},
            hist_kws={'color':'blue', 'label':'HIST'})

```

<img src="/images/kdehist.png" style="width:70%">

## Distribution Plots

```python
	sns.distplot(ser1,bins=25)
```
<img src="/images/distplot.png" style="width:70%">







## Jointplots Hex

```python
	sns.jointplot(data1,data2,kind='hex')

```

<img src="/images/jointplot.png" style="width:70%">

## KDE Plots

```python
	sns.kdeplot(dframe.X,dframe.Y,shade=True)
```

<img src="/images/kdeplot.png" style="width:70%">

## KDE & Histogram Plot

```python
	
	sns.distplot(dataset,bins=25, 
            kde_kws={'color':'indianred','label':'KDE Plot'},
            hist_kws={'color':'blue', 'label':'HIST'})

```

<img src="/images/kdehist.png" style="width:70%">

## Distribution Plots

```python
	sns.distplot(ser1,bins=25)
```
<img src="/images/distplot.png" style="width:70%">