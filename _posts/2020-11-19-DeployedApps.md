---
title: "Deployed Web Apps"
date: 2020-11-13
tags: [ML&AI]
excerpt: "Links to Deployed Web Apps"
mathjax: "True"
---

Below are the links to some apps I created and deployed to the web. 
These apps have been coded in Visual Studio Code, in python-- using libraries such as flask, bokeh, Streamlit, TensorFlow, just to name a few and have been deployed using git and the Heroku CLI.

It might take a few seconds to boot up when accessing for the very first time but, I swear they work :)


## Data Exploration and Correlation Finder

This app takes a timeseries dataset from the user and does teh following:
*   Provides descriptive statistics about a variable from the dataset, plots data using a line chart and a distribution chart.
*   Uses statsmodels to decompose the timeseries. We can select a variabe to decompose, and it will return the trend, seasonality and error which are underlying components of timeseries data.
*   Calculates the correlation between variables in the entire dataset and it plots a distribution matrix heatmap. 


## Mushroom Classifier
Are mushrooms edible or poisonous?
This app uses a dataset which contains certain mushroom characteristics and classify them using one of the following classifiers that can be selected by the user:
*   Support Vector MAchines SVM
*   Logistic Regression
*   Random Forest

[Find the Mushroom Classifier App here](https://binaryclassifiermushroom.herokuapp.com/)


## Uber Pickups in NYC
This apps analyzes Uber pickups in New York City, groups pickups hourly and plots the location of the picups in a map.
[Uber Pickups NYC App link](https://dataexplorerlit.herokuapp.com/)

## TaskMaster
This is a to-do list app created using Flask. 

[To-Do App -- made with Flask](https://flaskappintro.herokuapp.com/)

## StreamlitApp

Proof of Concept App to test Streamlit and deployment using Heroku.

[Streamlit & Heroku App -- Proof of Concept](https://streamlitapp.herokuapp.com/)

## Bokeh Dashboard

Proof of Concept App to test deployment of bokeh graphs to the web which enables the creation of dashboards that can be deployed, distributed and access in the open web.
The interactive graphs show fiancial data, closing prices of a certain stocks-- to be specific. 

[Bokeh Graphs/Dashboard Proof of Concept](https://staticbokehplot.herokuapp.com/)