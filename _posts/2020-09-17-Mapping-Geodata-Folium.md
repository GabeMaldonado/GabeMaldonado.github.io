---
title: "Mapping Geodata with Folium"
date: 2020-09-17
tags: [ML&AI]
excerpt: "Using python's Folium to create maps"
mathjax: "True"
---

## Mapping Geographical data with Folium 

Folium is a python librarie used to create maps and to work with geo location data.
For this post I compiled a non-inclusive list of the most emblematic footbal/soccer stadiums around the world and plot them on the map to show their location. 

```python

import folium

loc = 'Emblematic Footbal Stadiums Around the World'
title_html = '''
             <h3 align="center" style="font-size:16px"><b>{}</b></h3>
             '''.format(loc)   


m = folium.Map(
    location=[30.8082, -118.2474],
    zoom_start=3,
    tiles='Stamen Terrain')

folium.Marker(
    location=[-34.63565, -58.36465],
    popup="Estadio 'La Bombonera',  Boca Juniors",
    icon=folium.Icon(color='lightgreen')
).add_to(m)

folium.Marker(
    location=[-34.545319, -58.449736],
    popup='Estadio Monumental Americo Vespucio, River Plate',
    icon=folium.Icon(color='green')
).add_to(m)


folium.Marker(
    location=[-34.670267, -58.370969],
    popup='Estadio Libertadores De América, Club Atlético Independiente',
    icon=folium.Icon(color='green')
).add_to(m)



folium.Marker(
    location=[-25.292072, -57.657381],
    popup='Estadio Defensores del Chaco',
    icon=folium.Icon(color='green')
).add_to(m)

folium.Marker(
    location=[-34.796917, -56.067167],
    popup='Estadio Campeón del Siglo, Peñarol',
    icon=folium.Icon(color='green')
).add_to(m)

folium.Marker(
    location=[-34.884373, -56.1588],
    popup='Estadio Gran Parque Central, Nacional',
    icon=folium.Icon(color='green')
).add_to(m)

folium.Marker(
    location=[-33.506611, -70.605944],
    popup='Estadio Monumental David Arellano, Colo-Colo',
    icon=folium.Icon(color='green')
).add_to(m)

folium.Marker(
    location=[-12.055694, -76.935972],
    popup='Estadio Monumental "U", Club Universitario de Deportes',
    icon=folium.Icon(color='green')
).add_to(m)

folium.Marker(
    location=[0.107717, -78.489103],
    popup='Estadio Rodrigo Paz Delgado, Liga Deportiva Universitaria',
    icon=folium.Icon(color='green')
).add_to(m)

folium.Marker(
    location=[-0.177528, -78.476583],
    popup='Estadio Olímpico Atahualpa',
    icon=folium.Icon(color='green')
).add_to(m)

folium.Marker(
    location=[-2.185869, -79.924931],
    popup='Estadio Isidro Romero Carbo, Barcelona Sporting Club',
    icon=folium.Icon(color='green')
).add_to(m)


folium.Marker(
    location=[40.736667, -74.15027],
    popup='Red Bull Arena, New York Red Bulls',
    icon=folium.Icon(color='green')
).add_to(m)

folium.Marker(
    location=[33.755556, -84.4],
    popup='Estadio Mercedes Benz, Atlanta United',
    icon=folium.Icon(color='green')
).add_to(m)

folium.Marker(
    location=[33.864, -118.261],
    popup='Dignity Health Sports Park, LA Galaxy',
    icon=folium.Icon(color='green')
).add_to(m)


folium.Marker(
    location=[40.4530100, -3.6882900],
    popup='Estadio Santiago Bernabeu, Real Madrid',
    icon=folium.Icon(color='green')
).add_to(m)

folium.Marker(
    location=[41.3808000, 2.1231100],
    popup='Estadio Camp Nou, FC Barcelona',
    icon=folium.Icon(color='green')
).add_to(m)

folium.Marker(
    location=[38.752648359600805, -9.184699058532715],
    popup='Estadio do Sport Lisboa e Benfica',
    icon=folium.Icon(color='green')
).add_to(m)


folium.Marker(
    location=[-22.912167, -43.230164],
    popup='Estadio Maracana',
    icon=folium.Icon(color='green')
).add_to(m)

folium.Marker(
    location=[19.303056, -99.150556],
    popup='Estadio Azteca, Club America',
    icon=folium.Icon(color='green')
).add_to(m)

folium.Marker(
    location=[45.109444, 7.641111],
    popup='Estadio Juventus, Juventus ',
    icon=folium.Icon(color='green')
).add_to(m)


folium.Marker(
    location=[41.102869, 28.990419],
    popup='Estadio Türk Telekom, Galatasaray',
    icon=folium.Icon(color='green')
).add_to(m)


folium.Marker(
    location=[48.841389, 2.253056],
    popup='Estadio Parc des Princes, Paris Saint-Germain ',
    icon=folium.Icon(color='green')
).add_to(m)


folium.Marker(
    location=[48.218775, 11.624753],
    popup='Allianz Arena, Paris Saint-Germain ',
    icon=folium.Icon(color='green')
).add_to(m)

m.get_root().html.add_child(folium.Element(title_html))

m.save('emblematic_football_stadiums.html')
```


