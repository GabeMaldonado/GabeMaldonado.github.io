---
layout: archive
permalink: /data-visualizations/
title: "Data Visualizations"
author_profile: true
header:
---

<style>
img {
    display: block;
    margin-left: auto;
    margin-right: auto;
}
</style>


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





