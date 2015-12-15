# Let's map!

## CartoDB Editor

### Download Dataset
[Actividades Culturales en Madrid](http://datos.madrid.es/portal/site/egob/menuitem.c05c1f754a33a9fbe4b2e4b284f1a5a0/?vgnextoid=6c0b6d01df986410VgnVCM2000000c205a0aRCRD&vgnextchannel=374512b9ace9f310VgnVCM100000171f5a0aRCRD)

### Upload, georeference. Data View
* Type guessing
* Data types

### Second Layer
* Data Library
* Intersection
 
  ```
  UPDATE barrios SET num_points=(SELECT count(*) FROM act_cult_mad a WHERE ST_Intersects(a.the_geom, barrios.the_geom))
  ```

### Styling
* Choropleth/Category Visualization
* Simple / Heatmap
* Torque


### Infowindows + Legends
* Setting 
* HTML edits

### Two value symbolization 
* Conditional CSS
* Category+Bubble
  [Table](https://team.cartodb.com/u/ernestomb/tables/idealista_copy_2)
  ```
  #paradas_metro_madrid{

	[line="L1"] {
	   marker-fill: #30a3dc;
	}
	[line="L2"] {
	   marker-fill: #cd031f;
	}
	[line="L3"] {
	   marker-fill: #ffe114;
	}
	[line="L4"] {
	   marker-fill: #944248;
	}
	[line="L5"] {
	   marker-fill: #96bf0d;
	}
	[line="L6"] {
	   marker-fill: #9fa4a6;
	}
	[line="L7"] {
	   marker-fill: #faa64a;
	}
	[line="L8"] {
	   marker-fill: #f27ca2;
	}
	[line="L9"] {
	   marker-fill: #a3228d;
	}
	[line="L10"] {
	   marker-fill: #084594;
	}
	[line="L11"] {
	   marker-fill: #008b43;
	}
	[line="L12"] {
	   marker-fill: #a49a00;
	}
	[line="R"] {
	   marker-fill: #ffffff;
	   marker-line-color: #084594;
	}
	[line="ML1"] {
	   marker-fill: #ffffff;
	   marker-line-color: #30a3dc;
	   marker-width: 10;
	   marker-line-width: 1.5;
	}
	[line="ML2"] {
	   marker-fill: #ffffff;
	   marker-line-color: #a3228d;
	   marker-width: 10;
	   marker-line-width: 1.5;
	}
	[line="ML3"] {
	   marker-fill: #ffffff;
	   marker-line-color: #cd031f;
	   marker-width: 10;
	   marker-line-width: 1.5;
	}
	[lines=~'.*,.*'] {
	   marker-width:10; 
	   marker-fill: #fff;
	   marker-line-color: #333333;
	   marker-line-width: 1;
	  }

	[ avg_cost <= 99.6512166688177] {
	   marker-width: 26.0;
	}
	 [ avg_cost <= 79.8975594746927] {
	   marker-width: 22.8;
	}
	 [ avg_cost <= 64.4610968295546] {
	   marker-width: 21.3;
	}
	 [ avg_cost <= 55.1861590000312] {
	   marker-width: 19.5;
	}
	 [ avg_cost <= 44.3517170740995] {
	   marker-width: 18.3;
	}
	 [ avg_cost <= 39.3941763691236] {
	   marker-width: 16.7;
	}
	 [ avg_cost <= 31.496878607753] {
	   marker-width: 15.0;
	}
	 [ avg_cost <= 22.7452668127765] {
	   marker-width: 13.3;
	}
	 [ avg_cost <= 19.2089932827128] {
	   marker-width: 12.3;
	}
	 [ avg_cost <= 9.61107134646148] {
	   marker-width: 11.0;
	}

	}
```

### Share
Una vez creado nuestro mapa, podemos compartirlo de diferentes formas. Para empezar, haremos click on "Share" (Compartir) para descubrir las diferentes opciones.

![Compartir](https://www.dropbox.com/s/ikbzn0maq1ygrqs/Captura%20de%20pantalla%202015-12-15%20a%20las%2017.29.49.png?dl=0)

La opción **get the link** nos permitirá compartir el mapa dentro de nuestro perfil público. Esto significa que los visitantes tendrán más facilidad para ver el resto de nuestros mapas publicados. Además, los perfiles públicos incluyen un sistema de comentarios.

La opción **embed it** nos permitirá copiar el código HTML en nuestra página web para insertar nuestro mapa dentro de un artículo, por ejemplo. De esta forma insertaremos el mapa en una web en forma de IFrame.

Finalmente, la opción **CartoDB.js** nos ofrece el link al archivo de configuración de nuestro mapa, de forma que podamos crear aplicaciones interactivas usando Javascript.

# Otros recursos  

* CartoDB Academy: http://academy.cartodb.com
* CartoDB Docs: http://docs.cartodb.com
* CartoDB FAQs: http://docs.cartodb.com/faqs/
* CartoDB Tips&Tricks: http://docs.cartodb.com/tips-and-tricks/
* CartoDB Training: http://cartodb.github.io/training || https://github.com/cartodb/training
