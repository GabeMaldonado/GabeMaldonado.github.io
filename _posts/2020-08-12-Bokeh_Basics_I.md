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
Bokeh uses the ColumnDataSource as its main data structure. The ColumnDataSource is created automatically most of the time but it can also be created explicitly. This data structure is a dictionary which maps the column names to sequences of values. 

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