<!DOCTYPE html>
<head>    
    <meta http-equiv="content-type" content="text/html; charset=UTF-8" />
    <script>L_PREFER_CANVAS=false; L_NO_TOUCH=false; L_DISABLE_3D=false;</script>
    <script src="https://cdn.jsdelivr.net/npm/leaflet@1.4.0/dist/leaflet.js"></script>
    <script src="https://code.jquery.com/jquery-1.12.4.min.js"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Leaflet.awesome-markers/2.0.2/leaflet.awesome-markers.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/leaflet@1.4.0/dist/leaflet.css"/>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css"/>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css"/>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.6.3/css/font-awesome.min.css"/>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/Leaflet.awesome-markers/2.0.2/leaflet.awesome-markers.css"/>
    <link rel="stylesheet" href="https://rawcdn.githack.com/python-visualization/folium/master/folium/templates/leaflet.awesome.rotate.css"/>
    <style>html, body {width: 100%;height: 100%;margin: 0;padding: 0;}</style>
    <style>#map {position:absolute;top:0;bottom:0;right:0;left:0;}</style>
    
    <meta name="viewport" content="width=device-width,
        initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <style>#map_214cb8bbbf7547989381ecd3ab665230 {
        position: relative;
        width: 100.0%;
        height: 100.0%;
        left: 0.0%;
        top: 0.0%;
        }
    </style>
</head>
<body>    
    
             <h3 align="center" style="font-size:16px"><b>Emblematic Footbal Stadiums Around the World</b></h3>
             
    
    <div class="folium-map" id="map_214cb8bbbf7547989381ecd3ab665230" ></div>
