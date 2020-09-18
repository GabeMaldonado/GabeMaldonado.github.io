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


<html lang="en">
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
    <style>#map_c3cc23d32dde455796293eee4b1aedb6 {
        position: relative;
        width: 100.0%;
        height: 100.0%;
        left: 0.0%;
        top: 0.0%;
        }
    </style>
</head>
<body>    
    
    <div class="folium-map" id="map_c3cc23d32dde455796293eee4b1aedb6" ></div>
</body>
<script>    
    
    
        var bounds = null;
    

    var map_c3cc23d32dde455796293eee4b1aedb6 = L.map(
        'map_c3cc23d32dde455796293eee4b1aedb6', {
        center: [30.8082, -118.2474],
        zoom: 3,
        maxBounds: bounds,
        layers: [],
        worldCopyJump: false,
        crs: L.CRS.EPSG3857,
        zoomControl: true,
        });


    
    var tile_layer_c8e53877c6fe4d31987ec309361b21a8 = L.tileLayer(
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
}).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
    
        var marker_5c8a331770b14a9b94895240a17f25c6 = L.marker(
            [-34.63565, -58.36465],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_00a6539ded354fdfaa0bc730b1832506 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'lightgreen',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_5c8a331770b14a9b94895240a17f25c6.setIcon(icon_00a6539ded354fdfaa0bc730b1832506);
            
    
            var popup_e1dc022d690641858ef1356ff0280919 = L.popup({maxWidth: '100%'
            
            });

            
                var html_8e6b2ad883494e87ad361855424f7cd9 = $(`<div id="html_8e6b2ad883494e87ad361855424f7cd9" style="width: 100.0%; height: 100.0%;">Estadio 'La Bombonera',  Boca Juniors</div>`)[0];
                popup_e1dc022d690641858ef1356ff0280919.setContent(html_8e6b2ad883494e87ad361855424f7cd9);
            

            marker_5c8a331770b14a9b94895240a17f25c6.bindPopup(popup_e1dc022d690641858ef1356ff0280919)
            ;

            
        
    
        var marker_b8a6d04d58b54537a2336cf1b5d72267 = L.marker(
            [-34.545319, -58.449736],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_6b55835c1ce047fea493510a091de24d = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_b8a6d04d58b54537a2336cf1b5d72267.setIcon(icon_6b55835c1ce047fea493510a091de24d);
            
    
            var popup_4250e08d25f94289b71e2ea452c098ce = L.popup({maxWidth: '100%'
            
            });

            
                var html_8934ff7cc2ff4f06a49564e400208fc5 = $(`<div id="html_8934ff7cc2ff4f06a49564e400208fc5" style="width: 100.0%; height: 100.0%;">Estadio Monumental Americo Vespucio, River Plate</div>`)[0];
                popup_4250e08d25f94289b71e2ea452c098ce.setContent(html_8934ff7cc2ff4f06a49564e400208fc5);
            

            marker_b8a6d04d58b54537a2336cf1b5d72267.bindPopup(popup_4250e08d25f94289b71e2ea452c098ce)
            ;

            
        
    
        var marker_c953d4d15ae84e029c36db0f00504db6 = L.marker(
            [-34.670267, -58.370969],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_7a55f1accbc04fdba640c5dce1538627 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_c953d4d15ae84e029c36db0f00504db6.setIcon(icon_7a55f1accbc04fdba640c5dce1538627);
            
    
            var popup_6af3e11c464742709c9f7baf25256636 = L.popup({maxWidth: '100%'
            
            });

            
                var html_93ea3189d49848109b2c45c0e1691426 = $(`<div id="html_93ea3189d49848109b2c45c0e1691426" style="width: 100.0%; height: 100.0%;">Estadio Libertadores De América, Club Atlético Independiente</div>`)[0];
                popup_6af3e11c464742709c9f7baf25256636.setContent(html_93ea3189d49848109b2c45c0e1691426);
            

            marker_c953d4d15ae84e029c36db0f00504db6.bindPopup(popup_6af3e11c464742709c9f7baf25256636)
            ;

            
        
    
        var marker_5f71d39550be4882af02619a2e2e4ad6 = L.marker(
            [-25.292072, -57.657381],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_7e6d3dd152fa43d9a2f68c7268b7bafd = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_5f71d39550be4882af02619a2e2e4ad6.setIcon(icon_7e6d3dd152fa43d9a2f68c7268b7bafd);
            
    
            var popup_3aa42be19bda49f6ade8559db0af7cc8 = L.popup({maxWidth: '100%'
            
            });

            
                var html_de0f47cb9b104855ab5f1c776840adba = $(`<div id="html_de0f47cb9b104855ab5f1c776840adba" style="width: 100.0%; height: 100.0%;">Estadio Defensores del Chaco</div>`)[0];
                popup_3aa42be19bda49f6ade8559db0af7cc8.setContent(html_de0f47cb9b104855ab5f1c776840adba);
            

            marker_5f71d39550be4882af02619a2e2e4ad6.bindPopup(popup_3aa42be19bda49f6ade8559db0af7cc8)
            ;

            
        
    
        var marker_a694ec8d99b64fceb4daee30e5b6addc = L.marker(
            [-34.796917, -56.067167],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_f03100cf265947dab80ea21b5c1e0464 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_a694ec8d99b64fceb4daee30e5b6addc.setIcon(icon_f03100cf265947dab80ea21b5c1e0464);
            
    
            var popup_9a57aabc16734cabaaee5813943f77a6 = L.popup({maxWidth: '100%'
            
            });

            
                var html_f423396094114813aee341345a9305b4 = $(`<div id="html_f423396094114813aee341345a9305b4" style="width: 100.0%; height: 100.0%;">Estadio Campeón del Siglo, Peñarol</div>`)[0];
                popup_9a57aabc16734cabaaee5813943f77a6.setContent(html_f423396094114813aee341345a9305b4);
            

            marker_a694ec8d99b64fceb4daee30e5b6addc.bindPopup(popup_9a57aabc16734cabaaee5813943f77a6)
            ;

            
        
    
        var marker_53cd1fca54bb4e1a831112c184f07f5c = L.marker(
            [-34.884373, -56.1588],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_403f338db7154cf3abf129baffae1312 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_53cd1fca54bb4e1a831112c184f07f5c.setIcon(icon_403f338db7154cf3abf129baffae1312);
            
    
            var popup_e47607b44ba44669a8d6114838b88e2f = L.popup({maxWidth: '100%'
            
            });

            
                var html_7f85a07617ad4e599455cd774755d3f2 = $(`<div id="html_7f85a07617ad4e599455cd774755d3f2" style="width: 100.0%; height: 100.0%;">Estadio Gran Parque Central, Nacional</div>`)[0];
                popup_e47607b44ba44669a8d6114838b88e2f.setContent(html_7f85a07617ad4e599455cd774755d3f2);
            

            marker_53cd1fca54bb4e1a831112c184f07f5c.bindPopup(popup_e47607b44ba44669a8d6114838b88e2f)
            ;

            
        
    
        var marker_4e06e7731adb4705a39ffafdc6f2ec9e = L.marker(
            [-33.506611, -70.605944],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_02e10179cda54740a7b13b31fc74a1bd = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_4e06e7731adb4705a39ffafdc6f2ec9e.setIcon(icon_02e10179cda54740a7b13b31fc74a1bd);
            
    
            var popup_5ec12e7326ab4f9b81e70b5aedff9469 = L.popup({maxWidth: '100%'
            
            });

            
                var html_2051757b6eb84065941e0b8dd367c419 = $(`<div id="html_2051757b6eb84065941e0b8dd367c419" style="width: 100.0%; height: 100.0%;">Estadio Monumental David Arellano, Colo-Colo</div>`)[0];
                popup_5ec12e7326ab4f9b81e70b5aedff9469.setContent(html_2051757b6eb84065941e0b8dd367c419);
            

            marker_4e06e7731adb4705a39ffafdc6f2ec9e.bindPopup(popup_5ec12e7326ab4f9b81e70b5aedff9469)
            ;

            
        
    
        var marker_51b10aef72984323b81ed256bcf07775 = L.marker(
            [-12.055694, -76.935972],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_8946360998ea4e2bbde8671237e388d5 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_51b10aef72984323b81ed256bcf07775.setIcon(icon_8946360998ea4e2bbde8671237e388d5);
            
    
            var popup_14a9f22acba84422b6c8bc5ac47f9394 = L.popup({maxWidth: '100%'
            
            });

            
                var html_9219471f33a44084a355802bd6b430a6 = $(`<div id="html_9219471f33a44084a355802bd6b430a6" style="width: 100.0%; height: 100.0%;">Estadio Monumental "U", Club Universitario de Deportes</div>`)[0];
                popup_14a9f22acba84422b6c8bc5ac47f9394.setContent(html_9219471f33a44084a355802bd6b430a6);
            

            marker_51b10aef72984323b81ed256bcf07775.bindPopup(popup_14a9f22acba84422b6c8bc5ac47f9394)
            ;

            
        
    
        var marker_aff54b480d25403fac31a808bffb3a89 = L.marker(
            [0.107717, -78.489103],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_b996aa66bfe44a9a9764cbed27417ad0 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_aff54b480d25403fac31a808bffb3a89.setIcon(icon_b996aa66bfe44a9a9764cbed27417ad0);
            
    
            var popup_4927211ae9b74eacb498a927fbefb2ed = L.popup({maxWidth: '100%'
            
            });

            
                var html_0d32b5d7273545a4a3be06688760bb70 = $(`<div id="html_0d32b5d7273545a4a3be06688760bb70" style="width: 100.0%; height: 100.0%;">Estadio Rodrigo Paz Delgado, Liga Deportiva Universitaria</div>`)[0];
                popup_4927211ae9b74eacb498a927fbefb2ed.setContent(html_0d32b5d7273545a4a3be06688760bb70);
            

            marker_aff54b480d25403fac31a808bffb3a89.bindPopup(popup_4927211ae9b74eacb498a927fbefb2ed)
            ;

            
        
    
        var marker_4b54991204244970bd429445a2dfb0cc = L.marker(
            [-0.177528, -78.476583],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_ed4c6112dfb749289e6d6a20426a0dde = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_4b54991204244970bd429445a2dfb0cc.setIcon(icon_ed4c6112dfb749289e6d6a20426a0dde);
            
    
            var popup_85e45d882420400cba85e26c7e296f3a = L.popup({maxWidth: '100%'
            
            });

            
                var html_ac845166f86d45a78ca6f7a6a046b198 = $(`<div id="html_ac845166f86d45a78ca6f7a6a046b198" style="width: 100.0%; height: 100.0%;">Estadio Olímpico Atahualpa</div>`)[0];
                popup_85e45d882420400cba85e26c7e296f3a.setContent(html_ac845166f86d45a78ca6f7a6a046b198);
            

            marker_4b54991204244970bd429445a2dfb0cc.bindPopup(popup_85e45d882420400cba85e26c7e296f3a)
            ;

            
        
    
        var marker_db499b8d77684a6b8d209bdb6cc4c38c = L.marker(
            [-2.185869, -79.924931],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_61c890e9b24a420aae20134f176b29b9 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_db499b8d77684a6b8d209bdb6cc4c38c.setIcon(icon_61c890e9b24a420aae20134f176b29b9);
            
    
            var popup_e3b168cc8ff2442d98b36aae99a4426c = L.popup({maxWidth: '100%'
            
            });

            
                var html_764877d8aaf94ff58612b481d9134101 = $(`<div id="html_764877d8aaf94ff58612b481d9134101" style="width: 100.0%; height: 100.0%;">Estadio Isidro Romero Carbo, Barcelona Sporting Club</div>`)[0];
                popup_e3b168cc8ff2442d98b36aae99a4426c.setContent(html_764877d8aaf94ff58612b481d9134101);
            

            marker_db499b8d77684a6b8d209bdb6cc4c38c.bindPopup(popup_e3b168cc8ff2442d98b36aae99a4426c)
            ;

            
        
    
        var marker_6cf649e22db1463faff45bcc326b3e85 = L.marker(
            [40.736667, -74.15027],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_7462ce66e6ce4958943f47ccf36244a1 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_6cf649e22db1463faff45bcc326b3e85.setIcon(icon_7462ce66e6ce4958943f47ccf36244a1);
            
    
            var popup_7e64c21ed3464a3994eae1dace51f168 = L.popup({maxWidth: '100%'
            
            });

            
                var html_0134ad24aec44c85adb264a18aa6a621 = $(`<div id="html_0134ad24aec44c85adb264a18aa6a621" style="width: 100.0%; height: 100.0%;">Red Bull Arena, New York Red Bulls</div>`)[0];
                popup_7e64c21ed3464a3994eae1dace51f168.setContent(html_0134ad24aec44c85adb264a18aa6a621);
            

            marker_6cf649e22db1463faff45bcc326b3e85.bindPopup(popup_7e64c21ed3464a3994eae1dace51f168)
            ;

            
        
    
        var marker_1c286469c6584b17ae99d3f605ec1c78 = L.marker(
            [33.755556, -84.4],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_40fe4ce3e49c422889a0acfcf375c0ee = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_1c286469c6584b17ae99d3f605ec1c78.setIcon(icon_40fe4ce3e49c422889a0acfcf375c0ee);
            
    
            var popup_4ea510c338f943b1a8401330302e0524 = L.popup({maxWidth: '100%'
            
            });

            
                var html_df2314fd78384b4aa7ffa058fdfdb8c9 = $(`<div id="html_df2314fd78384b4aa7ffa058fdfdb8c9" style="width: 100.0%; height: 100.0%;">Estadio Mercedes Benz, Atlanta United</div>`)[0];
                popup_4ea510c338f943b1a8401330302e0524.setContent(html_df2314fd78384b4aa7ffa058fdfdb8c9);
            

            marker_1c286469c6584b17ae99d3f605ec1c78.bindPopup(popup_4ea510c338f943b1a8401330302e0524)
            ;

            
        
    
        var marker_43b471cb851642b7b08739c6c47aedb6 = L.marker(
            [33.864, -118.261],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_4bfedc608a5445948a6904f204c4d4a3 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_43b471cb851642b7b08739c6c47aedb6.setIcon(icon_4bfedc608a5445948a6904f204c4d4a3);
            
    
            var popup_fda97633fb4b42059c1e61f10a81daa2 = L.popup({maxWidth: '100%'
            
            });

            
                var html_0981cb0b36584863b2c6e172591a3e9a = $(`<div id="html_0981cb0b36584863b2c6e172591a3e9a" style="width: 100.0%; height: 100.0%;">Dignity Health Sports Park, LA Galaxy</div>`)[0];
                popup_fda97633fb4b42059c1e61f10a81daa2.setContent(html_0981cb0b36584863b2c6e172591a3e9a);
            

            marker_43b471cb851642b7b08739c6c47aedb6.bindPopup(popup_fda97633fb4b42059c1e61f10a81daa2)
            ;

            
        
    
        var marker_77f77065426a40bf9e0260543f76c384 = L.marker(
            [40.45301, -3.68829],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_c3da30b1d9af455b872c32da6ef3ec80 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_77f77065426a40bf9e0260543f76c384.setIcon(icon_c3da30b1d9af455b872c32da6ef3ec80);
            
    
            var popup_1d8e283a21374a19a15c5ac378049cd8 = L.popup({maxWidth: '100%'
            
            });

            
                var html_945f16dfda2a4be288aca9885c9466eb = $(`<div id="html_945f16dfda2a4be288aca9885c9466eb" style="width: 100.0%; height: 100.0%;">Estadio Santiago Bernabeu, Real Madrid</div>`)[0];
                popup_1d8e283a21374a19a15c5ac378049cd8.setContent(html_945f16dfda2a4be288aca9885c9466eb);
            

            marker_77f77065426a40bf9e0260543f76c384.bindPopup(popup_1d8e283a21374a19a15c5ac378049cd8)
            ;

            
        
    
        var marker_33c86e80c8584daba94b6b1d81eff703 = L.marker(
            [41.3808, 2.12311],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_c909df55f5234f448d92e1f72e832be7 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_33c86e80c8584daba94b6b1d81eff703.setIcon(icon_c909df55f5234f448d92e1f72e832be7);
            
    
            var popup_c7b51f6f00a740eeac300328d2538f65 = L.popup({maxWidth: '100%'
            
            });

            
                var html_a724c9bc2fa840ad9756c76c111a4e52 = $(`<div id="html_a724c9bc2fa840ad9756c76c111a4e52" style="width: 100.0%; height: 100.0%;">Estadio Camp Nou, FC Barcelona</div>`)[0];
                popup_c7b51f6f00a740eeac300328d2538f65.setContent(html_a724c9bc2fa840ad9756c76c111a4e52);
            

            marker_33c86e80c8584daba94b6b1d81eff703.bindPopup(popup_c7b51f6f00a740eeac300328d2538f65)
            ;

            
        
    
        var marker_39ec19868efe4c96855f504604bda945 = L.marker(
            [38.752648359600805, -9.184699058532715],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_46e07ac3a4214b998e6df67295d55e7d = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_39ec19868efe4c96855f504604bda945.setIcon(icon_46e07ac3a4214b998e6df67295d55e7d);
            
    
            var popup_e9285250a3d24363a77a203cd6f0d519 = L.popup({maxWidth: '100%'
            
            });

            
                var html_6cad0ba3cd1441558778af7bec77b0f2 = $(`<div id="html_6cad0ba3cd1441558778af7bec77b0f2" style="width: 100.0%; height: 100.0%;">Estadio do Sport Lisboa e Benfica</div>`)[0];
                popup_e9285250a3d24363a77a203cd6f0d519.setContent(html_6cad0ba3cd1441558778af7bec77b0f2);
            

            marker_39ec19868efe4c96855f504604bda945.bindPopup(popup_e9285250a3d24363a77a203cd6f0d519)
            ;

            
        
    
        var marker_f94254d24cf541a9897bbec3b82462c9 = L.marker(
            [-22.912167, -43.230164],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_8229daa494ff4fbc9abc6c7a64361095 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_f94254d24cf541a9897bbec3b82462c9.setIcon(icon_8229daa494ff4fbc9abc6c7a64361095);
            
    
            var popup_35993343fd3546c1be9a7bd8949bf92a = L.popup({maxWidth: '100%'
            
            });

            
                var html_45daf8fa48a04adfb14ed10ebb00cebd = $(`<div id="html_45daf8fa48a04adfb14ed10ebb00cebd" style="width: 100.0%; height: 100.0%;">Estadio Maracana</div>`)[0];
                popup_35993343fd3546c1be9a7bd8949bf92a.setContent(html_45daf8fa48a04adfb14ed10ebb00cebd);
            

            marker_f94254d24cf541a9897bbec3b82462c9.bindPopup(popup_35993343fd3546c1be9a7bd8949bf92a)
            ;

            
        
    
        var marker_1c0b358c497e4ebfbfd8d32bcd5a7785 = L.marker(
            [19.303056, -99.150556],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_ed0c573d4b2346b89ba646ed09de8a9a = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_1c0b358c497e4ebfbfd8d32bcd5a7785.setIcon(icon_ed0c573d4b2346b89ba646ed09de8a9a);
            
    
            var popup_d8c04c312b2844378a5391969601d07c = L.popup({maxWidth: '100%'
            
            });

            
                var html_52b68daed258432388f2f74a223fdd4f = $(`<div id="html_52b68daed258432388f2f74a223fdd4f" style="width: 100.0%; height: 100.0%;">Estadio Azteca, Club America</div>`)[0];
                popup_d8c04c312b2844378a5391969601d07c.setContent(html_52b68daed258432388f2f74a223fdd4f);
            

            marker_1c0b358c497e4ebfbfd8d32bcd5a7785.bindPopup(popup_d8c04c312b2844378a5391969601d07c)
            ;

            
        
    
        var marker_059b92df4e454a5984fe99dd62c7abf5 = L.marker(
            [45.109444, 7.641111],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_1d4b4421e62740bb9743aeafa92f8497 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_059b92df4e454a5984fe99dd62c7abf5.setIcon(icon_1d4b4421e62740bb9743aeafa92f8497);
            
    
            var popup_12f9e5b5834b41a1bb68429b701c1c12 = L.popup({maxWidth: '100%'
            
            });

            
                var html_096a6d1990a24892a2be41b4fbcd4c17 = $(`<div id="html_096a6d1990a24892a2be41b4fbcd4c17" style="width: 100.0%; height: 100.0%;">Estadio Juventus, Juventus </div>`)[0];
                popup_12f9e5b5834b41a1bb68429b701c1c12.setContent(html_096a6d1990a24892a2be41b4fbcd4c17);
            

            marker_059b92df4e454a5984fe99dd62c7abf5.bindPopup(popup_12f9e5b5834b41a1bb68429b701c1c12)
            ;

            
        
    
        var marker_32962aea0dfb471398d56f4f159366f6 = L.marker(
            [41.102869, 28.990419],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_e5af69b5276b4c32a4da183c4039cf2d = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_32962aea0dfb471398d56f4f159366f6.setIcon(icon_e5af69b5276b4c32a4da183c4039cf2d);
            
    
            var popup_9413d6f0e1bb4c6ca94c531d5abebe04 = L.popup({maxWidth: '100%'
            
            });

            
                var html_80744bb274b0437e8ba5e9c8d8d4bcb2 = $(`<div id="html_80744bb274b0437e8ba5e9c8d8d4bcb2" style="width: 100.0%; height: 100.0%;">Estadio Türk Telekom, Galatasaray</div>`)[0];
                popup_9413d6f0e1bb4c6ca94c531d5abebe04.setContent(html_80744bb274b0437e8ba5e9c8d8d4bcb2);
            

            marker_32962aea0dfb471398d56f4f159366f6.bindPopup(popup_9413d6f0e1bb4c6ca94c531d5abebe04)
            ;

            
        
    
        var marker_654c432129044cca91ca8e1c55fdb820 = L.marker(
            [48.841389, 2.253056],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_f2168f3808ac4fbfb74756dba41bc378 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_654c432129044cca91ca8e1c55fdb820.setIcon(icon_f2168f3808ac4fbfb74756dba41bc378);
            
    
            var popup_b41d7b267e40443b8d23a86b63638e49 = L.popup({maxWidth: '100%'
            
            });

            
                var html_b22935af307148d8adf9431ec68d08c6 = $(`<div id="html_b22935af307148d8adf9431ec68d08c6" style="width: 100.0%; height: 100.0%;">Estadio Parc des Princes, Paris Saint-Germain </div>`)[0];
                popup_b41d7b267e40443b8d23a86b63638e49.setContent(html_b22935af307148d8adf9431ec68d08c6);
            

            marker_654c432129044cca91ca8e1c55fdb820.bindPopup(popup_b41d7b267e40443b8d23a86b63638e49)
            ;

            
        
    
        var marker_fed179269fa347ec8fde3a26c81d9a19 = L.marker(
            [48.218775, 11.624753],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_c3cc23d32dde455796293eee4b1aedb6);
        
    

                var icon_c5e029413c7843589a5b805f764b855e = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_fed179269fa347ec8fde3a26c81d9a19.setIcon(icon_c5e029413c7843589a5b805f764b855e);
            
    
            var popup_00b03d4cadd44023b8a1787210d6eb12 = L.popup({maxWidth: '100%'
            
            });

            
                var html_091b4f96ec6f4a1fa8e05805de391473 = $(`<div id="html_091b4f96ec6f4a1fa8e05805de391473" style="width: 100.0%; height: 100.0%;">Allianz Arena, Paris Saint-Germain </div>`)[0];
                popup_00b03d4cadd44023b8a1787210d6eb12.setContent(html_091b4f96ec6f4a1fa8e05805de391473);
            

            marker_fed179269fa347ec8fde3a26c81d9a19.bindPopup(popup_00b03d4cadd44023b8a1787210d6eb12)
            ;          
        
</script>
</html>