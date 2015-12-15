# Webmaps. Una introducción. (by **@iriberri**)

## Qué es y cómo funciona: basemaps, tiles, rendering...

En 1996, MapQuest lanzó su servicio web.

![Mapquest](http://www.maps-of-mexico.com/images/mapquest.jpg)

Los primeros mapas web se componían de imágenes completas a las que se accedía mediante un menú de flechas. Para mover el mapa, era necesario volver a cargar toda la página con una nueva imagen.

En 2005, Google Maps preparó el camino que hasta entonces han ido siguiendo los mapas web. Google introdujo el concepto de "tile".

![GMaps](https://dl.dropboxusercontent.com/u/2879308/Screen%20Shot%202015-04-15%20at%2011.44.37.png)

Un tile es una imagen de 256x256 píxeles que tiene unos límites específicados, es decir, aunque el mapa sea diferente, ese tile siempre pertenece a un mismo lugar geográfico.

![Tile](https://dl.dropboxusercontent.com/u/2879308/tiles.gif)

La generación de mapas a partir de tiles permitió que los mapas web fueran mucho más rápidos de cargar, puesto que se reciben imágenes más pequeñas y únicamente se piden aquellas necesarias.

Los tiles se organizan por nivel de zoom: cada nivel de zoom tiene su propio conjunto de tiles.

En el **nivel de zoom 0** existe únicamente una imagen (tile) para mostrar todo el mundo

![Zoom 0](https://stamen-tiles-b.a.ssl.fastly.net/toner/0/0/0.png)

Con cada nivel de zoom adicional, el número de tiles aumenta exponencialmente.

En el **nivel de zoom 4** existen cuatro tiles para mostrar todo el mundo

![4-1](https://stamen-tiles-b.a.ssl.fastly.net/toner-background/1/0/0.png)
![4-3](https://stamen-tiles-b.a.ssl.fastly.net/toner-background/1/1/0.png)
![4-2](https://stamen-tiles-b.a.ssl.fastly.net/toner-background/1/0/1.png)
![4-4](https://stamen-tiles-b.a.ssl.fastly.net/toner-background/1/1/1.png)

A nivel 6:

![6](https://stamen-tiles-d.a.ssl.fastly.net/toner/6/32/23.png)

Estos tiles se renderizan y se almacenan en una caché. Un tile de un mapa es simplemente una imagen, por lo que nos podemos referir a ésta individualmente.

Por ejemplo:

**http://tile.openstreetmap.org/4/2/6.png**

![OSM](http://tile.openstreetmap.org/4/2/6.png)

La estructura de la URL nos permite saber que la tile pertenece al zoom 4 y tiene la posición X=2 Y=6 en el mapa.

![schema](https://i-msdn.sec.s-msft.com/dynimg/IC96238.jpg)

En general, un mapa se construye añadiendo capas de tiles encima de otras. Estas capas son comúnmente llamadas "baselayer" (mapa de base) y "datalayer" (que incluye encima cualquier dato, como puntos, polígonos o líneas).

Un **mapa base** es una capa estática que suele estar siempre presente en los mapas web y nos permite tener una percepción de la localización geográfica.

Los mapas base, al ser estáticos, se generan y se cachean para siempre (hasta que se desee añadir un cambio, como añadir una calle nueva en un mapa).

![mapabase](https://dl.dropboxusercontent.com/u/2879308/Screen%20Shot%202015-04-15%20at%2011.55.22.png)

Una **capa de datos** se dibuja encima del mapa base y permite analizar los datos geoespacialmente.

Las capas de datos se generan cada vez que aplicamos un estilo en nuestro mapa y se invalidan cada vez que hacemos un cambio en él ( código CartoCSS o cambios en los datos) para volverse a generar y cachear de nuevo.

![datos](https://dl.dropboxusercontent.com/u/2879308/Screen%20Shot%202015-04-15%20at%2011.55.37.png)

Cachear las imágenes permite que los mapas sean rápidos ya que los servidores no tienen que redibujar la información en el mapa cada vez que alguien accede al mismo.

![mercator](https://dl.dropboxusercontent.com/u/2879308/mercator.jpg)

==============

# Visualización de datos en CartoDB. Datasets, Layers y Mapas
## ¿A partir de qué datos podemos construir un mapa?
Cualquier información que tenga asociado un contenido geoespacial puede ser trasladada a un mapa. A un conjunto de datos con un formato adecuado se le llama **'Dataset'**

### ¿Qué significa "geoespacial"?
CartoDB puede pintar directamente en un mapa las coordenadas o geometrías que puedan estar incluídas directamente en un archivo. Algunos formatos, como los archivos Shapefile (.shp) suelen contener directamente las geometrías que se pueden dibujar encima de un mapa.

Si no cuentas con un archivo que tenga este tipo de información ya geocodificada, puedes convertir tu información en un mapa si tienes:
  * Nombres de ciudades
  * Códigos postales
  * Provincias y otras regiones administrativas
  * Códigos postales
  * Países

## ¿Qué formatos puede leer CartoDB?

CartoDB puede leer diferentes formatos:
* Archivos KML
* GeoJSON
* Shapefiles
* Archivos Excel
* Archivos CSV:

  ```
  provincia, partido, votos
  Alicante, PP, 2345
  Alicante, PSOE, 2345
  ```
  
  Los archivos CSV pueden crearse con cualquier editor de texto, como el bloc de notas.  

## Layers y Mapas
Una vez importados, puedes ver tus datos en forma de tabla, o directamente en el mapa.
A la representación geográfica de cada 'Dataset' lo llamamos **layer**
Un **mapa** puede contener una o más layers

En la vista de tabla puedes editar tus datos manualmente, así como aplicar filtros sobre ellos.
![Tabla](https://dl.dropboxusercontent.com/u/2879308/Screen%20Shot%202015-03-02%20at%2015.43.09.png)
En la vista de mapa puedes ver espacialmente tus datos, así como editarlos y filtrarlos.
![Mapa](https://dl.dropboxusercontent.com/u/2879308/Screen%20Shot%202015-03-02%20at%2015.43.34.png)
  
## PostGIS+CartoCSS
CartoDB utiliza una base de datos con capacidad espacial para almacenar, modificar y mostrar los datos. 
Cuando realizamos una 'consulta' (**query**) a la base de datos, establecemos una serie de normas para su representación. Estas normas se escriben en lenguaje [CartoCSS](https://github.com/mapbox/carto/blob/master/docs/latest.md).


