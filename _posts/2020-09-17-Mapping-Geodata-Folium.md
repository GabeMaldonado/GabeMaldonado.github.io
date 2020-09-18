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
    <style>#map_53165c7458c04fedadc55de78ba83742 {
        position: relative;
        width: 100.0%;
        height: 100.0%;
        left: 0.0%;
        top: 0.0%;
        }
    </style>
</head>
<body>    
    
    <div class="folium-map" id="map_53165c7458c04fedadc55de78ba83742" ></div>
</body>
<script>    
    
    
        var bounds = null;
    

    var map_53165c7458c04fedadc55de78ba83742 = L.map(
        'map_53165c7458c04fedadc55de78ba83742', {
        center: [30.8082, -118.2474],
        zoom: 3,
        maxBounds: bounds,
        layers: [],
        worldCopyJump: false,
        crs: L.CRS.EPSG3857,
        zoomControl: true,
        });


    
    var tile_layer_d545b2878ff3485d8f27e5549c17f997 = L.tileLayer(
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
}).addTo(map_53165c7458c04fedadc55de78ba83742);
    
        var marker_cacd3a90d2c5450596af4e5550b4a0c2 = L.marker(
            [-34.63565, -58.36465],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_0d2f6e9b18cf4cd4bcfd6c740a6623fa = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'lightgreen',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_cacd3a90d2c5450596af4e5550b4a0c2.setIcon(icon_0d2f6e9b18cf4cd4bcfd6c740a6623fa);
            
    
            var popup_a743c917f11d41a390dbb9273139b125 = L.popup({maxWidth: '100%'
            
            });

            
                var html_438ce8ff36d746b2843227d2ef8f9fef = $(`<div id="html_438ce8ff36d746b2843227d2ef8f9fef" style="width: 100.0%; height: 100.0%;">Estadio 'La Bombonera',  Boca Juniors</div>`)[0];
                popup_a743c917f11d41a390dbb9273139b125.setContent(html_438ce8ff36d746b2843227d2ef8f9fef);
            

            marker_cacd3a90d2c5450596af4e5550b4a0c2.bindPopup(popup_a743c917f11d41a390dbb9273139b125)
            ;

            
        
    
        var marker_7edbbb8ab85840fd954bfca1d318bcd5 = L.marker(
            [-34.545319, -58.449736],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_17006acc3146491da5e0f59b18351af5 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_7edbbb8ab85840fd954bfca1d318bcd5.setIcon(icon_17006acc3146491da5e0f59b18351af5);
            
    
            var popup_213a37bce3ef4bb9b4d35b054922d54c = L.popup({maxWidth: '100%'
            
            });

            
                var html_af11190789f64e5eb0375f5b114df3ac = $(`<div id="html_af11190789f64e5eb0375f5b114df3ac" style="width: 100.0%; height: 100.0%;">Estadio Monumental Americo Vespucio, River Plate</div>`)[0];
                popup_213a37bce3ef4bb9b4d35b054922d54c.setContent(html_af11190789f64e5eb0375f5b114df3ac);
            

            marker_7edbbb8ab85840fd954bfca1d318bcd5.bindPopup(popup_213a37bce3ef4bb9b4d35b054922d54c)
            ;

            
        
    
        var marker_603db52584ab4791ae77804af014979f = L.marker(
            [-34.670267, -58.370969],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_a553c4edf4b646e1852c1b8f54bf4cb5 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_603db52584ab4791ae77804af014979f.setIcon(icon_a553c4edf4b646e1852c1b8f54bf4cb5);
            
    
            var popup_832ed34a45a14ab6be93270a37d8bde6 = L.popup({maxWidth: '100%'
            
            });

            
                var html_c8ab902b51c34d199f1d4aeb240799a3 = $(`<div id="html_c8ab902b51c34d199f1d4aeb240799a3" style="width: 100.0%; height: 100.0%;">Estadio Libertadores De América, Club Atlético Independiente</div>`)[0];
                popup_832ed34a45a14ab6be93270a37d8bde6.setContent(html_c8ab902b51c34d199f1d4aeb240799a3);
            

            marker_603db52584ab4791ae77804af014979f.bindPopup(popup_832ed34a45a14ab6be93270a37d8bde6)
            ;

            
        
    
        var marker_41a986316741427c86fa52d2462cc4cd = L.marker(
            [-25.292072, -57.657381],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_50d5c0479a9c4905bad041f231c781d8 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_41a986316741427c86fa52d2462cc4cd.setIcon(icon_50d5c0479a9c4905bad041f231c781d8);
            
    
            var popup_e1796df7bc7547418f0453118d134152 = L.popup({maxWidth: '100%'
            
            });

            
                var html_d9ecca1b66cd4098891cb06e4def9847 = $(`<div id="html_d9ecca1b66cd4098891cb06e4def9847" style="width: 100.0%; height: 100.0%;">Estadio Defensores del Chaco</div>`)[0];
                popup_e1796df7bc7547418f0453118d134152.setContent(html_d9ecca1b66cd4098891cb06e4def9847);
            

            marker_41a986316741427c86fa52d2462cc4cd.bindPopup(popup_e1796df7bc7547418f0453118d134152)
            ;

            
        
    
        var marker_060f5f563614499f9c46c2f24b3c1101 = L.marker(
            [-34.796917, -56.067167],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_f3c4da950b974cd3a22e3c3718a5a0d3 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_060f5f563614499f9c46c2f24b3c1101.setIcon(icon_f3c4da950b974cd3a22e3c3718a5a0d3);
            
    
            var popup_31dd51db9e4d4a7a96b8518bea74df32 = L.popup({maxWidth: '100%'
            
            });

            
                var html_458d1ea8af934c2a98a7d53060f450f5 = $(`<div id="html_458d1ea8af934c2a98a7d53060f450f5" style="width: 100.0%; height: 100.0%;">Estadio Campeón del Siglo, Peñarol</div>`)[0];
                popup_31dd51db9e4d4a7a96b8518bea74df32.setContent(html_458d1ea8af934c2a98a7d53060f450f5);
            

            marker_060f5f563614499f9c46c2f24b3c1101.bindPopup(popup_31dd51db9e4d4a7a96b8518bea74df32)
            ;

            
        
    
        var marker_eb4cf046aeae44a6aaea6b0f25b8026d = L.marker(
            [-34.884373, -56.1588],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_339277660a5d4b47a667120343c20a77 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_eb4cf046aeae44a6aaea6b0f25b8026d.setIcon(icon_339277660a5d4b47a667120343c20a77);
            
    
            var popup_af2b7a69e49c4ef987615256e3abd8d3 = L.popup({maxWidth: '100%'
            
            });

            
                var html_c85b2db0d6dc402b835c58aac82f54db = $(`<div id="html_c85b2db0d6dc402b835c58aac82f54db" style="width: 100.0%; height: 100.0%;">Estadio Gran Parque Central, Nacional</div>`)[0];
                popup_af2b7a69e49c4ef987615256e3abd8d3.setContent(html_c85b2db0d6dc402b835c58aac82f54db);
            

            marker_eb4cf046aeae44a6aaea6b0f25b8026d.bindPopup(popup_af2b7a69e49c4ef987615256e3abd8d3)
            ;

            
        
    
        var marker_680325430c6b49c680695c25641c59e4 = L.marker(
            [-33.506611, -70.605944],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_018202a00812436aba50d2152bf75c74 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_680325430c6b49c680695c25641c59e4.setIcon(icon_018202a00812436aba50d2152bf75c74);
            
    
            var popup_d5306fb420324a5c91da585c4d513de2 = L.popup({maxWidth: '100%'
            
            });

            
                var html_e04ca9810ca24e88a1f50e665c6f123a = $(`<div id="html_e04ca9810ca24e88a1f50e665c6f123a" style="width: 100.0%; height: 100.0%;">Estadio Monumental David Arellano, Colo-Colo</div>`)[0];
                popup_d5306fb420324a5c91da585c4d513de2.setContent(html_e04ca9810ca24e88a1f50e665c6f123a);
            

            marker_680325430c6b49c680695c25641c59e4.bindPopup(popup_d5306fb420324a5c91da585c4d513de2)
            ;

            
        
    
        var marker_14fb9f0f155a41988036e154af0dbdb1 = L.marker(
            [-12.055694, -76.935972],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_dbb97bdc6585455d80461d10443de127 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_14fb9f0f155a41988036e154af0dbdb1.setIcon(icon_dbb97bdc6585455d80461d10443de127);
            
    
            var popup_010f877a275443b49dc3d55e9310ad4c = L.popup({maxWidth: '100%'
            
            });

            
                var html_6a2b4b133a7c4c8e8dc485ac2fab5ad9 = $(`<div id="html_6a2b4b133a7c4c8e8dc485ac2fab5ad9" style="width: 100.0%; height: 100.0%;">Estadio Monumental "U", Club Universitario de Deportes</div>`)[0];
                popup_010f877a275443b49dc3d55e9310ad4c.setContent(html_6a2b4b133a7c4c8e8dc485ac2fab5ad9);
            

            marker_14fb9f0f155a41988036e154af0dbdb1.bindPopup(popup_010f877a275443b49dc3d55e9310ad4c)
            ;

            
        
    
        var marker_9f74b69b09e145a29ba35b6fd36924e4 = L.marker(
            [0.107717, -78.489103],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_90fdfd34d6714418a0a88c273e3876db = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_9f74b69b09e145a29ba35b6fd36924e4.setIcon(icon_90fdfd34d6714418a0a88c273e3876db);
            
    
            var popup_e5f8057af4444049a09726bddcffc88a = L.popup({maxWidth: '100%'
            
            });

            
                var html_5213db134fb64ed28311bf86d44f603d = $(`<div id="html_5213db134fb64ed28311bf86d44f603d" style="width: 100.0%; height: 100.0%;">Estadio Rodrigo Paz Delgado, Liga Deportiva Universitaria</div>`)[0];
                popup_e5f8057af4444049a09726bddcffc88a.setContent(html_5213db134fb64ed28311bf86d44f603d);
            

            marker_9f74b69b09e145a29ba35b6fd36924e4.bindPopup(popup_e5f8057af4444049a09726bddcffc88a)
            ;

            
        
    
        var marker_89b37e67bb4b4887a839cdc4a4ee2f92 = L.marker(
            [-0.177528, -78.476583],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_4a766d1cd823484da119a6021542aaa2 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_89b37e67bb4b4887a839cdc4a4ee2f92.setIcon(icon_4a766d1cd823484da119a6021542aaa2);
            
    
            var popup_66b0898319884342a39f5029944369d9 = L.popup({maxWidth: '100%'
            
            });

            
                var html_0e83087778244d04bc382360c1b20e10 = $(`<div id="html_0e83087778244d04bc382360c1b20e10" style="width: 100.0%; height: 100.0%;">Estadio Olímpico Atahualpa</div>`)[0];
                popup_66b0898319884342a39f5029944369d9.setContent(html_0e83087778244d04bc382360c1b20e10);
            

            marker_89b37e67bb4b4887a839cdc4a4ee2f92.bindPopup(popup_66b0898319884342a39f5029944369d9)
            ;

            
        
    
        var marker_8cb0d5a5c07448d79d56d529a0a72460 = L.marker(
            [-2.185869, -79.924931],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_3102867abdfc4258a714a8be7afcefea = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_8cb0d5a5c07448d79d56d529a0a72460.setIcon(icon_3102867abdfc4258a714a8be7afcefea);
            
    
            var popup_8cff4cb42c2e4b20979427918b6533d7 = L.popup({maxWidth: '100%'
            
            });

            
                var html_d4e38d4f5f89488aa35993aa7ea00b24 = $(`<div id="html_d4e38d4f5f89488aa35993aa7ea00b24" style="width: 100.0%; height: 100.0%;">Estadio Isidro Romero Carbo, Barcelona Sporting Club</div>`)[0];
                popup_8cff4cb42c2e4b20979427918b6533d7.setContent(html_d4e38d4f5f89488aa35993aa7ea00b24);
            

            marker_8cb0d5a5c07448d79d56d529a0a72460.bindPopup(popup_8cff4cb42c2e4b20979427918b6533d7)
            ;

            
        
    
        var marker_50b07011746341f8a7951481642c788b = L.marker(
            [40.736667, -74.15027],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_fab8d9ae9c22406d8a478efb2bf155fa = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_50b07011746341f8a7951481642c788b.setIcon(icon_fab8d9ae9c22406d8a478efb2bf155fa);
            
    
            var popup_e443aa96b2eb49e2bc174d47a6337f01 = L.popup({maxWidth: '100%'
            
            });

            
                var html_97e72cb13df24f04a2887d76a184122d = $(`<div id="html_97e72cb13df24f04a2887d76a184122d" style="width: 100.0%; height: 100.0%;">Red Bull Arena, New York Red Bulls</div>`)[0];
                popup_e443aa96b2eb49e2bc174d47a6337f01.setContent(html_97e72cb13df24f04a2887d76a184122d);
            

            marker_50b07011746341f8a7951481642c788b.bindPopup(popup_e443aa96b2eb49e2bc174d47a6337f01)
            ;

            
        
    
        var marker_79d19840445e4f4bbdb3fabcb05818f4 = L.marker(
            [33.755556, -84.4],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_6d2815c3d3854268af9956eacc117215 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_79d19840445e4f4bbdb3fabcb05818f4.setIcon(icon_6d2815c3d3854268af9956eacc117215);
            
    
            var popup_001480b2167f477e9b68221b137980d0 = L.popup({maxWidth: '100%'
            
            });

            
                var html_52b8893664ce407698203e1935198821 = $(`<div id="html_52b8893664ce407698203e1935198821" style="width: 100.0%; height: 100.0%;">Estadio Mercedes Benz, Atlanta United</div>`)[0];
                popup_001480b2167f477e9b68221b137980d0.setContent(html_52b8893664ce407698203e1935198821);
            

            marker_79d19840445e4f4bbdb3fabcb05818f4.bindPopup(popup_001480b2167f477e9b68221b137980d0)
            ;

            
        
    
        var marker_9b1cbc733c214d5a8db3dc221b8cb2e5 = L.marker(
            [33.864, -118.261],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_75454670832f4d11bf3d22601842e64c = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_9b1cbc733c214d5a8db3dc221b8cb2e5.setIcon(icon_75454670832f4d11bf3d22601842e64c);
            
    
            var popup_9e67e3fb794744e79bdfc6fad8ca3d5a = L.popup({maxWidth: '100%'
            
            });

            
                var html_c187e8609bc247da904d948f9316d003 = $(`<div id="html_c187e8609bc247da904d948f9316d003" style="width: 100.0%; height: 100.0%;">Dignity Health Sports Park, LA Galaxy</div>`)[0];
                popup_9e67e3fb794744e79bdfc6fad8ca3d5a.setContent(html_c187e8609bc247da904d948f9316d003);
            

            marker_9b1cbc733c214d5a8db3dc221b8cb2e5.bindPopup(popup_9e67e3fb794744e79bdfc6fad8ca3d5a)
            ;

            
        
    
        var marker_cc7b2c35501e4993859c64ca7e2403d9 = L.marker(
            [40.45301, -3.68829],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_f514151bfd8442058b1c803ef5e1795e = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_cc7b2c35501e4993859c64ca7e2403d9.setIcon(icon_f514151bfd8442058b1c803ef5e1795e);
            
    
            var popup_85b55106c1bf44debce25ebce871597b = L.popup({maxWidth: '100%'
            
            });

            
                var html_4e7aa9ab06d2450bad8be3b8915e976b = $(`<div id="html_4e7aa9ab06d2450bad8be3b8915e976b" style="width: 100.0%; height: 100.0%;">Estadio Santiago Bernabeu, Real Madrid</div>`)[0];
                popup_85b55106c1bf44debce25ebce871597b.setContent(html_4e7aa9ab06d2450bad8be3b8915e976b);
            

            marker_cc7b2c35501e4993859c64ca7e2403d9.bindPopup(popup_85b55106c1bf44debce25ebce871597b)
            ;

            
        
    
        var marker_f9e53b6298bc4fea86d1031d80f86d07 = L.marker(
            [41.3808, 2.12311],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_b35697f51ff94f5cac3a60c64e727e1d = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_f9e53b6298bc4fea86d1031d80f86d07.setIcon(icon_b35697f51ff94f5cac3a60c64e727e1d);
            
    
            var popup_24e2e72e7f2848ba8c4dc5c36811f99c = L.popup({maxWidth: '100%'
            
            });

            
                var html_c2c23791d2de462da36b6294163031ad = $(`<div id="html_c2c23791d2de462da36b6294163031ad" style="width: 100.0%; height: 100.0%;">Estadio Camp Nou, FC Barcelona</div>`)[0];
                popup_24e2e72e7f2848ba8c4dc5c36811f99c.setContent(html_c2c23791d2de462da36b6294163031ad);
            

            marker_f9e53b6298bc4fea86d1031d80f86d07.bindPopup(popup_24e2e72e7f2848ba8c4dc5c36811f99c)
            ;

            
        
    
        var marker_4a19295b40844a3fa4e5c6c3b38a2261 = L.marker(
            [38.752648359600805, -9.184699058532715],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_ee633be6350f45d2a73b41803cb9514b = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_4a19295b40844a3fa4e5c6c3b38a2261.setIcon(icon_ee633be6350f45d2a73b41803cb9514b);
            
    
            var popup_a259201816204d9a99a232bc87a4d5c2 = L.popup({maxWidth: '100%'
            
            });

            
                var html_e9cc84031db449dbac6be165da4a51b6 = $(`<div id="html_e9cc84031db449dbac6be165da4a51b6" style="width: 100.0%; height: 100.0%;">Estadio do Sport Lisboa e Benfica</div>`)[0];
                popup_a259201816204d9a99a232bc87a4d5c2.setContent(html_e9cc84031db449dbac6be165da4a51b6);
            

            marker_4a19295b40844a3fa4e5c6c3b38a2261.bindPopup(popup_a259201816204d9a99a232bc87a4d5c2)
            ;

            
        
    
        var marker_90ef3a9a2f87464daf85123ee2fd0ece = L.marker(
            [-22.912167, -43.230164],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_69e4649c3f494725a459e01b6531bc82 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_90ef3a9a2f87464daf85123ee2fd0ece.setIcon(icon_69e4649c3f494725a459e01b6531bc82);
            
    
            var popup_f061a051901842968530c9e6533d4c9c = L.popup({maxWidth: '100%'
            
            });

            
                var html_fbaae938b8ed42bc88f91e03a38d9367 = $(`<div id="html_fbaae938b8ed42bc88f91e03a38d9367" style="width: 100.0%; height: 100.0%;">Estadio Maracana</div>`)[0];
                popup_f061a051901842968530c9e6533d4c9c.setContent(html_fbaae938b8ed42bc88f91e03a38d9367);
            

            marker_90ef3a9a2f87464daf85123ee2fd0ece.bindPopup(popup_f061a051901842968530c9e6533d4c9c)
            ;

            
        
    
        var marker_f06200d8f04a417d8ed0f036ce400337 = L.marker(
            [19.303056, -99.150556],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_b5ea611c71774d40b296aec75a89c166 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_f06200d8f04a417d8ed0f036ce400337.setIcon(icon_b5ea611c71774d40b296aec75a89c166);
            
    
            var popup_28ba9d5711ee419792c9f01cf579897f = L.popup({maxWidth: '100%'
            
            });

            
                var html_2a311f5d46d143b983a49bc96314e18a = $(`<div id="html_2a311f5d46d143b983a49bc96314e18a" style="width: 100.0%; height: 100.0%;">Estadio Azteca, Club America</div>`)[0];
                popup_28ba9d5711ee419792c9f01cf579897f.setContent(html_2a311f5d46d143b983a49bc96314e18a);
            

            marker_f06200d8f04a417d8ed0f036ce400337.bindPopup(popup_28ba9d5711ee419792c9f01cf579897f)
            ;

            
        
    
        var marker_ce9a826165f5416780784c88547cd83c = L.marker(
            [45.109444, 7.641111],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_564c50333a6648a99581d6343032697e = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_ce9a826165f5416780784c88547cd83c.setIcon(icon_564c50333a6648a99581d6343032697e);
            
    
            var popup_3ee7b3f819994f5585fc25cd4e137b72 = L.popup({maxWidth: '100%'
            
            });

            
                var html_2f1f1e98c01d474f98fa4308481dd2ec = $(`<div id="html_2f1f1e98c01d474f98fa4308481dd2ec" style="width: 100.0%; height: 100.0%;">Estadio Juventus, Juventus </div>`)[0];
                popup_3ee7b3f819994f5585fc25cd4e137b72.setContent(html_2f1f1e98c01d474f98fa4308481dd2ec);
            

            marker_ce9a826165f5416780784c88547cd83c.bindPopup(popup_3ee7b3f819994f5585fc25cd4e137b72)
            ;

            
        
    
        var marker_83cdaedd787e4f6ca045b6e57ec03b5a = L.marker(
            [41.102869, 28.990419],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_9398366db4604ea1b4bd1d56f2186b31 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_83cdaedd787e4f6ca045b6e57ec03b5a.setIcon(icon_9398366db4604ea1b4bd1d56f2186b31);
            
    
            var popup_7018e340d65b4dcbb8a9430e686c3e70 = L.popup({maxWidth: '100%'
            
            });

            
                var html_07caf072456a40a298a81db388ded4a1 = $(`<div id="html_07caf072456a40a298a81db388ded4a1" style="width: 100.0%; height: 100.0%;">Estadio Türk Telekom, Galatasaray</div>`)[0];
                popup_7018e340d65b4dcbb8a9430e686c3e70.setContent(html_07caf072456a40a298a81db388ded4a1);
            

            marker_83cdaedd787e4f6ca045b6e57ec03b5a.bindPopup(popup_7018e340d65b4dcbb8a9430e686c3e70)
            ;

            
        
    
        var marker_bc666bfa11594bbfb83a9ac51f43ae39 = L.marker(
            [48.841389, 2.253056],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_3f744d9c3bae468d9924add6c5204463 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_bc666bfa11594bbfb83a9ac51f43ae39.setIcon(icon_3f744d9c3bae468d9924add6c5204463);
            
    
            var popup_422cfa0068794e7bbb30c7e0173b0c52 = L.popup({maxWidth: '100%'
            
            });

            
                var html_ca24aea9868341fdbafe79bc76453c17 = $(`<div id="html_ca24aea9868341fdbafe79bc76453c17" style="width: 100.0%; height: 100.0%;">Estadio Parc des Princes, Paris Saint-Germain </div>`)[0];
                popup_422cfa0068794e7bbb30c7e0173b0c52.setContent(html_ca24aea9868341fdbafe79bc76453c17);
            

            marker_bc666bfa11594bbfb83a9ac51f43ae39.bindPopup(popup_422cfa0068794e7bbb30c7e0173b0c52)
            ;

            
        
    
        var marker_fb1e9488e9654fc4bb31a9f90ed19fef = L.marker(
            [48.218775, 11.624753],
            {
                icon: new L.Icon.Default(),
                }
            ).addTo(map_53165c7458c04fedadc55de78ba83742);
        
    

                var icon_cd7b6de8b1d1470cbe3cb1568f45c9f1 = L.AwesomeMarkers.icon({
                    icon: 'info-sign',
                    iconColor: 'white',
                    markerColor: 'green',
                    prefix: 'glyphicon',
                    extraClasses: 'fa-rotate-0'
                    });
                marker_fb1e9488e9654fc4bb31a9f90ed19fef.setIcon(icon_cd7b6de8b1d1470cbe3cb1568f45c9f1);
            
    
            var popup_8e2cd18d129842f5b6b0a4672bd964c5 = L.popup({maxWidth: '100%'
            
            });

            
                var html_e550089c95c647458dca77d019cc4f4c = $(`<div id="html_e550089c95c647458dca77d019cc4f4c" style="width: 100.0%; height: 100.0%;">Allianz Arena, Paris Saint-Germain </div>`)[0];
                popup_8e2cd18d129842f5b6b0a4672bd964c5.setContent(html_e550089c95c647458dca77d019cc4f4c);
            

            marker_fb1e9488e9654fc4bb31a9f90ed19fef.bindPopup(popup_8e2cd18d129842f5b6b0a4672bd964c5)
            ;

            
        
</script>