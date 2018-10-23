---
title: "Loading .csv and Excel files"
date: 2018-10-22
tags: [data science, data visualizations]
mathjax: "True"
---

# Loading .csv files

```python
	
	# Import pandas
	import pandas as pd

	# Import the data

	df = pd.read_csv('file-name.csv')

	# Display the first 5 rows

	print (df.head())

```

## Loading .csv files containing date-time-series data such as stock data

```python
	
	# We are handling missing values by passing na_values='NAN'

	df = pd.read_csv('file-name.csv', na_values='NAN', parse_dates=['Last Update'])

```  

# Loading Excel files

To load data in excel files we can use the pd.read_excel and pass the sheet 
name, if known, to 'sheetname' otherwise 'sheetname=0' 

```python
	
	df = pd.read_excel('excel-file.xlsx', sheetname='active-sheet-name', na_values='n/a')
	
```

## Loading data form two excel sheets

```python

	# First create an ExcelFile object

	xls_data = pd.ExcelFile('file-name.xlsx')

	# Retrieve sheet names

	names = xls.sheet_names

	# Create a dictionary with all the sheet names

	name_of_sheets = pd.read_excel(xls, sheetname=names, na_values='n/a')


```