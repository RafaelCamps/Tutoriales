# API Google Maps - JavaScript

## Insertar un mapa en nuestra Web

Para añadir un mapa de google maps a nuestra web es necesario tener una API key, que debemos solicitarla desde la consola para desarrolladores de google, una vez tengamos la APIkey debemos insertar el siguiente código en nuestro HTML:

```HTML

<script async defer src="https://maps.googleapis.com/maps/api/js?key=aquí-debemos-poner-nuestra-apikey&callback=initMap">
    </script>
```

Ahora es necesario crear un contenedor donde mostrar el mapa:

```html
<div id="mapa"></div>
```

A este `<div>` hay que darle unas propiedades `css` para que sea visible:

```css
/*Dentro del archivo .css*/
#mapa {
  height: 400px; /*La altura que queramos que tenga el contenedor del mapa*/
  width: 100%; /*El ancho que queremos que tenga el contenedor del mapa*/
}
```

Ahora solamente nos falta pasarle los datos a la función `initMap()` que es la que se ejecuta para mostrar el mapa, en el `<script>` que hemos copiado antes en **HTML** se ve al final del `src` es el **callback**.  
Para esto en nuestro archivo `.js` creamos dicha función:

```javascript
//Creamos la función initMap()

function initMap() {
  // Creamos la variable 'map', que es la q va a contener el mapa, esta recibe 2 parámetros, el contenedor donde mostrar el mapa y un objeto con las opciones:
  var map = new google.maps.Map(document.getElementById("mapa"), {
    // Una de las opciones es el zoom que queremos en el mapa
    zoom: 18,
    // Otra opción es dónde va a estar el centro del mismo
    center: restaurante,
  });
}
```

### Añadir un marcador

Dentro de la función `initMap()` debemos crear un marcador:

```javascript
function initMap() {
  // .
  // .
  // Tras declarar la variable map, creamos un marcador, que debe recibir ciertas propiedades:

  var marker = new google.maps.Marker({
    // Las coordenadas dónde ubicar el marcador - OBLIGATORIO
    position: { lat: 39.642306, lng: 3.006223 },
    // la referencia de en q mapa se debe mostrar - OBLIGATORIO
    map: map,
    // Un icono personlalizado, si se quiere, OPCIONAL
    icon: icono,
    // Un título que aparecerá al posicionar el ratón sobre el marcador, OPCIONAL
    title: nombre,
  });
}
```

### Añadir una ventana informativa al marcador

Es para que cuando alguien haga click sobre el marcador, aparezca un modal con cierta información sobre ese punto:

```javascript
// Dentro de la función initMap()

function initMap(){

// Creamos mapa
.
.
.
// Creamos marcador
.
.
.
// Creamos infoWindow, para ello creamos una variable

    var infowindow = new google.maps.InfoWindow({
    // Aquí le indicamos el contenido que queremos que tenga el modal
    content:
        '<h1>Nombre del sitio</h1><a href="https://www.misitio.com">Enlace a la web</a>',
    });

    // Tras crear la "infoWindow", la añadimos al marcador, añadiéndole a este un eventListener

    marker.addListener("click", function () {
    //Cuando el marcador reciba un click, se mostrará la infoWindow
    infowindow.open(map, marker);
    });
}


```

### Insertar múltiples marcadores en el mapa

Para insertar múltiples marcadores, lo mejor es hacerlo mediante una función que debemos crear, así evitamos tener que repetir los pasos de insertar un marcador, múltiples veces.

```javascript
// Creamos nuestra función que va a recibir unas propiedades, de un array de marcadores
function addMarker(props) {

    // La función va a crear un marcador con los datos recibidos del array de marcadores
      var marker = new google.maps.Marker({
        position: props.coords,
        map: map,
        title: props.title,
      });

     //Comprobamos si este marcador debe llevar un icono personalizado, si es así se lo asignamos al marcador
     if(props.iconImage){
         //Asignamos la imagen recibida al marcador
         marker.setIcon(props.iconImage)
     }

     //Comprobamos si el marcador recibe contenido para mostrar la infoWindow, si es así la creamos

      if (props.content) {
        //Creamos la infoWindow
        var infowindow = new google.maps.InfoWindow({
          content: props.content,
        });
        // Añadimos el evento al marcador, para mostrar la ventana.
        marker.addListener("click", function () {
          infowindow.open(map, marker);
        });
      }
    }

}

```

#### Crear el array con todos los marcadores

Para crear el array de marcadores, debemos crear un array de objetos, y cada uno debe tener las propiedades coords y title, el resto de propiedades son opcionales:

```javascript
var markers = [
  {
    //Marcador 1
    coords: {
      lat: 39.025631,
      lng: 2.125684,
    },
    title: "Título del marcador",
    content:
      "El contenido HTML que vamos a mostrar en la infoWindow, esta propiedad es opcional",
    iconImage:
      "ruta a la imagen del icono que queremos usar, si queremos un icono personalizado, esta propiedad es opcional",
  },
  {
    //Marcador 2
    coords: {
      lat: 43.025631,
      lng: 9.125684,
    },
    title: "Título del marcador 2",
    content:
      "El contenido HTML que vamos a mostrar en la infoWindow, esta propiedad es opcional",
    iconImage:
      "ruta a la imagen del icono que queremos usar, si queremos un icono personalizado, esta propiedad es opcional",
  },
  {
    //Un objeto por cada marcador, tantos cómo queramos!!
  },
];
```

Al llamar a la función, deberemos pasarle el objeto `props` que sería cada uno de los objetos contenidos en el array de marcadores, por lo que podríamos hacerlo mediante un bucle for:

```javascript
// Bucle for que ejecuta la función addMarkers tantas veces cómo marcadores tengamos en el array

for (var i = 0; i < markers.length; i++) {
  addMarker(markers[i]);
}
```
