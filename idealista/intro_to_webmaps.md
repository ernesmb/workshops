# Crea tu propia cuenta
Configura una nueva cuenta de CartoDB en https://cartodb.com/signup?

# Online mapping. Una introducción. (by @iriberri)

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

# Visualización de datos en CartoDB
## ¿A partir de qué datos podemos construir un mapa?
Cualquier información que tenga asociado un contenido geoespacial puede ser trasladada a un mapa.

## ¿Qué significa "geoespacial"?
CartoDB puede pintar directamente en un mapa las coordenadas o geometrías que puedan estar incluídas directamente en un archivo. Algunos formatos, como los archivos Shapefile (.shp) suelen contener directamente las geometrías que se pueden dibujar encima de un mapa.

Si no cuentas con un archivo que tenga este tipo de información ya geocodificada, puedes convertir tu información en un mapa si tienes:
  * Nombres de ciudades
  * Códigos postales
  * Provincias o comunidades autónomas (al igual que otro tipo de regiones en el resto del mundo, como los estados de EEUU).
  * Códigos postales
  * Países

## Conociendo diferentes fuentes de datos oficiales
Durante los últimos años ha habido un aumento significativo en la aparición de portales Open Data. Los propios gobiernos locales o nacionales ponen a disposición del público general una serie de documentos con información sobre diferentes aspectos que tienen lugar en lugares específicos. Algunos de estos datos contienen directamente las coordenadas o los polígonos que pueden pintarse sobre un mapa, mientras que otros necesitan ser **georeferenciados**.

## Entendiendo las fuentes de datos. ¿Qué formatos puede leer CartoDB?

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
  
  
CartoDB puede leer archivos Excel siempre y cuando sigan unas reglas básicas de formato:

  * La primera fila del archivo Excel debe contener los títulos para cada columna
  * Las celdas no pueden estar fusionadas: cada celda debe contener su propia información
  * Debemos eliminar las columnas o filas con información no necesaria
  * Si existen varias hojas, CartoDB tomará sólo la primera. 

### Tour: vista de tabla y vista de mapa
Una vez importados, puedes ver tus datos en forma de tabla de forma similar a Excel, o directamente en el mapa.

En la vista de tabla puedes editar tus datos manualmente, así como aplicar filtros sobre ellos.
![Tabla](https://dl.dropboxusercontent.com/u/2879308/Screen%20Shot%202015-03-02%20at%2015.43.09.png)
En la vista de mapa puedes ver espacialmente tus datos, así como editarlos y filtrarlos.
![Mapa](https://dl.dropboxusercontent.com/u/2879308/Screen%20Shot%202015-03-02%20at%2015.43.34.png)


# Nociones básicas de CartoDB
## Georeferenciación
Puedes visualizar tus datos en un mapa simplemente añadiendo geometrías a la información. En general, cualquier dato que quieras mostrar en un mapa necesitan tener una geometría asociada para poder ser dibujados.

### Opciones de georeferenciación

  * Latitud/longitud

    Si tu dataset contiene dos columnas con valores de latitud y longitud puedes usar esta opción para crear los puntos en el mapa.
  * Nombres de ciudades
  * Regiones administrativas

    CartoDB reconoce todas las regiones administrativas de nivel 0 (países), de nivel 1 (estados, CC.AA.) y de nivel 2 únicamente en España (provincias).
  * Códigos postales

    Para Francia, Estados Unidos, Canadá y Australia pueden encontrarse los códigos postales en forma de polígono. Para el resto del mundo se pueden georeferenciar códigos postales en forma de puntos.
  * Direcciones IP
  * Direcciones: By Street Addresses

    CartoDB usa el servicio de geocoding de Nokia para ofrecer esta opción. Tener datos cuidados y muy específicos es muy importante en este caso para evitar errores o conflictos.
  
## Filtrar y visualizar datos en diferentes capas. Ejemplo práctico.

1. Importamos nuestro dataset desde Data Library: Spanish provinces
2. Añadimos una nueva capa a nuestra tabla desde una tabla de populated places: se crea una visualización
3. Usamos el buscador para ir a Madrid
4. Filtramos el antiguo dataset por 'España': adm0name = Spain
5. Dibujamos la capa superior con un wizard de burbujas
6. Cambiamos el basemap
7. Activamos las infowindows
8. Añadimos overlays en algunas ciudades 
9. Editamos leyendas
10. Edición de CartoCSS

![mapa](https://dl.dropboxusercontent.com/u/2879308/Screen%20Shot%202015-04-15%20at%2023.28.16.png)

Una vez creado nuestro mapa, podemos compartirlo de diferentes formas. Para empezar, haremos click on "Share" (Compartir) para descubrir las diferentes opciones.

![Compartir](https://dl.dropboxusercontent.com/u/2879308/Screen%20Shot%202015-03-02%20at%2018.10.36.png)

La opción **get the link** nos permitirá compartir el mapa dentro de nuestro perfil público. Esto significa que los visitantes tendrán más facilidad para ver el resto de nuestros mapas publicados. Además, los perfiles públicos incluyen un sistema de comentarios.

La opción **embed it** nos permitirá copiar el código HTML en nuestra página web para insertar nuestro mapa dentro de un artículo, por ejemplo. De esta forma insertaremos el mapa en una web en forma de IFrame.

Finalmente, la opción **CartoDB.js** nos ofrece el link al archivo de configuración de nuestro mapa, de forma que podamos crear aplicaciones interactivas usando Javascript.

# Otros recursos  

* CartoDB Academy: http://academy.cartodb.com
* CartoDB Docs: http://docs.cartodb.com
* CartoDB FAQs: http://docs.cartodb.com/faqs/
* CartoDB Tips&Tricks: http://docs.cartodb.com/tips-and-tricks/
* CartoDB Training: http://cartodb.github.io/training || https://github.com/cartodb/training