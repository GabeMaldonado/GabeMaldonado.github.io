---
title: "Bokeh Basics I"
date: 2020-08-12
tags: [Data Visualization]
excerpt: "Bokeh Basics I"
mathjax: "True"
---


# Bokeh Basics - I

Bokeh is a python library that enables users to create beautiful, dynamic and interactive visualizations. 

To [learn more about Bokeh visit its website](https://docs.bokeh.org/en/latest/index.html)

Want to create visualizations? Let's get started!

```python
# import required libraries

from bokeh.io import output_notebook, show, reset_output, output_file

import bokeh
from bokeh.plotting import figure

import numpy as np
import pandas as pd

# import library for toy datasets
from vega_datasets import data as vds
```

## Load Data
We need data to plot! Bokeh provides example datsets we can use.

```python
from bokeh.sampledata import iris
# load iris dataset
df_iris = iris.flowers
# display first five rows in the df
df_iris.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>sepal_length</th>
      <th>sepal_width</th>
      <th>petal_length</th>
      <th>petal_width</th>
      <th>species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
  </tbody>
</table>

```python
# To display the graphs/output we need to run `output_notebook()` once if using JupyterLab
# and in every cell that would return a graph if using Colab
output_notebook()
```

## Creating Plots

To create plots we must follow this workflow:
*   Create a figure -- 
*   Create a glyph/plot. We have several options: line, bar, scatter.
*   show plot

## Bokeh's Data Structure
Bokeh uses the ColumnDataSource as its main data structure. The ColumnDataSource is a table-like data structure that maps string column names to sequences of data (columns). The ColumnDataSource is created automatically most of the time but it can also be created explicitly by passing a pandas dataframe to the class initializer:

`data = ColumnDataSource(df)`

```python
# to create the ColumnDataSource

 from bokeh.models import ColumnDataSource

 df = ColumnDataSource({'A' : [1, 2, 3, 4, 5],
                        'B' : [5, 4, 3, 2, 1],
                        'C' : [1, 3, 5, 1, 2 ]})
 df.data

 ```
 `{'A': [1, 2, 3, 4, 5], 'B': [5, 4, 3, 2, 1], 'C': [1, 3, 5, 1, 2]}`

 
## Create a Line Plot

We can create some random data to pass as our x and y values.

```python
# plot a linear graph

from bokeh.models import HoverTool

# create toy data

x_ax = np.arange(10)
y_ax = np.random.rand(10)

# Create plot

line_plot = figure(plot_width=600, plot_height=425, title='Line Plot', x_axis_label='X', y_axis_label='Y')
line_plot.line(x_ax, y_ax, legend_label='line', line_width=2)

# add hover tool
line_plot.add_tools(HoverTool())
output_file('/line_chart.html')

show(line_plot)
```

<html lang="en">
  
  <head>
    
      <meta charset="utf-8">
      <title>Bokeh Plot</title>
      
      
        
          
        
        
          
        <script type="text/javascript" src="https://cdn.bokeh.org/bokeh/release/bokeh-2.1.1.min.js" integrity="sha384-kLr4fYcqcSpbuI95brIH3vnnYCquzzSxHPU6XGQCIkQRGJwhg0StNbj1eegrHs12" crossorigin="anonymous"></script>
        <script type="text/javascript">
            Bokeh.set_log_level("info");
        </script>
        
      
      
    
  </head>
  
  
  <body>
    
      
        
          
          
            
              <div class="bk-root" id="c8f91f15-ce7b-443f-9677-0aae413ef7d4" data-root-id="5495"></div>
            
          
        
      
      
        <script type="application/json" id="5876">
          {"516b72a7-765d-4d69-8024-cf95700b1880":{"roots":{"references":[{"attributes":{"below":[{"id":"5506"}],"center":[{"id":"5509"},{"id":"5513"},{"id":"5541"}],"left":[{"id":"5510"}],"plot_height":425,"renderers":[{"id":"5531"}],"title":{"id":"5496"},"toolbar":{"id":"5521"},"x_range":{"id":"5498"},"x_scale":{"id":"5502"},"y_range":{"id":"5500"},"y_scale":{"id":"5504"}},"id":"5495","subtype":"Figure","type":"Plot"},{"attributes":{"axis":{"id":"5510"},"dimension":1,"ticker":null},"id":"5513","type":"Grid"},{"attributes":{"label":{"value":"line"},"renderers":[{"id":"5531"}]},"id":"5542","type":"LegendItem"},{"attributes":{"axis_label":"X","formatter":{"id":"5536"},"ticker":{"id":"5507"}},"id":"5506","type":"LinearAxis"},{"attributes":{},"id":"5538","type":"Selection"},{"attributes":{"text":"Line Plot"},"id":"5496","type":"Title"},{"attributes":{"data":{"x":[0,1,2,3,4,5,6,7,8,9],"y":{"__ndarray__":"7vmAazbX2T9AMak0mhPMPxxebtc9pNY/0LFj9rgB2j/cVRitP+jUP7ACACMiWdc/mCUp97t4xD/IuxAFBwDbP6tK2D8cB+c/l16hFgB36T8=","dtype":"float64","order":"little","shape":[10]}},"selected":{"id":"5538"},"selection_policy":{"id":"5539"}},"id":"5528","type":"ColumnDataSource"},{"attributes":{"line_color":"#1f77b4","line_width":2,"x":{"field":"x"},"y":{"field":"y"}},"id":"5529","type":"Line"},{"attributes":{},"id":"5514","type":"PanTool"},{"attributes":{},"id":"5519","type":"HelpTool"},{"attributes":{"data_source":{"id":"5528"},"glyph":{"id":"5529"},"hover_glyph":null,"muted_glyph":null,"nonselection_glyph":{"id":"5530"},"selection_glyph":null,"view":{"id":"5532"}},"id":"5531","type":"GlyphRenderer"},{"attributes":{},"id":"5517","type":"SaveTool"},{"attributes":{"overlay":{"id":"5520"}},"id":"5516","type":"BoxZoomTool"},{"attributes":{},"id":"5500","type":"DataRange1d"},{"attributes":{},"id":"5534","type":"BasicTickFormatter"},{"attributes":{},"id":"5504","type":"LinearScale"},{"attributes":{"bottom_units":"screen","fill_alpha":0.5,"fill_color":"lightgrey","left_units":"screen","level":"overlay","line_alpha":1.0,"line_color":"black","line_dash":[4,4],"line_width":2,"right_units":"screen","top_units":"screen"},"id":"5520","type":"BoxAnnotation"},{"attributes":{"items":[{"id":"5542"}]},"id":"5541","type":"Legend"},{"attributes":{"axis":{"id":"5506"},"ticker":null},"id":"5509","type":"Grid"},{"attributes":{"source":{"id":"5528"}},"id":"5532","type":"CDSView"},{"attributes":{"axis_label":"Y","formatter":{"id":"5534"},"ticker":{"id":"5511"}},"id":"5510","type":"LinearAxis"},{"attributes":{"callback":null},"id":"5543","type":"HoverTool"},{"attributes":{},"id":"5507","type":"BasicTicker"},{"attributes":{},"id":"5539","type":"UnionRenderers"},{"attributes":{"line_alpha":0.1,"line_color":"#1f77b4","line_width":2,"x":{"field":"x"},"y":{"field":"y"}},"id":"5530","type":"Line"},{"attributes":{},"id":"5536","type":"BasicTickFormatter"},{"attributes":{},"id":"5502","type":"LinearScale"},{"attributes":{},"id":"5511","type":"BasicTicker"},{"attributes":{"active_drag":"auto","active_inspect":"auto","active_multi":null,"active_scroll":"auto","active_tap":"auto","tools":[{"id":"5514"},{"id":"5515"},{"id":"5516"},{"id":"5517"},{"id":"5518"},{"id":"5519"},{"id":"5543"}]},"id":"5521","type":"Toolbar"},{"attributes":{},"id":"5515","type":"WheelZoomTool"},{"attributes":{},"id":"5498","type":"DataRange1d"},{"attributes":{},"id":"5518","type":"ResetTool"}],"root_ids":["5495"]},"title":"Bokeh Application","version":"2.1.1"}}
        </script>
        <script type="text/javascript">
          (function() {
            var fn = function() {
              Bokeh.safely(function() {
                (function(root) {
                  function embed_document(root) {
                    
                  var docs_json = document.getElementById('5876').textContent;
                  var render_items = [{"docid":"516b72a7-765d-4d69-8024-cf95700b1880","root_ids":["5495"],"roots":{"5495":"c8f91f15-ce7b-443f-9677-0aae413ef7d4"}}];
                  root.Bokeh.embed.embed_items(docs_json, render_items);
                
                  }
                  if (root.Bokeh !== undefined) {
                    embed_document(root);
                  } else {
                    var attempts = 0;
                    var timer = setInterval(function(root) {
                      if (root.Bokeh !== undefined) {
                        clearInterval(timer);
                        embed_document(root);
                      } else {
                        attempts++;
                        if (attempts > 100) {
                          clearInterval(timer);
                          console.log("Bokeh: ERROR: Unable to run BokehJS code because BokehJS library is missing");
                        }
                      }
                    }, 10, root)
                  }
                })(window);
              });
            };
            if (document.readyState != "loading") fn();
            else document.addEventListener("DOMContentLoaded", fn);
          })();
        </script>
    
  </body>
  
</html>

### Creating a multi-variable line plot

```python
output_notebook()

# create some random data
x_multi = np.arange(10)
y1_multi = np.random.rand(10)
y2_multi = np.random.rand(10)
y3_multi = np.random.rand(10)

# crete instance of the plot

multi_var_plot = figure(plot_width=600, plot_height=400, toolbar_location='below')
multi_var_plot.line(x_multi, y1_multi, color='yellow', line_width=4, legend_label='y1')
multi_var_plot.line(x_multi, y2_multi, color='blue', line_width=4, legend_label='y2')
multi_var_plot.line(x_multi, y3_multi, color='red', line_width=4, legend_label='y3')
multi_var_plot.add_tools(HoverTool())

output_file('/multiline_chart.html')

show(multi_var_plot)
```

<html lang="en">
  
  <head>
    
      <meta charset="utf-8">
      <title>Bokeh Plot</title>
      
      
        
          
        
        
          
        <script type="text/javascript" src="https://cdn.bokeh.org/bokeh/release/bokeh-2.1.1.min.js" integrity="sha384-kLr4fYcqcSpbuI95brIH3vnnYCquzzSxHPU6XGQCIkQRGJwhg0StNbj1eegrHs12" crossorigin="anonymous"></script>
        <script type="text/javascript">
            Bokeh.set_log_level("info");
        </script>
        
      
      
    
  </head>
  
  
  <body>
    
      
        
          
          
            
              <div class="bk-root" id="27a42496-e4c3-48b1-a9bf-e8dd293b15ee" data-root-id="7906"></div>
            
          
        
      
      
        <script type="application/json" id="8471">
          {"565641f3-1abd-48cb-ae98-4bf5fc049d51":{"roots":{"references":[{"attributes":{"below":[{"id":"7915"}],"center":[{"id":"7918"},{"id":"7922"},{"id":"7951"}],"left":[{"id":"7919"}],"plot_height":400,"renderers":[{"id":"7940"},{"id":"7956"},{"id":"7973"}],"title":{"id":"7942"},"toolbar":{"id":"7930"},"toolbar_location":"below","x_range":{"id":"7907"},"x_scale":{"id":"7911"},"y_range":{"id":"7909"},"y_scale":{"id":"7913"}},"id":"7906","subtype":"Figure","type":"Plot"},{"attributes":{"axis":{"id":"7915"},"ticker":null},"id":"7918","type":"Grid"},{"attributes":{},"id":"7985","type":"Selection"},{"attributes":{"formatter":{"id":"7944"},"ticker":{"id":"7920"}},"id":"7919","type":"LinearAxis"},{"attributes":{"data":{"x":[0,1,2,3,4,5,6,7,8,9],"y":{"__ndarray__":"YCbQlPnw5z/cN+i8r7zfP6y0E+LBeMQ/hvRWtvlV2T88a2dbpfvpP+sKm4Gg4eE/KPDe+nBIwz+wnrPpGiG0P86wcAcez+A/APm1011XzT8=","dtype":"float64","order":"little","shape":[10]}},"selected":{"id":"7948"},"selection_policy":{"id":"7949"}},"id":"7937","type":"ColumnDataSource"},{"attributes":{},"id":"7948","type":"Selection"},{"attributes":{"source":{"id":"7970"}},"id":"7974","type":"CDSView"},{"attributes":{"active_drag":"auto","active_inspect":"auto","active_multi":null,"active_scroll":"auto","active_tap":"auto","tools":[{"id":"7923"},{"id":"7924"},{"id":"7925"},{"id":"7926"},{"id":"7927"},{"id":"7928"},{"id":"7989"}]},"id":"7930","type":"Toolbar"},{"attributes":{"line_alpha":0.1,"line_color":"yellow","line_width":4,"x":{"field":"x"},"y":{"field":"y"}},"id":"7939","type":"Line"},{"attributes":{"items":[{"id":"7952"},{"id":"7969"},{"id":"7988"}]},"id":"7951","type":"Legend"},{"attributes":{"line_alpha":0.1,"line_color":"red","line_width":4,"x":{"field":"x"},"y":{"field":"y"}},"id":"7972","type":"Line"},{"attributes":{},"id":"7920","type":"BasicTicker"},{"attributes":{"axis":{"id":"7919"},"dimension":1,"ticker":null},"id":"7922","type":"Grid"},{"attributes":{"data_source":{"id":"7970"},"glyph":{"id":"7971"},"hover_glyph":null,"muted_glyph":null,"nonselection_glyph":{"id":"7972"},"selection_glyph":null,"view":{"id":"7974"}},"id":"7973","type":"GlyphRenderer"},{"attributes":{},"id":"7949","type":"UnionRenderers"},{"attributes":{"text":""},"id":"7942","type":"Title"},{"attributes":{"line_alpha":0.1,"line_color":"blue","line_width":4,"x":{"field":"x"},"y":{"field":"y"}},"id":"7955","type":"Line"},{"attributes":{},"id":"7986","type":"UnionRenderers"},{"attributes":{"data":{"x":[0,1,2,3,4,5,6,7,8,9],"y":{"__ndarray__":"E5QacjOk5T9DLzicphfmP2AVAQJLg7Q/eBU93mbY5j8RM6xr+hvmP6Qafy/0eMs/yfnE/UKG4z8AU9LE3SvYPxTgYijmsNw/RsGE4gH+4z8=","dtype":"float64","order":"little","shape":[10]}},"selected":{"id":"7985"},"selection_policy":{"id":"7986"}},"id":"7970","type":"ColumnDataSource"},{"attributes":{"label":{"value":"y3"},"renderers":[{"id":"7973"}]},"id":"7988","type":"LegendItem"},{"attributes":{"label":{"value":"y1"},"renderers":[{"id":"7940"}]},"id":"7952","type":"LegendItem"},{"attributes":{"overlay":{"id":"7929"}},"id":"7925","type":"BoxZoomTool"},{"attributes":{"source":{"id":"7953"}},"id":"7957","type":"CDSView"},{"attributes":{},"id":"7924","type":"WheelZoomTool"},{"attributes":{},"id":"7923","type":"PanTool"},{"attributes":{"line_color":"blue","line_width":4,"x":{"field":"x"},"y":{"field":"y"}},"id":"7954","type":"Line"},{"attributes":{"source":{"id":"7937"}},"id":"7941","type":"CDSView"},{"attributes":{},"id":"7966","type":"Selection"},{"attributes":{"data":{"x":[0,1,2,3,4,5,6,7,8,9],"y":{"__ndarray__":"/gSEEn9z6D/u1CvcBqDsP/A9IpjEce8/YNzFZMYYlj+6jX0aQXfWP8DUSm5cwLI/wKU+O/dVxD9a67lC+GnYPxzgwV/JNOw/emXFkgob3T8=","dtype":"float64","order":"little","shape":[10]}},"selected":{"id":"7966"},"selection_policy":{"id":"7967"}},"id":"7953","type":"ColumnDataSource"},{"attributes":{"callback":null},"id":"7989","type":"HoverTool"},{"attributes":{},"id":"7911","type":"LinearScale"},{"attributes":{"line_color":"yellow","line_width":4,"x":{"field":"x"},"y":{"field":"y"}},"id":"7938","type":"Line"},{"attributes":{},"id":"7926","type":"SaveTool"},{"attributes":{"data_source":{"id":"7953"},"glyph":{"id":"7954"},"hover_glyph":null,"muted_glyph":null,"nonselection_glyph":{"id":"7955"},"selection_glyph":null,"view":{"id":"7957"}},"id":"7956","type":"GlyphRenderer"},{"attributes":{},"id":"7967","type":"UnionRenderers"},{"attributes":{},"id":"7927","type":"ResetTool"},{"attributes":{},"id":"7928","type":"HelpTool"},{"attributes":{},"id":"7916","type":"BasicTicker"},{"attributes":{"line_color":"red","line_width":4,"x":{"field":"x"},"y":{"field":"y"}},"id":"7971","type":"Line"},{"attributes":{"formatter":{"id":"7946"},"ticker":{"id":"7916"}},"id":"7915","type":"LinearAxis"},{"attributes":{"data_source":{"id":"7937"},"glyph":{"id":"7938"},"hover_glyph":null,"muted_glyph":null,"nonselection_glyph":{"id":"7939"},"selection_glyph":null,"view":{"id":"7941"}},"id":"7940","type":"GlyphRenderer"},{"attributes":{},"id":"7944","type":"BasicTickFormatter"},{"attributes":{},"id":"7907","type":"DataRange1d"},{"attributes":{"label":{"value":"y2"},"renderers":[{"id":"7956"}]},"id":"7969","type":"LegendItem"},{"attributes":{},"id":"7909","type":"DataRange1d"},{"attributes":{},"id":"7913","type":"LinearScale"},{"attributes":{"bottom_units":"screen","fill_alpha":0.5,"fill_color":"lightgrey","left_units":"screen","level":"overlay","line_alpha":1.0,"line_color":"black","line_dash":[4,4],"line_width":2,"right_units":"screen","top_units":"screen"},"id":"7929","type":"BoxAnnotation"},{"attributes":{},"id":"7946","type":"BasicTickFormatter"}],"root_ids":["7906"]},"title":"Bokeh Application","version":"2.1.1"}}
        </script>
        <script type="text/javascript">
          (function() {
            var fn = function() {
              Bokeh.safely(function() {
                (function(root) {
                  function embed_document(root) {
                    
                  var docs_json = document.getElementById('8471').textContent;
                  var render_items = [{"docid":"565641f3-1abd-48cb-ae98-4bf5fc049d51","root_ids":["7906"],"roots":{"7906":"27a42496-e4c3-48b1-a9bf-e8dd293b15ee"}}];
                  root.Bokeh.embed.embed_items(docs_json, render_items);
                
                  }
                  if (root.Bokeh !== undefined) {
                    embed_document(root);
                  } else {
                    var attempts = 0;
                    var timer = setInterval(function(root) {
                      if (root.Bokeh !== undefined) {
                        clearInterval(timer);
                        embed_document(root);
                      } else {
                        attempts++;
                        if (attempts > 100) {
                          clearInterval(timer);
                          console.log("Bokeh: ERROR: Unable to run BokehJS code because BokehJS library is missing");
                        }
                      }
                    }, 10, root)
                  }
                })(window);
              });
            };
            if (document.readyState != "loading") fn();
            else document.addEventListener("DOMContentLoaded", fn);
          })();
        </script>
    
  </body>
  
</html>

## Creating Bar Charts

```python
# create random data

x_ax = ['cat1', 'cat2', 'cat3', 'cat4', 'cat5']
y_ax = np.random.rand(5) * 10

# sort data

sorted_cat = sorted(x_ax, key=lambda x: y_ax[x_ax.index(x)], reverse=True)

# Create instance of the bar chart

bar_chart = figure(x_range=sorted_cat, title='Bar Chart', x_axis_label='X', y_axis_label='Y', plot_height=300)
# use vbar for vertical and hvar for horizontal 
bar_chart.vbar(x_ax, top=y_ax, color='blue', width=0.4)
bar_chart.y_range.start = 0
bar_chart.add_tools(HoverTool())
output_file('/bar_chart.html')
show(bar_chart)
```

<html lang="en">
  
  <head>
    
      <meta charset="utf-8">
      <title>Bokeh Plot</title>
      
      
        
          
        
        
          
        <script type="text/javascript" src="https://cdn.bokeh.org/bokeh/release/bokeh-2.1.1.min.js" integrity="sha384-kLr4fYcqcSpbuI95brIH3vnnYCquzzSxHPU6XGQCIkQRGJwhg0StNbj1eegrHs12" crossorigin="anonymous"></script>
        <script type="text/javascript">
            Bokeh.set_log_level("info");
        </script>
        
      
      
    
  </head>
  
  
  <body>
    
      
        
          
          
            
              <div class="bk-root" id="dfc5f4b8-9213-47d7-aeb8-552599982598" data-root-id="4750"></div>
            
          
        
      
      
        <script type="application/json" id="5104">
          {"0bfab220-777b-4adf-94c4-a76389058771":{"roots":{"references":[{"attributes":{"below":[{"id":"4761"}],"center":[{"id":"4763"},{"id":"4767"}],"left":[{"id":"4764"}],"plot_height":300,"renderers":[{"id":"4785"}],"title":{"id":"4751"},"toolbar":{"id":"4775"},"x_range":{"id":"4753"},"x_scale":{"id":"4757"},"y_range":{"id":"4755"},"y_scale":{"id":"4759"}},"id":"4750","subtype":"Figure","type":"Plot"},{"attributes":{},"id":"4769","type":"WheelZoomTool"},{"attributes":{},"id":"4955","type":"CategoricalTickFormatter"},{"attributes":{"source":{"id":"4782"}},"id":"4786","type":"CDSView"},{"attributes":{"bottom_units":"screen","fill_alpha":0.5,"fill_color":"lightgrey","left_units":"screen","level":"overlay","line_alpha":1.0,"line_color":"black","line_dash":[4,4],"line_width":2,"right_units":"screen","top_units":"screen"},"id":"4774","type":"BoxAnnotation"},{"attributes":{"start":0},"id":"4755","type":"DataRange1d"},{"attributes":{},"id":"4757","type":"CategoricalScale"},{"attributes":{},"id":"4958","type":"UnionRenderers"},{"attributes":{},"id":"4759","type":"LinearScale"},{"attributes":{},"id":"4953","type":"BasicTickFormatter"},{"attributes":{"data_source":{"id":"4782"},"glyph":{"id":"4783"},"hover_glyph":null,"muted_glyph":null,"nonselection_glyph":{"id":"4784"},"selection_glyph":null,"view":{"id":"4786"}},"id":"4785","type":"GlyphRenderer"},{"attributes":{},"id":"4957","type":"Selection"},{"attributes":{},"id":"4762","type":"CategoricalTicker"},{"attributes":{"axis_label":"X","formatter":{"id":"4955"},"ticker":{"id":"4762"}},"id":"4761","type":"CategoricalAxis"},{"attributes":{"axis":{"id":"4761"},"ticker":null},"id":"4763","type":"Grid"},{"attributes":{"axis_label":"Y","formatter":{"id":"4953"},"ticker":{"id":"4765"}},"id":"4764","type":"LinearAxis"},{"attributes":{},"id":"4772","type":"ResetTool"},{"attributes":{"fill_color":{"value":"blue"},"line_color":{"value":"blue"},"top":{"field":"top"},"width":{"value":0.4},"x":{"field":"x"}},"id":"4783","type":"VBar"},{"attributes":{"factors":["cat3","cat1","cat4","cat2","cat5"]},"id":"4753","type":"FactorRange"},{"attributes":{},"id":"4771","type":"SaveTool"},{"attributes":{},"id":"4765","type":"BasicTicker"},{"attributes":{"overlay":{"id":"4774"}},"id":"4770","type":"BoxZoomTool"},{"attributes":{"axis":{"id":"4764"},"dimension":1,"ticker":null},"id":"4767","type":"Grid"},{"attributes":{},"id":"4773","type":"HelpTool"},{"attributes":{},"id":"4768","type":"PanTool"},{"attributes":{"callback":null},"id":"4787","type":"HoverTool"},{"attributes":{"data":{"top":{"__ndarray__":"qxQeoT2NHkAylUIAoIbvP/uedcCV2CFAbtws1jeOFEBgfpYDGavtPw==","dtype":"float64","order":"little","shape":[5]},"x":["cat1","cat2","cat3","cat4","cat5"]},"selected":{"id":"4957"},"selection_policy":{"id":"4958"}},"id":"4782","type":"ColumnDataSource"},{"attributes":{"fill_alpha":{"value":0.1},"fill_color":{"value":"blue"},"line_alpha":{"value":0.1},"line_color":{"value":"blue"},"top":{"field":"top"},"width":{"value":0.4},"x":{"field":"x"}},"id":"4784","type":"VBar"},{"attributes":{"active_drag":"auto","active_inspect":"auto","active_multi":null,"active_scroll":"auto","active_tap":"auto","tools":[{"id":"4768"},{"id":"4769"},{"id":"4770"},{"id":"4771"},{"id":"4772"},{"id":"4773"},{"id":"4787"}]},"id":"4775","type":"Toolbar"},{"attributes":{"text":"Bar Chart"},"id":"4751","type":"Title"}],"root_ids":["4750"]},"title":"Bokeh Application","version":"2.1.1"}}
        </script>
        <script type="text/javascript">
          (function() {
            var fn = function() {
              Bokeh.safely(function() {
                (function(root) {
                  function embed_document(root) {
                    
                  var docs_json = document.getElementById('5104').textContent;
                  var render_items = [{"docid":"0bfab220-777b-4adf-94c4-a76389058771","root_ids":["4750"],"roots":{"4750":"dfc5f4b8-9213-47d7-aeb8-552599982598"}}];
                  root.Bokeh.embed.embed_items(docs_json, render_items);
                
                  }
                  if (root.Bokeh !== undefined) {
                    embed_document(root);
                  } else {
                    var attempts = 0;
                    var timer = setInterval(function(root) {
                      if (root.Bokeh !== undefined) {
                        clearInterval(timer);
                        embed_document(root);
                      } else {
                        attempts++;
                        if (attempts > 100) {
                          clearInterval(timer);
                          console.log("Bokeh: ERROR: Unable to run BokehJS code because BokehJS library is missing");
                        }
                      }
                    }, 10, root)
                  }
                })(window);
              });
            };
            if (document.readyState != "loading") fn();
            else document.addEventListener("DOMContentLoaded", fn);
          })();
        </script>
    
  </body>
  
</html>

### Stacked Bar Chart

```python
# Stacked Bar Chart
df_stacked = pd.DataFrame({'y': [1, 2, 3, 4, 5],
                           'x1': [1,2, 4, 3, 4],
                           'x2' : [1, 4, 2, 2, 3]})

df_CDS_tacked = ColumnDataSource(df_stacked)

stacked_bar_chart = figure(plot_width=600, plot_height=300, title='Stacked Bar Chart')
stacked_bar_chart.hbar_stack(['x1', 'x2'],
                             y = 'y',
                             height = 0.8,
                             color = ('green', 'lightgreen'),
                             source=df_stacked
                             )
stacked_bar_chart.add_tools(HoverTool())
output_file('/stacked_bar_chart.html')
show(stacked_bar_chart)
```


<html lang="en">
  
  <head>
    
      <meta charset="utf-8">
      <title>Bokeh Plot</title>
      
      
        
          
        
        
          
        <script type="text/javascript" src="https://cdn.bokeh.org/bokeh/release/bokeh-2.1.1.min.js" integrity="sha384-kLr4fYcqcSpbuI95brIH3vnnYCquzzSxHPU6XGQCIkQRGJwhg0StNbj1eegrHs12" crossorigin="anonymous"></script>
        <script type="text/javascript">
            Bokeh.set_log_level("info");
        </script>
        
      
      
    
  </head>
  
  
  <body>
    
      
        
          
          
            
              <div class="bk-root" id="18aabacf-0814-4a30-993e-954c9d5f8f2a" data-root-id="7431"></div>
            
          
        
      
      
        <script type="application/json" id="7895">
          {"308af490-02bd-4535-b2d8-aa452aedd868":{"roots":{"references":[{"attributes":{"below":[{"id":"7442"}],"center":[{"id":"7445"},{"id":"7449"}],"left":[{"id":"7446"}],"plot_height":300,"renderers":[{"id":"7472"},{"id":"7478"}],"title":{"id":"7432"},"toolbar":{"id":"7457"},"x_range":{"id":"7434"},"x_scale":{"id":"7438"},"y_range":{"id":"7436"},"y_scale":{"id":"7440"}},"id":"7431","subtype":"Figure","type":"Plot"},{"attributes":{"axis":{"id":"7442"},"ticker":null},"id":"7445","type":"Grid"},{"attributes":{"formatter":{"id":"7706"},"ticker":{"id":"7447"}},"id":"7446","type":"LinearAxis"},{"attributes":{"source":{"id":"7468"}},"id":"7473","type":"CDSView"},{"attributes":{},"id":"7450","type":"PanTool"},{"attributes":{},"id":"7447","type":"BasicTicker"},{"attributes":{},"id":"7455","type":"HelpTool"},{"attributes":{"fill_alpha":{"value":0.1},"fill_color":{"value":"green"},"height":{"value":0.8},"left":{"expr":{"id":"7464"}},"line_alpha":{"value":0.1},"line_color":{"value":"green"},"right":{"expr":{"id":"7465"}},"y":{"field":"y"}},"id":"7471","type":"HBar"},{"attributes":{"data_source":{"id":"7468"},"glyph":{"id":"7470"},"hover_glyph":null,"muted_glyph":null,"name":"x1","nonselection_glyph":{"id":"7471"},"selection_glyph":null,"view":{"id":"7473"}},"id":"7472","type":"GlyphRenderer"},{"attributes":{"fields":["x1"]},"id":"7466","type":"Stack"},{"attributes":{"bottom_units":"screen","fill_alpha":0.5,"fill_color":"lightgrey","left_units":"screen","level":"overlay","line_alpha":1.0,"line_color":"black","line_dash":[4,4],"line_width":2,"right_units":"screen","top_units":"screen"},"id":"7456","type":"BoxAnnotation"},{"attributes":{"data_source":{"id":"7474"},"glyph":{"id":"7476"},"hover_glyph":null,"muted_glyph":null,"name":"x2","nonselection_glyph":{"id":"7477"},"selection_glyph":null,"view":{"id":"7479"}},"id":"7478","type":"GlyphRenderer"},{"attributes":{"active_drag":"auto","active_inspect":"auto","active_multi":null,"active_scroll":"auto","active_tap":"auto","tools":[{"id":"7450"},{"id":"7451"},{"id":"7452"},{"id":"7453"},{"id":"7454"},{"id":"7455"},{"id":"7480"}]},"id":"7457","type":"Toolbar"},{"attributes":{"fill_alpha":{"value":0.1},"fill_color":{"value":"lightgreen"},"height":{"value":0.8},"left":{"expr":{"id":"7466"}},"line_alpha":{"value":0.1},"line_color":{"value":"lightgreen"},"right":{"expr":{"id":"7467"}},"y":{"field":"y"}},"id":"7477","type":"HBar"},{"attributes":{"fields":["x1","x2"]},"id":"7467","type":"Stack"},{"attributes":{"source":{"id":"7474"}},"id":"7479","type":"CDSView"},{"attributes":{"callback":null},"id":"7480","type":"HoverTool"},{"attributes":{"overlay":{"id":"7456"}},"id":"7452","type":"BoxZoomTool"},{"attributes":{},"id":"7712","type":"Selection"},{"attributes":{"data":{"index":[0,1,2,3,4],"x1":[1,2,4,3,4],"x2":[1,4,2,2,3],"y":[1,2,3,4,5]},"selected":{"id":"7712"},"selection_policy":{"id":"7713"}},"id":"7474","type":"ColumnDataSource"},{"attributes":{"text":"Stacked Bar Chart"},"id":"7432","type":"Title"},{"attributes":{"fill_color":{"value":"lightgreen"},"height":{"value":0.8},"left":{"expr":{"id":"7466"}},"line_color":{"value":"lightgreen"},"right":{"expr":{"id":"7467"}},"y":{"field":"y"}},"id":"7476","type":"HBar"},{"attributes":{"data":{"index":[0,1,2,3,4],"x1":[1,2,4,3,4],"x2":[1,4,2,2,3],"y":[1,2,3,4,5]},"selected":{"id":"7710"},"selection_policy":{"id":"7711"}},"id":"7468","type":"ColumnDataSource"},{"attributes":{},"id":"7453","type":"SaveTool"},{"attributes":{},"id":"7434","type":"DataRange1d"},{"attributes":{},"id":"7711","type":"UnionRenderers"},{"attributes":{},"id":"7451","type":"WheelZoomTool"},{"attributes":{},"id":"7710","type":"Selection"},{"attributes":{},"id":"7454","type":"ResetTool"},{"attributes":{"fields":[]},"id":"7464","type":"Stack"},{"attributes":{},"id":"7706","type":"BasicTickFormatter"},{"attributes":{},"id":"7713","type":"UnionRenderers"},{"attributes":{},"id":"7708","type":"BasicTickFormatter"},{"attributes":{"axis":{"id":"7446"},"dimension":1,"ticker":null},"id":"7449","type":"Grid"},{"attributes":{"fill_color":{"value":"green"},"height":{"value":0.8},"left":{"expr":{"id":"7464"}},"line_color":{"value":"green"},"right":{"expr":{"id":"7465"}},"y":{"field":"y"}},"id":"7470","type":"HBar"},{"attributes":{},"id":"7438","type":"LinearScale"},{"attributes":{"fields":["x1"]},"id":"7465","type":"Stack"},{"attributes":{},"id":"7440","type":"LinearScale"},{"attributes":{},"id":"7436","type":"DataRange1d"},{"attributes":{"formatter":{"id":"7708"},"ticker":{"id":"7443"}},"id":"7442","type":"LinearAxis"},{"attributes":{},"id":"7443","type":"BasicTicker"}],"root_ids":["7431"]},"title":"Bokeh Application","version":"2.1.1"}}
        </script>
        <script type="text/javascript">
          (function() {
            var fn = function() {
              Bokeh.safely(function() {
                (function(root) {
                  function embed_document(root) {
                    
                  var docs_json = document.getElementById('7895').textContent;
                  var render_items = [{"docid":"308af490-02bd-4535-b2d8-aa452aedd868","root_ids":["7431"],"roots":{"7431":"18aabacf-0814-4a30-993e-954c9d5f8f2a"}}];
                  root.Bokeh.embed.embed_items(docs_json, render_items);
                
                  }
                  if (root.Bokeh !== undefined) {
                    embed_document(root);
                  } else {
                    var attempts = 0;
                    var timer = setInterval(function(root) {
                      if (root.Bokeh !== undefined) {
                        clearInterval(timer);
                        embed_document(root);
                      } else {
                        attempts++;
                        if (attempts > 100) {
                          clearInterval(timer);
                          console.log("Bokeh: ERROR: Unable to run BokehJS code because BokehJS library is missing");
                        }
                      }
                    }, 10, root)
                  }
                })(window);
              });
            };
            if (document.readyState != "loading") fn();
            else document.addEventListener("DOMContentLoaded", fn);
          })();
        </script>
    
  </body>
  
</html>

## Creating a Bar Chart Grouping Data

```python

from bokeh.transform import dodge

# create some random data

categories = ['category1', 'category2', 'category3']

df_grouped = pd.DataFrame({'categories' : categories,
                           '2018' : [2, 1, 4],
                           '2019' : [5, 3, 3],
                           '2020' : [3, 2, 4]})

# create instance of a figure
bar_grouped = figure(x_range=categories, y_range = (0, 10), plot_height = 350)

# define position of bars on chart
dodge1 = dodge('categories', -0.25, range=bar_grouped.x_range)
dodge2 = dodge('categories', 0.0, range=bar_grouped.x_range)
dodge3 = dodge('categories', 0.25, range=bar_grouped.x_range)

bar_grouped.vbar(x=dodge1, top='2018', width=0.2, source=df_grouped, color='blue', legend_label='2018')
bar_grouped.vbar(x=dodge2, top='2019', width=0.2, source=df_grouped, color='green', legend_label='2019')
bar_grouped.vbar(x=dodge3, top='2020', width=0.2, source=df_grouped, color='red', legend_label='2020')

# configure legend

bar_grouped.legend.location = 'top_left'
bar_grouped.legend.orientation = 'horizontal'


bar_grouped.add_tools(HoverTool())
output_file('/grouped_bar_chart.html')
show(bar_grouped)
```


<head>
    
      <meta charset="utf-8">
      <title>Bokeh Plot</title>
      
      
        
          
        
        
          
        <script type="text/javascript" src="https://cdn.bokeh.org/bokeh/release/bokeh-2.1.1.min.js" integrity="sha384-kLr4fYcqcSpbuI95brIH3vnnYCquzzSxHPU6XGQCIkQRGJwhg0StNbj1eegrHs12" crossorigin="anonymous"></script>
        <script type="text/javascript">
            Bokeh.set_log_level("info");
        </script>
        
      
      
    
  </head>
  
  
  <body>
    
      
        
          
          
            
              <div class="bk-root" id="e764092d-eca7-4931-9517-07a6c1226369" data-root-id="9808"></div>
            
          
        
      
      
        <script type="application/json" id="10389">
          {"2b8c35e9-8263-457f-970c-4416307ac451":{"roots":{"references":[{"attributes":{"below":[{"id":"9817"}],"center":[{"id":"9819"},{"id":"9823"},{"id":"9856"}],"left":[{"id":"9820"}],"plot_height":350,"renderers":[{"id":"9845"},{"id":"9862"},{"id":"9880"}],"title":{"id":"9848"},"toolbar":{"id":"9831"},"x_range":{"id":"9809"},"x_scale":{"id":"9813"},"y_range":{"id":"9811"},"y_scale":{"id":"9815"}},"id":"9808","subtype":"Figure","type":"Plot"},{"attributes":{},"id":"9824","type":"PanTool"},{"attributes":{},"id":"9828","type":"ResetTool"},{"attributes":{"range":{"id":"9809"},"value":0.25},"id":"9840","type":"Dodge"},{"attributes":{"label":{"value":"2020"},"renderers":[{"id":"9880"}]},"id":"9895","type":"LegendItem"},{"attributes":{"data":{"2018":[2,1,4],"2019":[5,3,3],"2020":[3,2,4],"categories":["category1","category2","category3"],"index":[0,1,2]},"selected":{"id":"9893"},"selection_policy":{"id":"9894"}},"id":"9876","type":"ColumnDataSource"},{"attributes":{},"id":"9829","type":"HelpTool"},{"attributes":{"axis":{"id":"9820"},"dimension":1,"ticker":null},"id":"9823","type":"Grid"},{"attributes":{},"id":"9827","type":"SaveTool"},{"attributes":{"data":{"2018":[2,1,4],"2019":[5,3,3],"2020":[3,2,4],"categories":["category1","category2","category3"],"index":[0,1,2]},"selected":{"id":"9854"},"selection_policy":{"id":"9855"}},"id":"9841","type":"ColumnDataSource"},{"attributes":{},"id":"9894","type":"UnionRenderers"},{"attributes":{"bottom_units":"screen","fill_alpha":0.5,"fill_color":"lightgrey","left_units":"screen","level":"overlay","line_alpha":1.0,"line_color":"black","line_dash":[4,4],"line_width":2,"right_units":"screen","top_units":"screen"},"id":"9830","type":"BoxAnnotation"},{"attributes":{"range":{"id":"9809"},"value":-0.25},"id":"9838","type":"Dodge"},{"attributes":{"active_drag":"auto","active_inspect":"auto","active_multi":null,"active_scroll":"auto","active_tap":"auto","tools":[{"id":"9824"},{"id":"9825"},{"id":"9826"},{"id":"9827"},{"id":"9828"},{"id":"9829"},{"id":"9896"}]},"id":"9831","type":"Toolbar"},{"attributes":{"source":{"id":"9876"}},"id":"9881","type":"CDSView"},{"attributes":{"range":{"id":"9809"}},"id":"9839","type":"Dodge"},{"attributes":{"end":10},"id":"9811","type":"Range1d"},{"attributes":{"fill_color":{"value":"red"},"line_color":{"value":"red"},"top":{"field":"2020"},"width":{"value":0.2},"x":{"field":"categories","transform":{"id":"9840"}}},"id":"9878","type":"VBar"},{"attributes":{},"id":"9873","type":"Selection"},{"attributes":{},"id":"9855","type":"UnionRenderers"},{"attributes":{"data_source":{"id":"9858"},"glyph":{"id":"9860"},"hover_glyph":null,"muted_glyph":null,"nonselection_glyph":{"id":"9861"},"selection_glyph":null,"view":{"id":"9863"}},"id":"9862","type":"GlyphRenderer"},{"attributes":{"label":{"value":"2018"},"renderers":[{"id":"9845"}]},"id":"9857","type":"LegendItem"},{"attributes":{},"id":"9815","type":"LinearScale"},{"attributes":{"text":""},"id":"9848","type":"Title"},{"attributes":{"factors":["category1","category2","category3"]},"id":"9809","type":"FactorRange"},{"attributes":{"fill_color":{"value":"green"},"line_color":{"value":"green"},"top":{"field":"2019"},"width":{"value":0.2},"x":{"field":"categories","transform":{"id":"9839"}}},"id":"9860","type":"VBar"},{"attributes":{"items":[{"id":"9857"},{"id":"9875"},{"id":"9895"}],"location":"top_left","orientation":"horizontal"},"id":"9856","type":"Legend"},{"attributes":{},"id":"9813","type":"CategoricalScale"},{"attributes":{},"id":"9851","type":"CategoricalTickFormatter"},{"attributes":{"data_source":{"id":"9876"},"glyph":{"id":"9878"},"hover_glyph":null,"muted_glyph":null,"nonselection_glyph":{"id":"9879"},"selection_glyph":null,"view":{"id":"9881"}},"id":"9880","type":"GlyphRenderer"},{"attributes":{},"id":"9854","type":"Selection"},{"attributes":{"label":{"value":"2019"},"renderers":[{"id":"9862"}]},"id":"9875","type":"LegendItem"},{"attributes":{"data":{"2018":[2,1,4],"2019":[5,3,3],"2020":[3,2,4],"categories":["category1","category2","category3"],"index":[0,1,2]},"selected":{"id":"9873"},"selection_policy":{"id":"9874"}},"id":"9858","type":"ColumnDataSource"},{"attributes":{},"id":"9818","type":"CategoricalTicker"},{"attributes":{},"id":"9849","type":"BasicTickFormatter"},{"attributes":{"fill_alpha":{"value":0.1},"fill_color":{"value":"blue"},"line_alpha":{"value":0.1},"line_color":{"value":"blue"},"top":{"field":"2018"},"width":{"value":0.2},"x":{"field":"categories","transform":{"id":"9838"}}},"id":"9844","type":"VBar"},{"attributes":{"formatter":{"id":"9851"},"ticker":{"id":"9818"}},"id":"9817","type":"CategoricalAxis"},{"attributes":{},"id":"9874","type":"UnionRenderers"},{"attributes":{},"id":"9821","type":"BasicTicker"},{"attributes":{"source":{"id":"9858"}},"id":"9863","type":"CDSView"},{"attributes":{"data_source":{"id":"9841"},"glyph":{"id":"9843"},"hover_glyph":null,"muted_glyph":null,"nonselection_glyph":{"id":"9844"},"selection_glyph":null,"view":{"id":"9846"}},"id":"9845","type":"GlyphRenderer"},{"attributes":{"formatter":{"id":"9849"},"ticker":{"id":"9821"}},"id":"9820","type":"LinearAxis"},{"attributes":{"axis":{"id":"9817"},"ticker":null},"id":"9819","type":"Grid"},{"attributes":{"source":{"id":"9841"}},"id":"9846","type":"CDSView"},{"attributes":{"overlay":{"id":"9830"}},"id":"9826","type":"BoxZoomTool"},{"attributes":{"callback":null},"id":"9896","type":"HoverTool"},{"attributes":{"fill_color":{"value":"blue"},"line_color":{"value":"blue"},"top":{"field":"2018"},"width":{"value":0.2},"x":{"field":"categories","transform":{"id":"9838"}}},"id":"9843","type":"VBar"},{"attributes":{},"id":"9893","type":"Selection"},{"attributes":{},"id":"9825","type":"WheelZoomTool"},{"attributes":{"fill_alpha":{"value":0.1},"fill_color":{"value":"red"},"line_alpha":{"value":0.1},"line_color":{"value":"red"},"top":{"field":"2020"},"width":{"value":0.2},"x":{"field":"categories","transform":{"id":"9840"}}},"id":"9879","type":"VBar"},{"attributes":{"fill_alpha":{"value":0.1},"fill_color":{"value":"green"},"line_alpha":{"value":0.1},"line_color":{"value":"green"},"top":{"field":"2019"},"width":{"value":0.2},"x":{"field":"categories","transform":{"id":"9839"}}},"id":"9861","type":"VBar"}],"root_ids":["9808"]},"title":"Bokeh Application","version":"2.1.1"}}
        </script>
        <script type="text/javascript">
          (function() {
            var fn = function() {
              Bokeh.safely(function() {
                (function(root) {
                  function embed_document(root) {
                    
                  var docs_json = document.getElementById('10389').textContent;
                  var render_items = [{"docid":"2b8c35e9-8263-457f-970c-4416307ac451","root_ids":["9808"],"roots":{"9808":"e764092d-eca7-4931-9517-07a6c1226369"}}];
                  root.Bokeh.embed.embed_items(docs_json, render_items);
                
                  }
                  if (root.Bokeh !== undefined) {
                    embed_document(root);
                  } else {
                    var attempts = 0;
                    var timer = setInterval(function(root) {
                      if (root.Bokeh !== undefined) {
                        clearInterval(timer);
                        embed_document(root);
                      } else {
                        attempts++;
                        if (attempts > 100) {
                          clearInterval(timer);
                          console.log("Bokeh: ERROR: Unable to run BokehJS code because BokehJS library is missing");
                        }
                      }
                    }, 10, root)
                  }
                })(window);
              });
            };
            if (document.readyState != "loading") fn();
            else document.addEventListener("DOMContentLoaded", fn);
          })();
        </script>
    
  </body>
  
## Stacked Area Chart

```python
# create dummy data for the chart

df_area_stacked = pd.DataFrame({'x' : [1, 2, 3, 4, 5],
                                'y1' : [1, 3, 1, 4, 5],
                                'y2' : [1, 2, 3, 4, 2]})

stacked_area_chart = figure(plot_width=600, plot_height=300)

stacked_area_chart.varea_stack(['y1', 'y2'],
                               x = 'x',
                               color = ('coral', 'cadetblue'),
                               source = df_area_stacked)
show(stacked_area_chart)
```

<head>
    
      <meta charset="utf-8">
      <title>Bokeh Plot</title>
      
      
        
          
        
        
          
        <script type="text/javascript" src="https://cdn.bokeh.org/bokeh/release/bokeh-2.1.1.min.js" integrity="sha384-kLr4fYcqcSpbuI95brIH3vnnYCquzzSxHPU6XGQCIkQRGJwhg0StNbj1eegrHs12" crossorigin="anonymous"></script>
        <script type="text/javascript">
            Bokeh.set_log_level("info");
        </script>
        
      
      
    
  </head>
  
  
  <body>
    
      
        
          
          
            
              <div class="bk-root" id="a6f981c5-7b85-435c-a3b2-ebf9dc3f5620" data-root-id="5432"></div>
            
          
        
      
      
        <script type="application/json" id="5828">
          {"fa91f574-24b4-4b00-a38a-eb61c239a893":{"roots":{"references":[{"attributes":{"below":[{"id":"5441"}],"center":[{"id":"5444"},{"id":"5448"}],"left":[{"id":"5445"}],"plot_height":300,"renderers":[{"id":"5471"},{"id":"5477"}],"title":{"id":"5620"},"toolbar":{"id":"5456"},"x_range":{"id":"5433"},"x_scale":{"id":"5437"},"y_range":{"id":"5435"},"y_scale":{"id":"5439"}},"id":"5432","subtype":"Figure","type":"Plot"},{"attributes":{},"id":"5628","type":"Selection"},{"attributes":{},"id":"5623","type":"BasicTickFormatter"},{"attributes":{"formatter":{"id":"5623"},"ticker":{"id":"5442"}},"id":"5441","type":"LinearAxis"},{"attributes":{"source":{"id":"5473"}},"id":"5478","type":"CDSView"},{"attributes":{"fields":[]},"id":"5463","type":"Stack"},{"attributes":{"data_source":{"id":"5473"},"glyph":{"id":"5475"},"hover_glyph":null,"muted_glyph":null,"name":"y2","nonselection_glyph":{"id":"5476"},"selection_glyph":null,"view":{"id":"5478"}},"id":"5477","type":"GlyphRenderer"},{"attributes":{"source":{"id":"5467"}},"id":"5472","type":"CDSView"},{"attributes":{"fields":["y1","y2"]},"id":"5466","type":"Stack"},{"attributes":{"fill_color":"cadetblue","x":{"field":"x"},"y1":{"expr":{"id":"5465"}},"y2":{"expr":{"id":"5466"}}},"id":"5475","type":"VArea"},{"attributes":{"axis":{"id":"5441"},"ticker":null},"id":"5444","type":"Grid"},{"attributes":{},"id":"5629","type":"UnionRenderers"},{"attributes":{},"id":"5627","type":"UnionRenderers"},{"attributes":{},"id":"5442","type":"BasicTicker"},{"attributes":{"data":{"index":[0,1,2,3,4],"x":[1,2,3,4,5],"y1":[1,3,1,4,5],"y2":[1,2,3,4,2]},"selected":{"id":"5628"},"selection_policy":{"id":"5629"}},"id":"5473","type":"ColumnDataSource"},{"attributes":{"bottom_units":"screen","fill_alpha":0.5,"fill_color":"lightgrey","left_units":"screen","level":"overlay","line_alpha":1.0,"line_color":"black","line_dash":[4,4],"line_width":2,"right_units":"screen","top_units":"screen"},"id":"5455","type":"BoxAnnotation"},{"attributes":{},"id":"5446","type":"BasicTicker"},{"attributes":{"fill_alpha":0.1,"fill_color":"coral","x":{"field":"x"},"y1":{"expr":{"id":"5463"}},"y2":{"expr":{"id":"5464"}}},"id":"5470","type":"VArea"},{"attributes":{},"id":"5453","type":"ResetTool"},{"attributes":{},"id":"5437","type":"LinearScale"},{"attributes":{"fill_color":"coral","x":{"field":"x"},"y1":{"expr":{"id":"5463"}},"y2":{"expr":{"id":"5464"}}},"id":"5469","type":"VArea"},{"attributes":{"data_source":{"id":"5467"},"glyph":{"id":"5469"},"hover_glyph":null,"muted_glyph":null,"name":"y1","nonselection_glyph":{"id":"5470"},"selection_glyph":null,"view":{"id":"5472"}},"id":"5471","type":"GlyphRenderer"},{"attributes":{},"id":"5454","type":"HelpTool"},{"attributes":{},"id":"5621","type":"BasicTickFormatter"},{"attributes":{},"id":"5450","type":"WheelZoomTool"},{"attributes":{"fields":["y1"]},"id":"5464","type":"Stack"},{"attributes":{"text":""},"id":"5620","type":"Title"},{"attributes":{},"id":"5626","type":"Selection"},{"attributes":{"active_drag":"auto","active_inspect":"auto","active_multi":null,"active_scroll":"auto","active_tap":"auto","tools":[{"id":"5449"},{"id":"5450"},{"id":"5451"},{"id":"5452"},{"id":"5453"},{"id":"5454"}]},"id":"5456","type":"Toolbar"},{"attributes":{"formatter":{"id":"5621"},"ticker":{"id":"5446"}},"id":"5445","type":"LinearAxis"},{"attributes":{"data":{"index":[0,1,2,3,4],"x":[1,2,3,4,5],"y1":[1,3,1,4,5],"y2":[1,2,3,4,2]},"selected":{"id":"5626"},"selection_policy":{"id":"5627"}},"id":"5467","type":"ColumnDataSource"},{"attributes":{},"id":"5439","type":"LinearScale"},{"attributes":{},"id":"5435","type":"DataRange1d"},{"attributes":{"axis":{"id":"5445"},"dimension":1,"ticker":null},"id":"5448","type":"Grid"},{"attributes":{"fields":["y1"]},"id":"5465","type":"Stack"},{"attributes":{},"id":"5433","type":"DataRange1d"},{"attributes":{},"id":"5452","type":"SaveTool"},{"attributes":{},"id":"5449","type":"PanTool"},{"attributes":{"overlay":{"id":"5455"}},"id":"5451","type":"BoxZoomTool"},{"attributes":{"fill_alpha":0.1,"fill_color":"cadetblue","x":{"field":"x"},"y1":{"expr":{"id":"5465"}},"y2":{"expr":{"id":"5466"}}},"id":"5476","type":"VArea"}],"root_ids":["5432"]},"title":"Bokeh Application","version":"2.1.1"}}
        </script>
        <script type="text/javascript">
          (function() {
            var fn = function() {
              Bokeh.safely(function() {
                (function(root) {
                  function embed_document(root) {
                    
                  var docs_json = document.getElementById('5828').textContent;
                  var render_items = [{"docid":"fa91f574-24b4-4b00-a38a-eb61c239a893","root_ids":["5432"],"roots":{"5432":"a6f981c5-7b85-435c-a3b2-ebf9dc3f5620"}}];
                  root.Bokeh.embed.embed_items(docs_json, render_items);
                
                  }
                  if (root.Bokeh !== undefined) {
                    embed_document(root);
                  } else {
                    var attempts = 0;
                    var timer = setInterval(function(root) {
                      if (root.Bokeh !== undefined) {
                        clearInterval(timer);
                        embed_document(root);
                      } else {
                        attempts++;
                        if (attempts > 100) {
                          clearInterval(timer);
                          console.log("Bokeh: ERROR: Unable to run BokehJS code because BokehJS library is missing");
                        }
                      }
                    }, 10, root)
                  }
                })(window);
              });
            };
            if (document.readyState != "loading") fn();
            else document.addEventListener("DOMContentLoaded", fn);
          })();
        </script>
    
  </body>

## Scatter Plots

Load the car dataset from vega
```python
df_cars = vds.cars()
df_cars.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>Name</th>
      <th>Miles_per_Gallon</th>
      <th>Cylinders</th>
      <th>Displacement</th>
      <th>Horsepower</th>
      <th>Weight_in_lbs</th>
      <th>Acceleration</th>
      <th>Year</th>
      <th>Origin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>chevrolet chevelle malibu</td>
      <td>18.0</td>
      <td>8</td>
      <td>307.0</td>
      <td>130.0</td>
      <td>3504</td>
      <td>12.0</td>
      <td>1970-01-01</td>
      <td>USA</td>
    </tr>
    <tr>
      <th>1</th>
      <td>buick skylark 320</td>
      <td>15.0</td>
      <td>8</td>
      <td>350.0</td>
      <td>165.0</td>
      <td>3693</td>
      <td>11.5</td>
      <td>1970-01-01</td>
      <td>USA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>plymouth satellite</td>
      <td>18.0</td>
      <td>8</td>
      <td>318.0</td>
      <td>150.0</td>
      <td>3436</td>
      <td>11.0</td>
      <td>1970-01-01</td>
      <td>USA</td>
    </tr>
    <tr>
      <th>3</th>
      <td>amc rebel sst</td>
      <td>16.0</td>
      <td>8</td>
      <td>304.0</td>
      <td>150.0</td>
      <td>3433</td>
      <td>12.0</td>
      <td>1970-01-01</td>
      <td>USA</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ford torino</td>
      <td>17.0</td>
      <td>8</td>
      <td>302.0</td>
      <td>140.0</td>
      <td>3449</td>
      <td>10.5</td>
      <td>1970-01-01</td>
      <td>USA</td>
    </tr>
  </tbody>
</table>

<head>
    
      <meta charset="utf-8">
      <title>Bokeh Plot</title>
      
      
        
          
        
        
          
        <script type="text/javascript" src="https://cdn.bokeh.org/bokeh/release/bokeh-2.1.1.min.js" integrity="sha384-kLr4fYcqcSpbuI95brIH3vnnYCquzzSxHPU6XGQCIkQRGJwhg0StNbj1eegrHs12" crossorigin="anonymous"></script>
        <script type="text/javascript">
            Bokeh.set_log_level("info");
        </script>
        
      
      
    
  </head>
  
  
  <body>
    
      
        
          
          
            
              <div class="bk-root" id="cf29326c-833c-4c60-b0c7-cde9caae4102" data-root-id="12156"></div>
            
          
        
      
      
        <script type="application/json" id="12621">
          {"8535aaba-4692-4931-9d8e-629e6ac7abd8":{"roots":{"references":[{"attributes":{"below":[{"id":"12167"}],"center":[{"id":"12170"},{"id":"12174"}],"left":[{"id":"12171"}],"plot_height":400,"renderers":[{"id":"12192"}],"title":{"id":"12157"},"toolbar":{"id":"12182"},"x_range":{"id":"12159"},"x_scale":{"id":"12163"},"y_range":{"id":"12161"},"y_scale":{"id":"12165"}},"id":"12156","subtype":"Figure","type":"Plot"},{"attributes":{},"id":"12180","type":"HelpTool"},{"attributes":{"bottom_units":"screen","fill_alpha":0.5,"fill_color":"lightgrey","left_units":"screen","level":"overlay","line_alpha":1.0,"line_color":"black","line_dash":[4,4],"line_width":2,"right_units":"screen","top_units":"screen"},"id":"12181","type":"BoxAnnotation"},{"attributes":{},"id":"12172","type":"BasicTicker"},{"attributes":{"data_source":{"id":"12189"},"glyph":{"id":"12190"},"hover_glyph":null,"muted_glyph":null,"nonselection_glyph":{"id":"12191"},"selection_glyph":null,"view":{"id":"12193"}},"id":"12192","type":"GlyphRenderer"},{"attributes":{},"id":"12168","type":"BasicTicker"},{"attributes":{"overlay":{"id":"12181"}},"id":"12177","type":"BoxZoomTool"},{"attributes":{},"id":"12165","type":"LinearScale"},{"attributes":{},"id":"12179","type":"ResetTool"},{"attributes":{"fill_alpha":{"value":0.1},"fill_color":{"value":"blue"},"line_alpha":{"value":0.1},"line_color":{"value":"gray"},"size":{"units":"screen","value":10},"x":{"field":"x"},"y":{"field":"y"}},"id":"12191","type":"Circle"},{"attributes":{},"id":"12159","type":"DataRange1d"},{"attributes":{},"id":"12163","type":"LinearScale"},{"attributes":{"text":"Weight and MPH Comparison"},"id":"12157","type":"Title"},{"attributes":{"source":{"id":"12189"}},"id":"12193","type":"CDSView"},{"attributes":{},"id":"12475","type":"Selection"},{"attributes":{"axis":{"id":"12171"},"dimension":1,"ticker":null},"id":"12174","type":"Grid"},{"attributes":{},"id":"12470","type":"BasicTickFormatter"},{"attributes":{"fill_alpha":{"value":0.5},"fill_color":{"value":"blue"},"line_color":{"value":"gray"},"size":{"units":"screen","value":10},"x":{"field":"x"},"y":{"field":"y"}},"id":"12190","type":"Circle"},{"attributes":{},"id":"12178","type":"SaveTool"},{"attributes":{"axis_label":"Weight in pounds","formatter":{"id":"12472"},"ticker":{"id":"12168"}},"id":"12167","type":"LinearAxis"},{"attributes":{},"id":"12472","type":"BasicTickFormatter"},{"attributes":{"callback":null},"id":"12194","type":"HoverTool"},{"attributes":{},"id":"12476","type":"UnionRenderers"},{"attributes":{},"id":"12175","type":"PanTool"},{"attributes":{},"id":"12176","type":"WheelZoomTool"},{"attributes":{"active_drag":"auto","active_inspect":"auto","active_multi":null,"active_scroll":"auto","active_tap":"auto","tools":[{"id":"12175"},{"id":"12176"},{"id":"12177"},{"id":"12178"},{"id":"12179"},{"id":"12180"},{"id":"12194"}]},"id":"12182","type":"Toolbar"},{"attributes":{"axis_label":"MPH","formatter":{"id":"12470"},"ticker":{"id":"12172"}},"id":"12171","type":"LinearAxis"},{"attributes":{"data":{"x":[3504,3693,3436,3433,3449,4341,4354,4312,4425,3850,3090,4142,4034,4166,3850,3563,3609,3353,3761,3086,2372,2833,2774,2587,2130,1835,2672,2430,2375,2234,2648,4615,4376,4382,4732,2130,2264,2228,2046,1978,2634,3439,3329,3302,3288,4209,4464,4154,4096,4955,4746,5140,2962,2408,3282,3139,2220,2123,2074,2065,1773,1613,1834,1955,2278,2126,2254,2408,2226,4274,4385,4135,4129,3672,4633,4502,4456,4422,2330,3892,4098,4294,4077,2933,2511,2979,2189,2395,2288,2506,2164,2100,4100,3672,3988,4042,3777,4952,4464,4363,4237,4735,4951,3821,3121,3278,2945,3021,2904,1950,4997,4906,4654,4499,2789,2279,2401,2379,2124,2310,2472,2265,4082,4278,1867,2158,2582,2868,3399,2660,2807,3664,3102,2875,2901,3336,1950,2451,1836,2542,3781,3632,3613,4141,4699,4457,4638,4257,2219,1963,2300,1649,2003,2125,2108,2246,2489,2391,2000,3264,3459,3432,3158,4668,4440,4498,4657,3907,3897,3730,3785,3039,3221,3169,2171,2639,2914,2592,2702,2223,2545,2984,1937,3211,2694,2957,2945,2671,1795,2464,2220,2572,2255,2202,4215,4190,3962,4215,3233,3353,3012,3085,2035,2164,1937,1795,3651,3574,3645,3193,1825,1990,2155,2565,3150,3940,3270,2930,3820,4380,4055,3870,3755,2045,2155,1825,2300,1945,3880,4060,4140,4295,3520,3425,3630,3525,4220,4165,4325,4335,1940,2740,2265,2755,2051,2075,1985,2190,2815,2600,2720,1985,1800,1985,2070,1800,3365,3735,3570,3535,3155,2965,2720,3430,3210,3380,3070,3620,3410,3425,3445,3205,4080,2155,2560,2300,2230,2515,2745,2855,2405,2830,3140,2795,3410,1990,2135,3245,2990,2890,3265,3360,3840,3725,3955,3830,4360,4054,3605,3940,1925,1975,1915,2670,3530,3900,3190,3420,2200,2150,2020,2130,2670,2595,2700,2556,2144,1968,2120,2019,2678,2870,3003,3381,2188,2711,2542,2434,2265,2110,2800,2110,2085,2335,2950,3250,1850,1835,2145,1845,2910,2420,2500,2905,2290,2490,2635,2620,2725,2385,1755,1875,1760,2065,1975,2050,1985,2215,2045,2380,2190,2320,2210,2350,2615,2635,3230,2800,3160,2900,2930,3415,3725,3060,3465,2605,2640,2395,2575,2525,2735,2865,3035,1980,2025,1970,2125,2125,2160,2205,2245,1965,1965,1995,2945,3015,2585,2835,2665,2370,2950,2790,2130,2295,2625,2720],"y":{"__ndarray__":"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","dtype":"float64","order":"little","shape":[406]}},"selected":{"id":"12475"},"selection_policy":{"id":"12476"}},"id":"12189","type":"ColumnDataSource"},{"attributes":{},"id":"12161","type":"DataRange1d"},{"attributes":{"axis":{"id":"12167"},"ticker":null},"id":"12170","type":"Grid"}],"root_ids":["12156"]},"title":"Bokeh Application","version":"2.1.1"}}
        </script>
        <script type="text/javascript">
          (function() {
            var fn = function() {
              Bokeh.safely(function() {
                (function(root) {
                  function embed_document(root) {
                    
                  var docs_json = document.getElementById('12621').textContent;
                  var render_items = [{"docid":"8535aaba-4692-4931-9d8e-629e6ac7abd8","root_ids":["12156"],"roots":{"12156":"cf29326c-833c-4c60-b0c7-cde9caae4102"}}];
                  root.Bokeh.embed.embed_items(docs_json, render_items);
                
                  }
                  if (root.Bokeh !== undefined) {
                    embed_document(root);
                  } else {
                    var attempts = 0;
                    var timer = setInterval(function(root) {
                      if (root.Bokeh !== undefined) {
                        clearInterval(timer);
                        embed_document(root);
                      } else {
                        attempts++;
                        if (attempts > 100) {
                          clearInterval(timer);
                          console.log("Bokeh: ERROR: Unable to run BokehJS code because BokehJS library is missing");
                        }
                      }
                    }, 10, root)
                  }
                })(window);
              });
            };
            if (document.readyState != "loading") fn();
            else document.addEventListener("DOMContentLoaded", fn);
          })();
        </script>
    
  </body>

## Scatter Plot for Categorical Data
We can use the famous *iris* dataset to plot categorical data. This dataset contains attributes about three different flower species: setosa, versicolor, virginica. 



```python
# load iris df from vega
df_iris = vds.iris()
df_iris.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>sepalLength</th>
      <th>sepalWidth</th>
      <th>petalLength</th>
      <th>petalWidth</th>
      <th>species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
  </tbody>
</table>

```python
from bokeh.transform import factor_cmap, factor_mark

# load data
species = ['setosa', 'versicolor', 'virginica']
markers = ['hex', 'cross', 'triangle']

sub_scatter = figure(plot_width=600,
                     plot_height=400, 
                     title='Iris Scatter Plot',
                     x_axis_label='Petal Length',
                     y_axis_label='Petal Width')

sub_scatter.scatter(x='petalLength',
                    y='petalWidth',
                    source=df_iris,
                    legend_label='species',
                    fill_alpha=0.5,
                    size=15,
                    color=factor_cmap(field_name='species', palette='Dark2_4', factors=species),
                    marker=factor_mark('species', markers, species))

sub_scatter.legend.location="top_left"
output_file('/sub_scatter.html')
show(sub_scatter)
```

<head>
    
      <meta charset="utf-8">
      <title>Bokeh Plot</title>
      
      
        
          
        
        
          
        <script type="text/javascript" src="https://cdn.bokeh.org/bokeh/release/bokeh-2.1.1.min.js" integrity="sha384-kLr4fYcqcSpbuI95brIH3vnnYCquzzSxHPU6XGQCIkQRGJwhg0StNbj1eegrHs12" crossorigin="anonymous"></script>
        <script type="text/javascript">
            Bokeh.set_log_level("info");
        </script>
        
      
      
    
  </head>
  
  
  <body>
    
      
        
          
          
            
              <div class="bk-root" id="75e14808-8c3c-4340-a701-e24611331403" data-root-id="3498"></div>
            
          
        
      
      
        <script type="application/json" id="3780">
          {"ff101cdc-1d82-4d46-83cb-8d8f5fb9ae77":{"roots":{"references":[{"attributes":{"below":[{"id":"3509"}],"center":[{"id":"3512"},{"id":"3516"},{"id":"3547"}],"left":[{"id":"3513"}],"plot_height":400,"renderers":[{"id":"3537"}],"title":{"id":"3499"},"toolbar":{"id":"3524"},"x_range":{"id":"3501"},"x_scale":{"id":"3505"},"y_range":{"id":"3503"},"y_scale":{"id":"3507"}},"id":"3498","subtype":"Figure","type":"Plot"},{"attributes":{},"id":"3501","type":"DataRange1d"},{"attributes":{"active_drag":"auto","active_inspect":"auto","active_multi":null,"active_scroll":"auto","active_tap":"auto","tools":[{"id":"3517"},{"id":"3518"},{"id":"3519"},{"id":"3520"},{"id":"3521"},{"id":"3522"}]},"id":"3524","type":"Toolbar"},{"attributes":{},"id":"3503","type":"DataRange1d"},{"attributes":{},"id":"3505","type":"LinearScale"},{"attributes":{},"id":"3507","type":"LinearScale"},{"attributes":{"axis_label":"Petal Length","formatter":{"id":"3542"},"ticker":{"id":"3510"}},"id":"3509","type":"LinearAxis"},{"attributes":{"bottom_units":"screen","fill_alpha":0.5,"fill_color":"lightgrey","left_units":"screen","level":"overlay","line_alpha":1.0,"line_color":"black","line_dash":[4,4],"line_width":2,"right_units":"screen","top_units":"screen"},"id":"3523","type":"BoxAnnotation"},{"attributes":{},"id":"3510","type":"BasicTicker"},{"attributes":{"axis":{"id":"3509"},"ticker":null},"id":"3512","type":"Grid"},{"attributes":{},"id":"3540","type":"BasicTickFormatter"},{"attributes":{"axis_label":"Petal Width","formatter":{"id":"3540"},"ticker":{"id":"3514"}},"id":"3513","type":"LinearAxis"},{"attributes":{"data_source":{"id":"3533"},"glyph":{"id":"3535"},"hover_glyph":null,"muted_glyph":null,"nonselection_glyph":{"id":"3536"},"selection_glyph":null,"view":{"id":"3538"}},"id":"3537","type":"GlyphRenderer"},{"attributes":{},"id":"3514","type":"BasicTicker"},{"attributes":{"source":{"id":"3533"}},"id":"3538","type":"CDSView"},{"attributes":{"axis":{"id":"3513"},"dimension":1,"ticker":null},"id":"3516","type":"Grid"},{"attributes":{"fill_alpha":{"value":0.1},"fill_color":{"field":"species","transform":{"id":"3531"}},"line_alpha":{"value":0.1},"line_color":{"field":"species","transform":{"id":"3531"}},"marker":{"field":"species","transform":{"id":"3532"}},"size":{"units":"screen","value":15},"x":{"field":"petalLength"},"y":{"field":"petalWidth"}},"id":"3536","type":"Scatter"},{"attributes":{"data":{"index":[0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,85,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100,101,102,103,104,105,106,107,108,109,110,111,112,113,114,115,116,117,118,119,120,121,122,123,124,125,126,127,128,129,130,131,132,133,134,135,136,137,138,139,140,141,142,143,144,145,146,147,148,149],"petalLength":{"__ndarray__":"ZmZmZmZm9j9mZmZmZmb2P83MzMzMzPQ/AAAAAAAA+D9mZmZmZmb2PzQzMzMzM/s/ZmZmZmZm9j8AAAAAAAD4P2ZmZmZmZvY/AAAAAAAA+D8AAAAAAAD4P5qZmZmZmfk/ZmZmZmZm9j+amZmZmZnxPzMzMzMzM/M/AAAAAAAA+D/NzMzMzMz0P2ZmZmZmZvY/NDMzMzMz+z8AAAAAAAD4PzQzMzMzM/s/AAAAAAAA+D8AAAAAAADwPzQzMzMzM/s/ZmZmZmZm/j+amZmZmZn5P5qZmZmZmfk/AAAAAAAA+D9mZmZmZmb2P5qZmZmZmfk/mpmZmZmZ+T8AAAAAAAD4PwAAAAAAAPg/ZmZmZmZm9j8AAAAAAAD4PzMzMzMzM/M/zczMzMzM9D9mZmZmZmb2P83MzMzMzPQ/AAAAAAAA+D/NzMzMzMz0P83MzMzMzPQ/zczMzMzM9D+amZmZmZn5P2ZmZmZmZv4/ZmZmZmZm9j+amZmZmZn5P2ZmZmZmZvY/AAAAAAAA+D9mZmZmZmb2P83MzMzMzBJAAAAAAAAAEkCamZmZmZkTQAAAAAAAABBAZmZmZmZmEkAAAAAAAAASQM3MzMzMzBJAZmZmZmZmCkBmZmZmZmYSQDMzMzMzMw9AAAAAAAAADEDNzMzMzMwQQAAAAAAAABBAzczMzMzMEkDNzMzMzMwMQJqZmZmZmRFAAAAAAAAAEkBmZmZmZmYQQAAAAAAAABJAMzMzMzMzD0AzMzMzMzMTQAAAAAAAABBAmpmZmZmZE0DNzMzMzMwSQDMzMzMzMxFAmpmZmZmZEUAzMzMzMzMTQAAAAAAAABRAAAAAAAAAEkAAAAAAAAAMQGZmZmZmZg5AmpmZmZmZDUAzMzMzMzMPQGZmZmZmZhRAAAAAAAAAEkAAAAAAAAASQM3MzMzMzBJAmpmZmZmZEUBmZmZmZmYQQAAAAAAAABBAmpmZmZmZEUBmZmZmZmYSQAAAAAAAABBAZmZmZmZmCkDNzMzMzMwQQM3MzMzMzBBAzczMzMzMEEAzMzMzMzMRQAAAAAAAAAhAZmZmZmZmEEAAAAAAAAAYQGZmZmZmZhRAmpmZmZmZF0BmZmZmZmYWQDMzMzMzMxdAZmZmZmZmGkAAAAAAAAASQDMzMzMzMxlAMzMzMzMzF0BmZmZmZmYYQGZmZmZmZhRAMzMzMzMzFUAAAAAAAAAWQAAAAAAAABRAZmZmZmZmFEAzMzMzMzMVQAAAAAAAABZAzczMzMzMGkCamZmZmZkbQAAAAAAAABRAzczMzMzMFkCamZmZmZkTQM3MzMzMzBpAmpmZmZmZE0DNzMzMzMwWQAAAAAAAABhAMzMzMzMzE0CamZmZmZkTQGZmZmZmZhZAMzMzMzMzF0BmZmZmZmYYQJqZmZmZmRlAZmZmZmZmFkBmZmZmZmYUQGZmZmZmZhZAZmZmZmZmGEBmZmZmZmYWQAAAAAAAABZAMzMzMzMzE0CamZmZmZkVQGZmZmZmZhZAZmZmZmZmFEBmZmZmZmYUQJqZmZmZmRdAzczMzMzMFkDNzMzMzMwUQAAAAAAAABRAzczMzMzMFECamZmZmZkVQGZmZmZmZhRA","dtype":"float64","order":"little","shape":[150]},"petalWidth":{"__ndarray__":"mpmZmZmZyT+amZmZmZnJP5qZmZmZmck/mpmZmZmZyT+amZmZmZnJP5qZmZmZmdk/NDMzMzMz0z+amZmZmZnJP5qZmZmZmck/mpmZmZmZuT+amZmZmZnJP5qZmZmZmck/mpmZmZmZuT+amZmZmZm5P5qZmZmZmck/mpmZmZmZ2T+amZmZmZnZPzQzMzMzM9M/NDMzMzMz0z80MzMzMzPTP5qZmZmZmck/mpmZmZmZ2T+amZmZmZnJPwAAAAAAAOA/mpmZmZmZyT+amZmZmZnJP5qZmZmZmdk/mpmZmZmZyT+amZmZmZnJP5qZmZmZmck/mpmZmZmZyT+amZmZmZnZP5qZmZmZmbk/mpmZmZmZyT+amZmZmZnJP5qZmZmZmck/mpmZmZmZyT+amZmZmZm5P5qZmZmZmck/mpmZmZmZyT80MzMzMzPTPzQzMzMzM9M/mpmZmZmZyT80MzMzMzPjP5qZmZmZmdk/NDMzMzMz0z+amZmZmZnJP5qZmZmZmck/mpmZmZmZyT+amZmZmZnJP2ZmZmZmZvY/AAAAAAAA+D8AAAAAAAD4P83MzMzMzPQ/AAAAAAAA+D/NzMzMzMz0P5qZmZmZmfk/AAAAAAAA8D/NzMzMzMz0P2ZmZmZmZvY/AAAAAAAA8D8AAAAAAAD4PwAAAAAAAPA/ZmZmZmZm9j/NzMzMzMz0P2ZmZmZmZvY/AAAAAAAA+D8AAAAAAADwPwAAAAAAAPg/mpmZmZmZ8T/NzMzMzMz8P83MzMzMzPQ/AAAAAAAA+D8zMzMzMzPzP83MzMzMzPQ/ZmZmZmZm9j9mZmZmZmb2PzQzMzMzM/s/AAAAAAAA+D8AAAAAAADwP5qZmZmZmfE/AAAAAAAA8D8zMzMzMzPzP5qZmZmZmfk/AAAAAAAA+D+amZmZmZn5PwAAAAAAAPg/zczMzMzM9D/NzMzMzMz0P83MzMzMzPQ/MzMzMzMz8z9mZmZmZmb2PzMzMzMzM/M/AAAAAAAA8D/NzMzMzMz0PzMzMzMzM/M/zczMzMzM9D/NzMzMzMz0P5qZmZmZmfE/zczMzMzM9D8AAAAAAAAEQGZmZmZmZv4/zczMzMzMAEDNzMzMzMz8P5qZmZmZmQFAzczMzMzMAEA0MzMzMzP7P83MzMzMzPw/zczMzMzM/D8AAAAAAAAEQAAAAAAAAABAZmZmZmZm/j/NzMzMzMwAQAAAAAAAAABAMzMzMzMzA0BmZmZmZmYCQM3MzMzMzPw/mpmZmZmZAUBmZmZmZmYCQAAAAAAAAPg/ZmZmZmZmAkAAAAAAAAAAQAAAAAAAAABAzczMzMzM/D/NzMzMzMwAQM3MzMzMzPw/zczMzMzM/D/NzMzMzMz8P83MzMzMzABAmpmZmZmZ+T9mZmZmZmb+PwAAAAAAAABAmpmZmZmZAUAAAAAAAAD4P2ZmZmZmZvY/ZmZmZmZmAkAzMzMzMzMDQM3MzMzMzPw/zczMzMzM/D/NzMzMzMwAQDMzMzMzMwNAZmZmZmZmAkBmZmZmZmb+P2ZmZmZmZgJAAAAAAAAABEBmZmZmZmYCQGZmZmZmZv4/AAAAAAAAAEBmZmZmZmYCQM3MzMzMzPw/","dtype":"float64","order":"little","shape":[150]},"sepalLength":{"__ndarray__":"ZmZmZmZmFECamZmZmZkTQM3MzMzMzBJAZmZmZmZmEkAAAAAAAAAUQJqZmZmZmRVAZmZmZmZmEkAAAAAAAAAUQJqZmZmZmRFAmpmZmZmZE0CamZmZmZkVQDMzMzMzMxNAMzMzMzMzE0AzMzMzMzMRQDMzMzMzMxdAzczMzMzMFkCamZmZmZkVQGZmZmZmZhRAzczMzMzMFkBmZmZmZmYUQJqZmZmZmRVAZmZmZmZmFEBmZmZmZmYSQGZmZmZmZhRAMzMzMzMzE0AAAAAAAAAUQAAAAAAAABRAzczMzMzMFEDNzMzMzMwUQM3MzMzMzBJAMzMzMzMzE0CamZmZmZkVQM3MzMzMzBRAAAAAAAAAFkCamZmZmZkTQAAAAAAAABRAAAAAAAAAFkCamZmZmZkTQJqZmZmZmRFAZmZmZmZmFEAAAAAAAAAUQAAAAAAAABJAmpmZmZmZEUAAAAAAAAAUQGZmZmZmZhRAMzMzMzMzE0BmZmZmZmYUQGZmZmZmZhJAMzMzMzMzFUAAAAAAAAAUQAAAAAAAABxAmpmZmZmZGUCamZmZmZkbQAAAAAAAABZAAAAAAAAAGkDNzMzMzMwWQDMzMzMzMxlAmpmZmZmZE0BmZmZmZmYaQM3MzMzMzBRAAAAAAAAAFECamZmZmZkXQAAAAAAAABhAZmZmZmZmGEBmZmZmZmYWQM3MzMzMzBpAZmZmZmZmFkAzMzMzMzMXQM3MzMzMzBhAZmZmZmZmFkCamZmZmZkXQGZmZmZmZhhAMzMzMzMzGUBmZmZmZmYYQJqZmZmZmRlAZmZmZmZmGkAzMzMzMzMbQM3MzMzMzBpAAAAAAAAAGEDNzMzMzMwWQAAAAAAAABZAAAAAAAAAFkAzMzMzMzMXQAAAAAAAABhAmpmZmZmZFUAAAAAAAAAYQM3MzMzMzBpAMzMzMzMzGUBmZmZmZmYWQAAAAAAAABZAAAAAAAAAFkBmZmZmZmYYQDMzMzMzMxdAAAAAAAAAFEBmZmZmZmYWQM3MzMzMzBZAzczMzMzMFkDNzMzMzMwYQGZmZmZmZhRAzczMzMzMFkAzMzMzMzMZQDMzMzMzMxdAZmZmZmZmHEAzMzMzMzMZQAAAAAAAABpAZmZmZmZmHkCamZmZmZkTQDMzMzMzMx1AzczMzMzMGkDNzMzMzMwcQAAAAAAAABpAmpmZmZmZGUAzMzMzMzMbQM3MzMzMzBZAMzMzMzMzF0CamZmZmZkZQAAAAAAAABpAzczMzMzMHkDNzMzMzMweQAAAAAAAABhAmpmZmZmZG0BmZmZmZmYWQM3MzMzMzB5AMzMzMzMzGUDNzMzMzMwaQM3MzMzMzBxAzczMzMzMGEBmZmZmZmYYQJqZmZmZmRlAzczMzMzMHECamZmZmZkdQJqZmZmZmR9AmpmZmZmZGUAzMzMzMzMZQGZmZmZmZhhAzczMzMzMHkAzMzMzMzMZQJqZmZmZmRlAAAAAAAAAGECamZmZmZkbQM3MzMzMzBpAmpmZmZmZG0AzMzMzMzMXQDMzMzMzMxtAzczMzMzMGkDNzMzMzMwaQDMzMzMzMxlAAAAAAAAAGkDNzMzMzMwYQJqZmZmZmRdA","dtype":"float64","order":"little","shape":[150]},"sepalWidth":{"__ndarray__":"AAAAAAAADEAAAAAAAAAIQJqZmZmZmQlAzczMzMzMCEDNzMzMzMwMQDMzMzMzMw9AMzMzMzMzC0AzMzMzMzMLQDMzMzMzMwdAzczMzMzMCECamZmZmZkNQDMzMzMzMwtAAAAAAAAACEAAAAAAAAAIQAAAAAAAABBAmpmZmZmZEUAzMzMzMzMPQAAAAAAAAAxAZmZmZmZmDkBmZmZmZmYOQDMzMzMzMwtAmpmZmZmZDUDNzMzMzMwMQGZmZmZmZgpAMzMzMzMzC0AAAAAAAAAIQDMzMzMzMwtAAAAAAAAADEAzMzMzMzMLQJqZmZmZmQlAzczMzMzMCEAzMzMzMzMLQGZmZmZmZhBAzczMzMzMEEDNzMzMzMwIQJqZmZmZmQlAAAAAAAAADEDNzMzMzMwMQAAAAAAAAAhAMzMzMzMzC0AAAAAAAAAMQGZmZmZmZgJAmpmZmZmZCUAAAAAAAAAMQGZmZmZmZg5AAAAAAAAACEBmZmZmZmYOQJqZmZmZmQlAmpmZmZmZDUBmZmZmZmYKQJqZmZmZmQlAmpmZmZmZCUDNzMzMzMwIQGZmZmZmZgJAZmZmZmZmBkBmZmZmZmYGQGZmZmZmZgpAMzMzMzMzA0AzMzMzMzMHQJqZmZmZmQVAAAAAAAAAAEAAAAAAAAAIQJqZmZmZmQFAMzMzMzMzB0AzMzMzMzMHQM3MzMzMzAhAAAAAAAAACECamZmZmZkFQJqZmZmZmQFAAAAAAAAABECamZmZmZkJQGZmZmZmZgZAAAAAAAAABEBmZmZmZmYGQDMzMzMzMwdAAAAAAAAACEBmZmZmZmYGQAAAAAAAAAhAMzMzMzMzB0DNzMzMzMwEQDMzMzMzMwNAMzMzMzMzA0CamZmZmZkFQJqZmZmZmQVAAAAAAAAACEAzMzMzMzMLQM3MzMzMzAhAZmZmZmZmAkAAAAAAAAAIQAAAAAAAAARAzczMzMzMBEAAAAAAAAAIQM3MzMzMzARAZmZmZmZmAkCamZmZmZkFQAAAAAAAAAhAMzMzMzMzB0AzMzMzMzMHQAAAAAAAAARAZmZmZmZmBkBmZmZmZmYKQJqZmZmZmQVAAAAAAAAACEAzMzMzMzMHQAAAAAAAAAhAAAAAAAAACEAAAAAAAAAEQDMzMzMzMwdAAAAAAAAABEDNzMzMzMwMQJqZmZmZmQlAmpmZmZmZBUAAAAAAAAAIQAAAAAAAAARAZmZmZmZmBkCamZmZmZkJQAAAAAAAAAhAZmZmZmZmDkDNzMzMzMwEQJqZmZmZmQFAmpmZmZmZCUBmZmZmZmYGQGZmZmZmZgZAmpmZmZmZBUBmZmZmZmYKQJqZmZmZmQlAZmZmZmZmBkAAAAAAAAAIQGZmZmZmZgZAAAAAAAAACEBmZmZmZmYGQGZmZmZmZg5AZmZmZmZmBkBmZmZmZmYGQM3MzMzMzARAAAAAAAAACEAzMzMzMzMLQM3MzMzMzAhAAAAAAAAACEDNzMzMzMwIQM3MzMzMzAhAzczMzMzMCECamZmZmZkFQJqZmZmZmQlAZmZmZmZmCkAAAAAAAAAIQAAAAAAAAARAAAAAAAAACEAzMzMzMzMLQAAAAAAAAAhA","dtype":"float64","order":"little","shape":[150]},"species":["setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica"]},"selected":{"id":"3546"},"selection_policy":{"id":"3545"}},"id":"3533","type":"ColumnDataSource"},{"attributes":{"factors":["setosa","versicolor","virginica"],"markers":["hex","cross","triangle"]},"id":"3532","type":"CategoricalMarkerMapper"},{"attributes":{"fill_alpha":{"value":0.5},"fill_color":{"field":"species","transform":{"id":"3531"}},"line_color":{"field":"species","transform":{"id":"3531"}},"marker":{"field":"species","transform":{"id":"3532"}},"size":{"units":"screen","value":15},"x":{"field":"petalLength"},"y":{"field":"petalWidth"}},"id":"3535","type":"Scatter"},{"attributes":{},"id":"3542","type":"BasicTickFormatter"},{"attributes":{},"id":"3517","type":"PanTool"},{"attributes":{},"id":"3545","type":"UnionRenderers"},{"attributes":{},"id":"3518","type":"WheelZoomTool"},{"attributes":{},"id":"3546","type":"Selection"},{"attributes":{"factors":["setosa","versicolor","virginica"],"palette":["#1b9e77","#d95f02","#7570b3","#e7298a"]},"id":"3531","type":"CategoricalColorMapper"},{"attributes":{"overlay":{"id":"3523"}},"id":"3519","type":"BoxZoomTool"},{"attributes":{"items":[{"id":"3548"}],"location":"top_left"},"id":"3547","type":"Legend"},{"attributes":{},"id":"3520","type":"SaveTool"},{"attributes":{"label":{"value":"species"},"renderers":[{"id":"3537"}]},"id":"3548","type":"LegendItem"},{"attributes":{},"id":"3521","type":"ResetTool"},{"attributes":{"text":"Iris Scatter Plot"},"id":"3499","type":"Title"},{"attributes":{},"id":"3522","type":"HelpTool"}],"root_ids":["3498"]},"title":"Bokeh Application","version":"2.1.1"}}
        </script>
        <script type="text/javascript">
          (function() {
            var fn = function() {
              Bokeh.safely(function() {
                (function(root) {
                  function embed_document(root) {
                    
                  var docs_json = document.getElementById('3780').textContent;
                  var render_items = [{"docid":"ff101cdc-1d82-4d46-83cb-8d8f5fb9ae77","root_ids":["3498"],"roots":{"3498":"75e14808-8c3c-4340-a701-e24611331403"}}];
                  root.Bokeh.embed.embed_items(docs_json, render_items);
                
                  }
                  if (root.Bokeh !== undefined) {
                    embed_document(root);
                  } else {
                    var attempts = 0;
                    var timer = setInterval(function(root) {
                      if (root.Bokeh !== undefined) {
                        clearInterval(timer);
                        embed_document(root);
                      } else {
                        attempts++;
                        if (attempts > 100) {
                          clearInterval(timer);
                          console.log("Bokeh: ERROR: Unable to run BokehJS code because BokehJS library is missing");
                        }
                      }
                    }, 10, root)
                  }
                })(window);
              });
            };
            if (document.readyState != "loading") fn();
            else document.addEventListener("DOMContentLoaded", fn);
          })();
        </script>
    
  </body>



