---
title: "Loading .csv and Excel files"
date: 2018-10-22
tags: [data science, data visualizations]
mathjax: "True"
---
{ % include adsense.html % }

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

## To combine two or more dataframes we can use 'pd.concat' which will concatenate or "stack" the dataframes vertically.

```python
	pd.concat([df1, df2, df3])
```

## We can also use  **broadcasting** to add new columns to our data frames.

```python
	df1['New Column Name'] = 'Value'

```

## To automatically read and concatename three excel spread sheets

```python
	# Create the pd.ExcelFile() object
	xls = pd.ExcelFile('file-name.xlsx')

	# Extract the sheet names from xls
	sheetnames = xls.sheet_names

	# create an empty list: listings
	data = []

	# Import the data
	for names in sheetnames:
    	df = pd.read_excel(xls, sheetname=shetnames, na_values='n/a')
    	df['New Colum Name'] = names
    	data.append(df)

	# Concatenate the listings: df1
	df1 = pd.concat(df)

	# Inspect the results
	df1.info()
	print(df1.head())
```