</body>
<script>    
    
    
        var bounds = null;
    

    var map_214cb8bbbf7547989381ecd3ab665230 = L.map(
        'map_214cb8bbbf7547989381ecd3ab665230', {
        center: [30.8082, -118.2474],
        zoom: 3,
        maxBounds: bounds,
        layers: [],
        worldCopyJump: false,
        crs: L.CRS.EPSG3857,
        zoomControl: true,
        });


    
    var tile_layer_89a7a5ee1b09480a937752c262196de2 = L.tileLayer(
        'https://stamen-tiles-{s}.a.ssl.fastly.net/terrain/{z}/{x}/{y}.jpg',
        {
        "attribution": null,
        "detectRetina": false,
        "maxNativeZoom": 18,
        "maxZoom": 18,
        "minZoom": 0,
        "noWrap": false,
        "opacity": 1,
        "subdomains": "abc",
        "tms": false
}).addTo(map_214cb8bbbf7547989381ecd3ab665230);
    
        var marker_7c83297af10148cdb2d9c31bd5a1902d = L.marker(
            [-34.63565, -58.36465],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_14feaba4f73b48b4b4f473a194592cc8 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'lightgreen',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_7c83297af10148cdb2d9c31bd5a1902d.setIcon(icon_14feaba4f73b48b4b4f473a194592cc8);
            
    
            var popup_2baf7ad0cfc74d68b774234d763ca7a0 = L.popup({maxWidth: '100%'
            
            });

            
                var html_37252790d9a6422a99cb05fece9a1696 = $(`<div id="html_37252790d9a6422a99cb05fece9a1696" style="width: 100.0%; height: 100.0%;">Estadio 'La Bombonera',  Boca Juniors</div>`)[0];
                popup_2baf7ad0cfc74d68b774234d763ca7a0.setContent(html_37252790d9a6422a99cb05fece9a1696);
            

            marker_7c83297af10148cdb2d9c31bd5a1902d.bindPopup(popup_2baf7ad0cfc74d68b774234d763ca7a0)
            ;

            
        
    
        var marker_032c952e82184ad1828f64ce9f6edee8 = L.marker(
            [-34.545319, -58.449736],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_b2610f4e43b04edbb84a500e3ea2ffe8 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_032c952e82184ad1828f64ce9f6edee8.setIcon(icon_b2610f4e43b04edbb84a500e3ea2ffe8);
            
    
            var popup_ba16d520d5a84ab595f769d89ad7d6c9 = L.popup({maxWidth: '100%'
            
            });

            
                var html_6d0d89e4293244639ca7aac630d45980 = $(`<div id="html_6d0d89e4293244639ca7aac630d45980" style="width: 100.0%; height: 100.0%;">Estadio Monumental Americo Vespucio, River Plate</div>`)[0];
                popup_ba16d520d5a84ab595f769d89ad7d6c9.setContent(html_6d0d89e4293244639ca7aac630d45980);
            

            marker_032c952e82184ad1828f64ce9f6edee8.bindPopup(popup_ba16d520d5a84ab595f769d89ad7d6c9)
            ;

            
        
    
        var marker_8b2c7d12f3534e50b6f50669a64fcccf = L.marker(
            [-34.670267, -58.370969],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_1e7902b47cf74e7c94d15792e3a13f06 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_8b2c7d12f3534e50b6f50669a64fcccf.setIcon(icon_1e7902b47cf74e7c94d15792e3a13f06);
            
    
            var popup_05745c56cb1647b98ccf08732c90f637 = L.popup({maxWidth: '100%'
            
            });

            
                var html_ec99e6870a0447289d4d5e46bb272b9f = $(`<div id="html_ec99e6870a0447289d4d5e46bb272b9f" style="width: 100.0%; height: 100.0%;">Estadio Libertadores De América, Club Atlético Independiente</div>`)[0];
                popup_05745c56cb1647b98ccf08732c90f637.setContent(html_ec99e6870a0447289d4d5e46bb272b9f);
            

            marker_8b2c7d12f3534e50b6f50669a64fcccf.bindPopup(popup_05745c56cb1647b98ccf08732c90f637)
            ;

            
        
    
        var marker_c6a982a10ad740e584a4450a9b8cdfb8 = L.marker(
            [-25.292072, -57.657381],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_42c3158c2f0b43b28a0df3d2d0e5aba1 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_c6a982a10ad740e584a4450a9b8cdfb8.setIcon(icon_42c3158c2f0b43b28a0df3d2d0e5aba1);
            
    
            var popup_6fbfb38003754d4196050a6e402f0d18 = L.popup({maxWidth: '100%'
            
            });

            
                var html_e28f6ecd9a564773b69a7182aeaf63de = $(`<div id="html_e28f6ecd9a564773b69a7182aeaf63de" style="width: 100.0%; height: 100.0%;">Estadio Defensores del Chaco</div>`)[0];
                popup_6fbfb38003754d4196050a6e402f0d18.setContent(html_e28f6ecd9a564773b69a7182aeaf63de);
            

            marker_c6a982a10ad740e584a4450a9b8cdfb8.bindPopup(popup_6fbfb38003754d4196050a6e402f0d18)
            ;

            
        
    
        var marker_e7ae9448ba914ff6ae2d99362c5229e0 = L.marker(
            [-34.796917, -56.067167],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_022f6b920e5c41f78436119f75b68e77 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_e7ae9448ba914ff6ae2d99362c5229e0.setIcon(icon_022f6b920e5c41f78436119f75b68e77);
            
    
            var popup_7de83ca45d3b4c3f9d89a28cab5f3454 = L.popup({maxWidth: '100%'
            
            });

            
                var html_23b9a77ba73542ec9b9a248bb75fa805 = $(`<div id="html_23b9a77ba73542ec9b9a248bb75fa805" style="width: 100.0%; height: 100.0%;">Estadio Campeón del Siglo, Peñarol</div>`)[0];
                popup_7de83ca45d3b4c3f9d89a28cab5f3454.setContent(html_23b9a77ba73542ec9b9a248bb75fa805);
            

            marker_e7ae9448ba914ff6ae2d99362c5229e0.bindPopup(popup_7de83ca45d3b4c3f9d89a28cab5f3454)
            ;

            
        
    
        var marker_3eb0e2f49d2d4a71859439d2b83fd290 = L.marker(
            [-34.884373, -56.1588],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_5909565a96194903bc980d7af902d644 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_3eb0e2f49d2d4a71859439d2b83fd290.setIcon(icon_5909565a96194903bc980d7af902d644);
            
    
            var popup_1b32ecfb012f4ef9bdd09ce9f3d69280 = L.popup({maxWidth: '100%'
            
            });

            
                var html_707df571bfc74accb5e8d5618a50e462 = $(`<div id="html_707df571bfc74accb5e8d5618a50e462" style="width: 100.0%; height: 100.0%;">Estadio Gran Parque Central, Nacional</div>`)[0];
                popup_1b32ecfb012f4ef9bdd09ce9f3d69280.setContent(html_707df571bfc74accb5e8d5618a50e462);
            

            marker_3eb0e2f49d2d4a71859439d2b83fd290.bindPopup(popup_1b32ecfb012f4ef9bdd09ce9f3d69280)
            ;

            
        
    
        var marker_6794c26d5aa241869060da2474cac258 = L.marker(
            [-33.506611, -70.605944],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_074d3a2a8680444a8059060217033eb0 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_6794c26d5aa241869060da2474cac258.setIcon(icon_074d3a2a8680444a8059060217033eb0);
            
    
            var popup_f72bef8150fd4aec85ce596ccc2ffd52 = L.popup({maxWidth: '100%'
            
            });

            
                var html_455e65c972ae41ae94e202aab81200e8 = $(`<div id="html_455e65c972ae41ae94e202aab81200e8" style="width: 100.0%; height: 100.0%;">Estadio Monumental David Arellano, Colo-Colo</div>`)[0];
                popup_f72bef8150fd4aec85ce596ccc2ffd52.setContent(html_455e65c972ae41ae94e202aab81200e8);
            

            marker_6794c26d5aa241869060da2474cac258.bindPopup(popup_f72bef8150fd4aec85ce596ccc2ffd52)
            ;

            
        
    
        var marker_3df23473762848cca8bc2365aba3f8c0 = L.marker(
            [-12.055694, -76.935972],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_f6530307d8c34ecea88ce108563290d3 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_3df23473762848cca8bc2365aba3f8c0.setIcon(icon_f6530307d8c34ecea88ce108563290d3);
            
    
            var popup_1d6202af4339498e8df748bbac61e487 = L.popup({maxWidth: '100%'
            
            });

            
                var html_679d6a894ee644e4a5074eb2a467fbc8 = $(`<div id="html_679d6a894ee644e4a5074eb2a467fbc8" style="width: 100.0%; height: 100.0%;">Estadio Monumental "U", Club Universitario de Deportes</div>`)[0];
                popup_1d6202af4339498e8df748bbac61e487.setContent(html_679d6a894ee644e4a5074eb2a467fbc8);
            

            marker_3df23473762848cca8bc2365aba3f8c0.bindPopup(popup_1d6202af4339498e8df748bbac61e487)
            ;

            
        
    
        var marker_f131eef77490429a8bbb48bec1c64016 = L.marker(
            [0.107717, -78.489103],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_709a7c6081544aacaed43deb53ec61f2 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_f131eef77490429a8bbb48bec1c64016.setIcon(icon_709a7c6081544aacaed43deb53ec61f2);
            
    
            var popup_1f7bc8cde3024ea69d77edcf706309cb = L.popup({maxWidth: '100%'
            
            });

            
                var html_046a043c75b0414488a58f37d5295fb0 = $(`<div id="html_046a043c75b0414488a58f37d5295fb0" style="width: 100.0%; height: 100.0%;">Estadio Rodrigo Paz Delgado, Liga Deportiva Universitaria</div>`)[0];
                popup_1f7bc8cde3024ea69d77edcf706309cb.setContent(html_046a043c75b0414488a58f37d5295fb0);
            

            marker_f131eef77490429a8bbb48bec1c64016.bindPopup(popup_1f7bc8cde3024ea69d77edcf706309cb)
            ;

            
        
    
        var marker_cbde37c1743445ffb27d5a65497c351a = L.marker(
            [-0.177528, -78.476583],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_fa4775f4d56e459091d31c7d9b1e4072 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_cbde37c1743445ffb27d5a65497c351a.setIcon(icon_fa4775f4d56e459091d31c7d9b1e4072);
            
    
            var popup_a582dde559214dbab9065775fec1d8dd = L.popup({maxWidth: '100%'
            
            });

            
                var html_c80220df55344c12b05fb5ceb38120f4 = $(`<div id="html_c80220df55344c12b05fb5ceb38120f4" style="width: 100.0%; height: 100.0%;">Estadio Olímpico Atahualpa</div>`)[0];
                popup_a582dde559214dbab9065775fec1d8dd.setContent(html_c80220df55344c12b05fb5ceb38120f4);
            

            marker_cbde37c1743445ffb27d5a65497c351a.bindPopup(popup_a582dde559214dbab9065775fec1d8dd)
            ;

            
        
    
        var marker_52fe7037b3c54862b1335b7e2601576b = L.marker(
            [-2.185869, -79.924931],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_c5ce581679524f5997b1466db8634314 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_52fe7037b3c54862b1335b7e2601576b.setIcon(icon_c5ce581679524f5997b1466db8634314);
            
    
            var popup_86fb9858c3f64326a22abdd8744a59cf = L.popup({maxWidth: '100%'
            
            });

            
                var html_248e41b353e046d0a98d06ce1579105f = $(`<div id="html_248e41b353e046d0a98d06ce1579105f" style="width: 100.0%; height: 100.0%;">Estadio Isidro Romero Carbo, Barcelona Sporting Club</div>`)[0];
                popup_86fb9858c3f64326a22abdd8744a59cf.setContent(html_248e41b353e046d0a98d06ce1579105f);
            

            marker_52fe7037b3c54862b1335b7e2601576b.bindPopup(popup_86fb9858c3f64326a22abdd8744a59cf)
            ;

            
        
    
        var marker_443c7efad0e2443b927e6f02b828257c = L.marker(
            [40.736667, -74.15027],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_4b79bf50369a45efa8e4ca5cd861a0c7 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_443c7efad0e2443b927e6f02b828257c.setIcon(icon_4b79bf50369a45efa8e4ca5cd861a0c7);
            
    
            var popup_83961ad87850403a85ba4bc4cb214f92 = L.popup({maxWidth: '100%'
            
            });

            
                var html_22138188bb704092bfe46c68998366c8 = $(`<div id="html_22138188bb704092bfe46c68998366c8" style="width: 100.0%; height: 100.0%;">Red Bull Arena, New York Red Bulls</div>`)[0];
                popup_83961ad87850403a85ba4bc4cb214f92.setContent(html_22138188bb704092bfe46c68998366c8);
            

            marker_443c7efad0e2443b927e6f02b828257c.bindPopup(popup_83961ad87850403a85ba4bc4cb214f92)
            ;

            
        
    
        var marker_0e872677c2694856a352ae46fe261d04 = L.marker(
            [33.755556, -84.4],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_e582278ffc8042339035b1b32caf101d = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_0e872677c2694856a352ae46fe261d04.setIcon(icon_e582278ffc8042339035b1b32caf101d);
            
    
            var popup_08c1f2490f6e44a093f81a6e49877c6d = L.popup({maxWidth: '100%'
            
            });

            
                var html_25fe0b9999f44b879595f40987b34b68 = $(`<div id="html_25fe0b9999f44b879595f40987b34b68" style="width: 100.0%; height: 100.0%;">Estadio Mercedes Benz, Atlanta United</div>`)[0];
                popup_08c1f2490f6e44a093f81a6e49877c6d.setContent(html_25fe0b9999f44b879595f40987b34b68);
            

            marker_0e872677c2694856a352ae46fe261d04.bindPopup(popup_08c1f2490f6e44a093f81a6e49877c6d)
            ;

            
        
    
        var marker_7e72724857184ef8b1985a9c406d42d6 = L.marker(
            [33.864, -118.261],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_d578883b89f34edca8b63a44749778c8 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_7e72724857184ef8b1985a9c406d42d6.setIcon(icon_d578883b89f34edca8b63a44749778c8);
            
    
            var popup_835afd6b53b04cca9e6c9b10d24ff2b6 = L.popup({maxWidth: '100%'
            
            });

            
                var html_8e7992809d4344348553d69e186458f3 = $(`<div id="html_8e7992809d4344348553d69e186458f3" style="width: 100.0%; height: 100.0%;">Dignity Health Sports Park, LA Galaxy</div>`)[0];
                popup_835afd6b53b04cca9e6c9b10d24ff2b6.setContent(html_8e7992809d4344348553d69e186458f3);
            

            marker_7e72724857184ef8b1985a9c406d42d6.bindPopup(popup_835afd6b53b04cca9e6c9b10d24ff2b6)
            ;

            
        
    
        var marker_f93243f6c0284684aa5a070ff70ee14c = L.marker(
            [40.45301, -3.68829],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_1c6178d5f8c84d39a3c8ce65e26c4896 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_f93243f6c0284684aa5a070ff70ee14c.setIcon(icon_1c6178d5f8c84d39a3c8ce65e26c4896);
            
    
            var popup_9c649a0058954b20b7bd00a2e736b9f0 = L.popup({maxWidth: '100%'
            
            });

            
                var html_7c3d13fa912748659834ad6e5dc91c39 = $(`<div id="html_7c3d13fa912748659834ad6e5dc91c39" style="width: 100.0%; height: 100.0%;">Estadio Santiago Bernabeu, Real Madrid</div>`)[0];
                popup_9c649a0058954b20b7bd00a2e736b9f0.setContent(html_7c3d13fa912748659834ad6e5dc91c39);
            

            marker_f93243f6c0284684aa5a070ff70ee14c.bindPopup(popup_9c649a0058954b20b7bd00a2e736b9f0)
            ;

            
        
    
        var marker_34ee54a3209741e09406f614d2334d0a = L.marker(
            [41.3808, 2.12311],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_3d8f04a490174a8881f20783edf08156 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_34ee54a3209741e09406f614d2334d0a.setIcon(icon_3d8f04a490174a8881f20783edf08156);
            
    
            var popup_2ec2682d4e094e2fb851807723735b9a = L.popup({maxWidth: '100%'
            
            });

            
                var html_8db508af4dc1429da791466dd9764cd3 = $(`<div id="html_8db508af4dc1429da791466dd9764cd3" style="width: 100.0%; height: 100.0%;">Estadio Camp Nou, FC Barcelona</div>`)[0];
                popup_2ec2682d4e094e2fb851807723735b9a.setContent(html_8db508af4dc1429da791466dd9764cd3);
            

            marker_34ee54a3209741e09406f614d2334d0a.bindPopup(popup_2ec2682d4e094e2fb851807723735b9a)
            ;

            
        
    
        var marker_e06e0846bd23477383f1e34a2a4ac19b = L.marker(
            [38.752648359600805, -9.184699058532715],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_f30dd81e77da49b9a3c444ff6263bcbb = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_e06e0846bd23477383f1e34a2a4ac19b.setIcon(icon_f30dd81e77da49b9a3c444ff6263bcbb);
            
    
            var popup_9a06c81c97074546b8a7de416c76effa = L.popup({maxWidth: '100%'
            
            });

            
                var html_e6caae6806c6454cbf1bc227aea04988 = $(`<div id="html_e6caae6806c6454cbf1bc227aea04988" style="width: 100.0%; height: 100.0%;">Estadio do Sport Lisboa e Benfica</div>`)[0];
                popup_9a06c81c97074546b8a7de416c76effa.setContent(html_e6caae6806c6454cbf1bc227aea04988);
            

            marker_e06e0846bd23477383f1e34a2a4ac19b.bindPopup(popup_9a06c81c97074546b8a7de416c76effa)
            ;

            
        
    
        var marker_d9fb3876f19540af83a782a5643e4781 = L.marker(
            [-22.912167, -43.230164],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_63896540b26e4b569a602ddeb8ef47e8 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_d9fb3876f19540af83a782a5643e4781.setIcon(icon_63896540b26e4b569a602ddeb8ef47e8);
            
    
            var popup_418ba9f4b57b42f5b576ad2cd79e5732 = L.popup({maxWidth: '100%'
            
            });

            
                var html_8e2d7dd6fa974c89a41700214f9c5f19 = $(`<div id="html_8e2d7dd6fa974c89a41700214f9c5f19" style="width: 100.0%; height: 100.0%;">Estadio Maracana</div>`)[0];
                popup_418ba9f4b57b42f5b576ad2cd79e5732.setContent(html_8e2d7dd6fa974c89a41700214f9c5f19);
            

            marker_d9fb3876f19540af83a782a5643e4781.bindPopup(popup_418ba9f4b57b42f5b576ad2cd79e5732)
            ;

            
        
    
        var marker_c579a2b52d524646b1a3c51f6f46f2a8 = L.marker(
            [19.303056, -99.150556],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_3fea1f48e80040b3ad8c252fff2b987c = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_c579a2b52d524646b1a3c51f6f46f2a8.setIcon(icon_3fea1f48e80040b3ad8c252fff2b987c);
            
    
            var popup_92f2462693ea499ea79a950003586b5d = L.popup({maxWidth: '100%'
            
            });

            
                var html_ebd4497b4c9c48338ff70a756979d5b2 = $(`<div id="html_ebd4497b4c9c48338ff70a756979d5b2" style="width: 100.0%; height: 100.0%;">Estadio Azteca, Club America</div>`)[0];
                popup_92f2462693ea499ea79a950003586b5d.setContent(html_ebd4497b4c9c48338ff70a756979d5b2);
            

            marker_c579a2b52d524646b1a3c51f6f46f2a8.bindPopup(popup_92f2462693ea499ea79a950003586b5d)
            ;

            
        
    
        var marker_b4d1af8363e64cd0b35dcfcb59ab65ab = L.marker(
            [45.109444, 7.641111],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_529e350347754d579fd869957ffdd9d8 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_b4d1af8363e64cd0b35dcfcb59ab65ab.setIcon(icon_529e350347754d579fd869957ffdd9d8);
            
    
            var popup_ec89f6dbcbfe41958f343d3b2d5e31b9 = L.popup({maxWidth: '100%'
            
            });

            
                var html_45200cf4cf2d461cbc3d9aedb1a71dc4 = $(`<div id="html_45200cf4cf2d461cbc3d9aedb1a71dc4" style="width: 100.0%; height: 100.0%;">Estadio Juventus, Juventus </div>`)[0];
                popup_ec89f6dbcbfe41958f343d3b2d5e31b9.setContent(html_45200cf4cf2d461cbc3d9aedb1a71dc4);
            

            marker_b4d1af8363e64cd0b35dcfcb59ab65ab.bindPopup(popup_ec89f6dbcbfe41958f343d3b2d5e31b9)
            ;

            
        
    
        var marker_fb6f0ea7952642149a7166446a1c9c77 = L.marker(
            [41.102869, 28.990419],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_4be201d05eb84dbf9471c44c0de7ff9d = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_fb6f0ea7952642149a7166446a1c9c77.setIcon(icon_4be201d05eb84dbf9471c44c0de7ff9d);
            
    
            var popup_38a49c709cbb4309b07ea939f6fd6f43 = L.popup({maxWidth: '100%'
            
            });

            
                var html_e1d8234c73be4c4caba4917565327ad3 = $(`<div id="html_e1d8234c73be4c4caba4917565327ad3" style="width: 100.0%; height: 100.0%;">Estadio Türk Telekom, Galatasaray</div>`)[0];
                popup_38a49c709cbb4309b07ea939f6fd6f43.setContent(html_e1d8234c73be4c4caba4917565327ad3);
            

            marker_fb6f0ea7952642149a7166446a1c9c77.bindPopup(popup_38a49c709cbb4309b07ea939f6fd6f43)
            ;

            
        
    
        var marker_ea59570812614908b41ac6e8d84c32e4 = L.marker(
            [48.841389, 2.253056],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_3c22efc246d04ef999ec0867b259f014 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_ea59570812614908b41ac6e8d84c32e4.setIcon(icon_3c22efc246d04ef999ec0867b259f014);
            
    
            var popup_5982d6026dbe40789eff519a43a3c1ba = L.popup({maxWidth: '100%'
            
            });

            
                var html_0025eb053fc24a45a9902810fafa7156 = $(`<div id="html_0025eb053fc24a45a9902810fafa7156" style="width: 100.0%; height: 100.0%;">Estadio Parc des Princes, Paris Saint-Germain </div>`)[0];
                popup_5982d6026dbe40789eff519a43a3c1ba.setContent(html_0025eb053fc24a45a9902810fafa7156);
            

            marker_ea59570812614908b41ac6e8d84c32e4.bindPopup(popup_5982d6026dbe40789eff519a43a3c1ba)
            ;

            
        
    
        var marker_63683318ec254bbc9c890196e743b955 = L.marker(
            [48.218775, 11.624753],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_214cb8bbbf7547989381ecd3ab665230);
        
    

                var icon_3740c7b1b6b64c8988c1facde40f6e6f = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_63683318ec254bbc9c890196e743b955.setIcon(icon_3740c7b1b6b64c8988c1facde40f6e6f);
            
    
            var popup_73871e77527b42ec9a65719c180f9753 = L.popup({maxWidth: '100%'
            
            });

            
                var html_06b4213e5b034f8a8a13224d06b12074 = $(`<div id="html_06b4213e5b034f8a8a13224d06b12074" style="width: 100.0%; height: 100.0%;">Allianz Arena, Paris Saint-Germain </div>`)[0];
                popup_73871e77527b42ec9a65719c180f9753.setContent(html_06b4213e5b034f8a8a13224d06b12074);
            

            marker_63683318ec254bbc9c890196e743b955.bindPopup(popup_73871e77527b42ec9a65719c180f9753)
            ;

            
        
</script>