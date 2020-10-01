---
title: "Mapping Geodata with Folium"
date: 2020-09-17
tags: [ML&AI]
excerpt: "Using python's Folium to create maps"
mathjax: "True"
---



Folium is a python library used to create maps and to work with geo location data.
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

[Link to the Folium Map](
https://colab.research.google.com/drive/1nCnVa-h9RgJzJl2JIcqcZjSC2iotM8qV#scrollTo=6v6OUFoiJBeb)