---
title: "Mapping Geodata with Folium"
date: 2020-09-07
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
    <style>#map_82ba626ffb4147af86356c2c1cc719c7 {
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
             
    
    <div class="folium-map" id="map_82ba626ffb4147af86356c2c1cc719c7" ></div>
</body>
<script>    
    
    
        var bounds = null;
    

    var map_82ba626ffb4147af86356c2c1cc719c7 = L.map(
        'map_82ba626ffb4147af86356c2c1cc719c7', {
        center: [30.8082, -118.2474],
        zoom: 3,
        maxBounds: bounds,
        layers: [],
        worldCopyJump: false,
        crs: L.CRS.EPSG3857,
        zoomControl: true,
        });


    
    var tile_layer_0272f293d5144236b917b63e66ed5e26 = L.tileLayer(
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
}).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
    
        var marker_1e8f647d5ea744d192f54435caad5014 = L.marker(
            [-34.63565, -58.36465],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_516277c163234a8aa64227df42611b70 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'lightgreen',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_1e8f647d5ea744d192f54435caad5014.setIcon(icon_516277c163234a8aa64227df42611b70);
            
    
            var popup_d461bf4a992444b39eec06099389536e = L.popup({maxWidth: '100%'
            
            });

            
                var html_876322a1de3640a992fce2ff8d82665c = $(`<div id="html_876322a1de3640a992fce2ff8d82665c" style="width: 100.0%; height: 100.0%;">Estadio 'La Bombonera',  Boca Juniors</div>`)[0];
                popup_d461bf4a992444b39eec06099389536e.setContent(html_876322a1de3640a992fce2ff8d82665c);
            

            marker_1e8f647d5ea744d192f54435caad5014.bindPopup(popup_d461bf4a992444b39eec06099389536e)
            ;

            
        
    
        var marker_0c1f1e0a99774d0c81022c0871de2d58 = L.marker(
            [-34.545319, -58.449736],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_fc9c277fe8aa4675ac510dabef0690ee = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_0c1f1e0a99774d0c81022c0871de2d58.setIcon(icon_fc9c277fe8aa4675ac510dabef0690ee);
            
    
            var popup_4379faca2d2a46eeb135a9f17d0c7b2f = L.popup({maxWidth: '100%'
            
            });

            
                var html_bcc802e12184430b99e4f62c332a7bc4 = $(`<div id="html_bcc802e12184430b99e4f62c332a7bc4" style="width: 100.0%; height: 100.0%;">Estadio Monumental Americo Vespucio, River Plate</div>`)[0];
                popup_4379faca2d2a46eeb135a9f17d0c7b2f.setContent(html_bcc802e12184430b99e4f62c332a7bc4);
            

            marker_0c1f1e0a99774d0c81022c0871de2d58.bindPopup(popup_4379faca2d2a46eeb135a9f17d0c7b2f)
            ;

            
        
    
        var marker_3a0ea6a03d3d469f97559aaa8e8c1ca1 = L.marker(
            [-34.670267, -58.370969],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_cd0cc82330ce4745a1b1a044f11f8844 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_3a0ea6a03d3d469f97559aaa8e8c1ca1.setIcon(icon_cd0cc82330ce4745a1b1a044f11f8844);
            
    
            var popup_4fd177764d1d4bd0a68c5f5e6d99620a = L.popup({maxWidth: '100%'
            
            });

            
                var html_3aa2153551a046e5aa9ba51f581b202c = $(`<div id="html_3aa2153551a046e5aa9ba51f581b202c" style="width: 100.0%; height: 100.0%;">Estadio Libertadores De América, Club Atlético Independiente</div>`)[0];
                popup_4fd177764d1d4bd0a68c5f5e6d99620a.setContent(html_3aa2153551a046e5aa9ba51f581b202c);
            

            marker_3a0ea6a03d3d469f97559aaa8e8c1ca1.bindPopup(popup_4fd177764d1d4bd0a68c5f5e6d99620a)
            ;

            
        
    
        var marker_8de1c9a8464a4fdf8cfbd4aafc9ec201 = L.marker(
            [-25.292072, -57.657381],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_a00ee58613074952a52e0fb0ef332cb4 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_8de1c9a8464a4fdf8cfbd4aafc9ec201.setIcon(icon_a00ee58613074952a52e0fb0ef332cb4);
            
    
            var popup_a013bd07e5844c828860fd6089cf8a72 = L.popup({maxWidth: '100%'
            
            });

            
                var html_d371dd0136d045c684b0a2574564b65b = $(`<div id="html_d371dd0136d045c684b0a2574564b65b" style="width: 100.0%; height: 100.0%;">Estadio Defensores del Chaco</div>`)[0];
                popup_a013bd07e5844c828860fd6089cf8a72.setContent(html_d371dd0136d045c684b0a2574564b65b);
            

            marker_8de1c9a8464a4fdf8cfbd4aafc9ec201.bindPopup(popup_a013bd07e5844c828860fd6089cf8a72)
            ;

            
        
    
        var marker_f33fb9996ec746b491a30fa56228ba05 = L.marker(
            [-34.796917, -56.067167],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_f4fc9451ef0d45e8836e6bc23a667541 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_f33fb9996ec746b491a30fa56228ba05.setIcon(icon_f4fc9451ef0d45e8836e6bc23a667541);
            
    
            var popup_25bc9e03a8b842f09926ed2dae813d57 = L.popup({maxWidth: '100%'
            
            });

            
                var html_79631b400a3442babf69458602aa1ca1 = $(`<div id="html_79631b400a3442babf69458602aa1ca1" style="width: 100.0%; height: 100.0%;">Estadio Campeón del Siglo, Peñarol</div>`)[0];
                popup_25bc9e03a8b842f09926ed2dae813d57.setContent(html_79631b400a3442babf69458602aa1ca1);
            

            marker_f33fb9996ec746b491a30fa56228ba05.bindPopup(popup_25bc9e03a8b842f09926ed2dae813d57)
            ;

            
        
    
        var marker_1233b46aac7f492c8be991249ae1370c = L.marker(
            [-34.884373, -56.1588],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_a84dfe4b37874736ab56bffd852ef8a9 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_1233b46aac7f492c8be991249ae1370c.setIcon(icon_a84dfe4b37874736ab56bffd852ef8a9);
            
    
            var popup_89b8dc8c6bcf4cd7945f9cf6feadf587 = L.popup({maxWidth: '100%'
            
            });

            
                var html_881702b22ff443df8abdf2baa6eb8265 = $(`<div id="html_881702b22ff443df8abdf2baa6eb8265" style="width: 100.0%; height: 100.0%;">Estadio Gran Parque Central, Nacional</div>`)[0];
                popup_89b8dc8c6bcf4cd7945f9cf6feadf587.setContent(html_881702b22ff443df8abdf2baa6eb8265);
            

            marker_1233b46aac7f492c8be991249ae1370c.bindPopup(popup_89b8dc8c6bcf4cd7945f9cf6feadf587)
            ;

            
        
    
        var marker_68a657ba92e246aa8aef770cbc6b89d2 = L.marker(
            [-33.506611, -70.605944],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_74853be1a1b84d7cb6806cd0a929d306 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_68a657ba92e246aa8aef770cbc6b89d2.setIcon(icon_74853be1a1b84d7cb6806cd0a929d306);
            
    
            var popup_46d74c3786054f3abafc824a380c6323 = L.popup({maxWidth: '100%'
            
            });

            
                var html_b11473b699d74a839cb84d1213cb33d2 = $(`<div id="html_b11473b699d74a839cb84d1213cb33d2" style="width: 100.0%; height: 100.0%;">Estadio Monumental David Arellano, Colo-Colo</div>`)[0];
                popup_46d74c3786054f3abafc824a380c6323.setContent(html_b11473b699d74a839cb84d1213cb33d2);
            

            marker_68a657ba92e246aa8aef770cbc6b89d2.bindPopup(popup_46d74c3786054f3abafc824a380c6323)
            ;

            
        
    
        var marker_448aaf55ab1d42aca81d7ab43623ae5f = L.marker(
            [-12.055694, -76.935972],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_264fe051ad7e4d1290dee553989cd8be = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_448aaf55ab1d42aca81d7ab43623ae5f.setIcon(icon_264fe051ad7e4d1290dee553989cd8be);
            
    
            var popup_33bfe883bdf9408da903159cb00bff9a = L.popup({maxWidth: '100%'
            
            });

            
                var html_6dabef25237a43e2bd18fffa93665357 = $(`<div id="html_6dabef25237a43e2bd18fffa93665357" style="width: 100.0%; height: 100.0%;">Estadio Monumental "U", Club Universitario de Deportes</div>`)[0];
                popup_33bfe883bdf9408da903159cb00bff9a.setContent(html_6dabef25237a43e2bd18fffa93665357);
            

            marker_448aaf55ab1d42aca81d7ab43623ae5f.bindPopup(popup_33bfe883bdf9408da903159cb00bff9a)
            ;

            
        
    
        var marker_c5dd64b9ce11439f8181d52b74735fff = L.marker(
            [0.107717, -78.489103],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_55e58766c6444333999c512d3fcb2ee0 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_c5dd64b9ce11439f8181d52b74735fff.setIcon(icon_55e58766c6444333999c512d3fcb2ee0);
            
    
            var popup_8ed41ba42faa4ba79fc9b303c75cafba = L.popup({maxWidth: '100%'
            
            });

            
                var html_4421010cc2dc4d39bbda6507b77b2764 = $(`<div id="html_4421010cc2dc4d39bbda6507b77b2764" style="width: 100.0%; height: 100.0%;">Estadio Rodrigo Paz Delgado, Liga Deportiva Universitaria</div>`)[0];
                popup_8ed41ba42faa4ba79fc9b303c75cafba.setContent(html_4421010cc2dc4d39bbda6507b77b2764);
            

            marker_c5dd64b9ce11439f8181d52b74735fff.bindPopup(popup_8ed41ba42faa4ba79fc9b303c75cafba)
            ;

            
        
    
        var marker_7a186b148bec4072b1000ffc580746f8 = L.marker(
            [-0.177528, -78.476583],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_11acc5e465e64f688e6eda75960630d9 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_7a186b148bec4072b1000ffc580746f8.setIcon(icon_11acc5e465e64f688e6eda75960630d9);
            
    
            var popup_6a9618a2e9a64d17bb843a7329cf96e5 = L.popup({maxWidth: '100%'
            
            });

            
                var html_c63a7bd0cb574959a6d4b3c102a84351 = $(`<div id="html_c63a7bd0cb574959a6d4b3c102a84351" style="width: 100.0%; height: 100.0%;">Estadio Olímpico Atahualpa</div>`)[0];
                popup_6a9618a2e9a64d17bb843a7329cf96e5.setContent(html_c63a7bd0cb574959a6d4b3c102a84351);
            

            marker_7a186b148bec4072b1000ffc580746f8.bindPopup(popup_6a9618a2e9a64d17bb843a7329cf96e5)
            ;

            
        
    
        var marker_4e49b7485b1e4ff7928080fd20497fbe = L.marker(
            [-2.185869, -79.924931],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_cecb8a03b35045a6a5bb307a09758931 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_4e49b7485b1e4ff7928080fd20497fbe.setIcon(icon_cecb8a03b35045a6a5bb307a09758931);
            
    
            var popup_7035be1084474117927e2a858f0a8cce = L.popup({maxWidth: '100%'
            
            });

            
                var html_10e459209f7a46728812aeb2c1351f52 = $(`<div id="html_10e459209f7a46728812aeb2c1351f52" style="width: 100.0%; height: 100.0%;">Estadio Isidro Romero Carbo, Barcelona Sporting Club</div>`)[0];
                popup_7035be1084474117927e2a858f0a8cce.setContent(html_10e459209f7a46728812aeb2c1351f52);
            

            marker_4e49b7485b1e4ff7928080fd20497fbe.bindPopup(popup_7035be1084474117927e2a858f0a8cce)
            ;

            
        
    
        var marker_62643733728c43e1907dbf6e11781243 = L.marker(
            [40.736667, -74.15027],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_7698037b984a4af7b4429adc9854b324 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_62643733728c43e1907dbf6e11781243.setIcon(icon_7698037b984a4af7b4429adc9854b324);
            
    
            var popup_bd952c90ca82420aac5ea75a110e3be5 = L.popup({maxWidth: '100%'
            
            });

            
                var html_c3bfd42ae56e47579149b274f996f951 = $(`<div id="html_c3bfd42ae56e47579149b274f996f951" style="width: 100.0%; height: 100.0%;">Red Bull Arena, New York Red Bulls</div>`)[0];
                popup_bd952c90ca82420aac5ea75a110e3be5.setContent(html_c3bfd42ae56e47579149b274f996f951);
            

            marker_62643733728c43e1907dbf6e11781243.bindPopup(popup_bd952c90ca82420aac5ea75a110e3be5)
            ;

            
        
    
        var marker_06ab5e9ff2e4413598c87c6d515613fe = L.marker(
            [33.755556, -84.4],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_21cdc34255c646d8bbaf7944bb081cf4 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_06ab5e9ff2e4413598c87c6d515613fe.setIcon(icon_21cdc34255c646d8bbaf7944bb081cf4);
            
    
            var popup_37f469ba506f439a9428ac1dd9aae1f4 = L.popup({maxWidth: '100%'
            
            });

            
                var html_891920b8d4c3411a9f496a911b66f2af = $(`<div id="html_891920b8d4c3411a9f496a911b66f2af" style="width: 100.0%; height: 100.0%;">Estadio Mercedes Benz, Atlanta United</div>`)[0];
                popup_37f469ba506f439a9428ac1dd9aae1f4.setContent(html_891920b8d4c3411a9f496a911b66f2af);
            

            marker_06ab5e9ff2e4413598c87c6d515613fe.bindPopup(popup_37f469ba506f439a9428ac1dd9aae1f4)
            ;

            
        
    
        var marker_f7c935950074403dac5ad6f0ee8d44a9 = L.marker(
            [33.864, -118.261],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_612546fefe904a4eb3b3038ac08e2145 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_f7c935950074403dac5ad6f0ee8d44a9.setIcon(icon_612546fefe904a4eb3b3038ac08e2145);
            
    
            var popup_b2601597940b439fbcd491eb68d534ff = L.popup({maxWidth: '100%'
            
            });

            
                var html_3082b7d132254d2fbcd1fd65b7d73def = $(`<div id="html_3082b7d132254d2fbcd1fd65b7d73def" style="width: 100.0%; height: 100.0%;">Dignity Health Sports Park, LA Galaxy</div>`)[0];
                popup_b2601597940b439fbcd491eb68d534ff.setContent(html_3082b7d132254d2fbcd1fd65b7d73def);
            

            marker_f7c935950074403dac5ad6f0ee8d44a9.bindPopup(popup_b2601597940b439fbcd491eb68d534ff)
            ;

            
        
    
        var marker_87d0ed624b1448a9b35cde79b6f3093e = L.marker(
            [40.45301, -3.68829],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_4055c909ce184d949397067a43c0e75d = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_87d0ed624b1448a9b35cde79b6f3093e.setIcon(icon_4055c909ce184d949397067a43c0e75d);
            
    
            var popup_220f9ab843e84099b35e25858e40baef = L.popup({maxWidth: '100%'
            
            });

            
                var html_57f4d60aa7624588a0e473e084520b99 = $(`<div id="html_57f4d60aa7624588a0e473e084520b99" style="width: 100.0%; height: 100.0%;">Estadio Santiago Bernabeu, Real Madrid</div>`)[0];
                popup_220f9ab843e84099b35e25858e40baef.setContent(html_57f4d60aa7624588a0e473e084520b99);
            

            marker_87d0ed624b1448a9b35cde79b6f3093e.bindPopup(popup_220f9ab843e84099b35e25858e40baef)
            ;

            
        
    
        var marker_4b4799d8af0a41289265064034a00b06 = L.marker(
            [41.3808, 2.12311],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_c4ef47336ad6454e8bd593d219e9e31a = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_4b4799d8af0a41289265064034a00b06.setIcon(icon_c4ef47336ad6454e8bd593d219e9e31a);
            
    
            var popup_730cc5feac2d47b9a60778df3a753c2c = L.popup({maxWidth: '100%'
            
            });

            
                var html_8da126f35a114970bc98288f2c230e8c = $(`<div id="html_8da126f35a114970bc98288f2c230e8c" style="width: 100.0%; height: 100.0%;">Estadio Camp Nou, FC Barcelona</div>`)[0];
                popup_730cc5feac2d47b9a60778df3a753c2c.setContent(html_8da126f35a114970bc98288f2c230e8c);
            

            marker_4b4799d8af0a41289265064034a00b06.bindPopup(popup_730cc5feac2d47b9a60778df3a753c2c)
            ;

            
        
    
        var marker_6ddbc5b2382d48069c274ccc40e7589b = L.marker(
            [38.752648359600805, -9.184699058532715],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_6ab2c1d721184cec9efb0a850a0b6506 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_6ddbc5b2382d48069c274ccc40e7589b.setIcon(icon_6ab2c1d721184cec9efb0a850a0b6506);
            
    
            var popup_b84fa9b7f26a48cead269d8e18b03f42 = L.popup({maxWidth: '100%'
            
            });

            
                var html_2b35d7f9120d4367b1571a9b0a6563f8 = $(`<div id="html_2b35d7f9120d4367b1571a9b0a6563f8" style="width: 100.0%; height: 100.0%;">Estadio do Sport Lisboa e Benfica</div>`)[0];
                popup_b84fa9b7f26a48cead269d8e18b03f42.setContent(html_2b35d7f9120d4367b1571a9b0a6563f8);
            

            marker_6ddbc5b2382d48069c274ccc40e7589b.bindPopup(popup_b84fa9b7f26a48cead269d8e18b03f42)
            ;

            
        
    
        var marker_7e3e85e70da649c6be544ac39add8179 = L.marker(
            [-22.912167, -43.230164],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_1ca3adb20b584518b912b6d4b243f4e7 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_7e3e85e70da649c6be544ac39add8179.setIcon(icon_1ca3adb20b584518b912b6d4b243f4e7);
            
    
            var popup_9c73167fd31047bdba6f1e4d44804450 = L.popup({maxWidth: '100%'
            
            });

            
                var html_ac9f6044635c498a8fe492e5bbf2f3d2 = $(`<div id="html_ac9f6044635c498a8fe492e5bbf2f3d2" style="width: 100.0%; height: 100.0%;">Estadio Maracana</div>`)[0];
                popup_9c73167fd31047bdba6f1e4d44804450.setContent(html_ac9f6044635c498a8fe492e5bbf2f3d2);
            

            marker_7e3e85e70da649c6be544ac39add8179.bindPopup(popup_9c73167fd31047bdba6f1e4d44804450)
            ;

            
        
    
        var marker_b7410c9af6b74452af3153ae025538b3 = L.marker(
            [19.303056, -99.150556],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_b624596d09614849b9784e50eb5e2c1d = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_b7410c9af6b74452af3153ae025538b3.setIcon(icon_b624596d09614849b9784e50eb5e2c1d);
            
    
            var popup_06fc53116a364feabe29d8080c7c36c4 = L.popup({maxWidth: '100%'
            
            });

            
                var html_4c470256a51845a29fa39ffaaec7d587 = $(`<div id="html_4c470256a51845a29fa39ffaaec7d587" style="width: 100.0%; height: 100.0%;">Estadio Azteca, Club America</div>`)[0];
                popup_06fc53116a364feabe29d8080c7c36c4.setContent(html_4c470256a51845a29fa39ffaaec7d587);
            

            marker_b7410c9af6b74452af3153ae025538b3.bindPopup(popup_06fc53116a364feabe29d8080c7c36c4)
            ;

            
        
    
        var marker_04c1741d336f43b3a792ab67c8a186b3 = L.marker(
            [45.109444, 7.641111],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_1e8c672b6647494d88884918b302574c = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_04c1741d336f43b3a792ab67c8a186b3.setIcon(icon_1e8c672b6647494d88884918b302574c);
            
    
            var popup_0f12298f642244a6bf763eec48936050 = L.popup({maxWidth: '100%'
            
            });

            
                var html_6a0d28fb3b90414ea3aedb7659c14766 = $(`<div id="html_6a0d28fb3b90414ea3aedb7659c14766" style="width: 100.0%; height: 100.0%;">Estadio Juventus, Juventus </div>`)[0];
                popup_0f12298f642244a6bf763eec48936050.setContent(html_6a0d28fb3b90414ea3aedb7659c14766);
            

            marker_04c1741d336f43b3a792ab67c8a186b3.bindPopup(popup_0f12298f642244a6bf763eec48936050)
            ;

            
        
    
        var marker_f61c4bf84afe4b498131bc56929d4512 = L.marker(
            [41.102869, 28.990419],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_5cb5306bd14644e7b619834585e455fa = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_f61c4bf84afe4b498131bc56929d4512.setIcon(icon_5cb5306bd14644e7b619834585e455fa);
            
    
            var popup_b1ab9a98bc8a4c31a9784473d9c381cf = L.popup({maxWidth: '100%'
            
            });

            
                var html_6127a3ceb72846c3a662fa729e84a364 = $(`<div id="html_6127a3ceb72846c3a662fa729e84a364" style="width: 100.0%; height: 100.0%;">Estadio Türk Telekom, Galatasaray</div>`)[0];
                popup_b1ab9a98bc8a4c31a9784473d9c381cf.setContent(html_6127a3ceb72846c3a662fa729e84a364);
            

            marker_f61c4bf84afe4b498131bc56929d4512.bindPopup(popup_b1ab9a98bc8a4c31a9784473d9c381cf)
            ;

            
        
    
        var marker_507a4e9e0d214afe83b45a2a79432e97 = L.marker(
            [48.841389, 2.253056],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_53ce4a45bfb94b939dd3d2db1f8f1d95 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_507a4e9e0d214afe83b45a2a79432e97.setIcon(icon_53ce4a45bfb94b939dd3d2db1f8f1d95);
            
    
            var popup_d24ef45157664672b766453d75f238c2 = L.popup({maxWidth: '100%'
            
            });

            
                var html_b126b6492dcd45a89b31cfed853540ad = $(`<div id="html_b126b6492dcd45a89b31cfed853540ad" style="width: 100.0%; height: 100.0%;">Estadio Parc des Princes, Paris Saint-Germain </div>`)[0];
                popup_d24ef45157664672b766453d75f238c2.setContent(html_b126b6492dcd45a89b31cfed853540ad);
            

            marker_507a4e9e0d214afe83b45a2a79432e97.bindPopup(popup_d24ef45157664672b766453d75f238c2)
            ;

            
        
    
        var marker_618267d8a4ba473392770b2165eb5bb4 = L.marker(
            [48.218775, 11.624753],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_82ba626ffb4147af86356c2c1cc719c7);
        
    

                var icon_9cc5eb0fdbe8464591ccbf200d26c14a = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_618267d8a4ba473392770b2165eb5bb4.setIcon(icon_9cc5eb0fdbe8464591ccbf200d26c14a);
            
    
            var popup_324d249edf894f9499e11d1bb1d5cb8b = L.popup({maxWidth: '100%'
            
            });

            
                var html_a016cb30df9f487c92b37a7190838b21 = $(`<div id="html_a016cb30df9f487c92b37a7190838b21" style="width: 100.0%; height: 100.0%;">Allianz Arena, Paris Saint-Germain </div>`)[0];
                popup_324d249edf894f9499e11d1bb1d5cb8b.setContent(html_a016cb30df9f487c92b37a7190838b21);
            

            marker_618267d8a4ba473392770b2165eb5bb4.bindPopup(popup_324d249edf894f9499e11d1bb1d5cb8b)
            ;

            
        
</script>



