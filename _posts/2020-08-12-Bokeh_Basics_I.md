---
title: "Bokeh Basics I"
date: 2020-08-12
tags: [Data Visualization]
excerpt: "Bokeh Basics I"
mathjax: "True"
---




<!DOCTYPE html>
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