# Drawing shapes on a Leaflet map

## Getting started

### Make a project directory

```
mkdir leaflet-draw-example
```

### Create necessary files

```
touch index.js index.html style.css
```

### Create package.json file

```
npm init
```

Answer the prompts, and you should get output similar to this:

```
{
  "name": "leaflet-draw-example",
  "version": "0.0.0",
  "description": "drawing shapes on a leaflet map",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "MIT"
}
```

### Install leaflet and leaflet-draw

```
npm i --save leaflet leaflet-draw leaflet-providers
```

## Basic CSS & HTML

### Add rule to style.css

```
#map {
  height: 300px;
}
```

### Add boilerplate to index.html

```
<!doctype html>
<html>
<head>
  <title>leaflet-draw example</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="node_modules/leaflet/dist/leaflet.css">
  <link rel="stylesheet" href="node_modules/leaflet-draw/dist/leaflet.draw.css">
  <!--[if lte IE 8]>
    <link rel="stylesheet" href="node_modules/leaflet/dist/leaflet.ie.css" />
  <![endif]-->
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div id="map"></div>
  <script src="bundle.js"></script>
</body>
</html>
```

## Edit index.js

### Require the leaflet modules

```
var L = require('leaflet');
require('leaflet-draw');
require('leaflet-providers');
```

### Set Leaflet images path

```
L.Icon.Default.imagePath = 'node_modules/leaflet/dist/images/';
```

### Create map

```
var map = L.map('map');
```

### Set the latitude, longitude, and zoom of the map

```
map.setView([47.63, -122.32], 11);
```

### Use `L.tileLayer.provider()` method to add Stamen Watercolor tiles and add tile layer to map

```
var layer = L.tileLayer.provider('Stamen.Watercolor');
layer.addTo(map);
```

### Initialize a geoJson layer to save the features drawn on the map

```
var drawnItems = L.geoJson()
map.addLayer(drawnItems);
```

### Create draw controls and add them to the map

```
var drawControl = new L.Control.Draw({
  edit: { featureGroup: drawnItems }
});

map.addControl(drawControl);
```

### Create features array for storing an array fo GeoJSON features

```
var features = [];
```

### Listen for the `draw:created` event
```
map.on('draw:created', function (e) {
  drawnItems.addLayer(e.layer);
  var layers = drawnItems._layers;
  for (var key in layers) features.push(layers[key].toGeoJSON());
  console.log(drawnItems)
});
```

### Listen for the `draw:edited` event
```
map.on('draw:edited', function (e) {
  var layers = drawnItems._layers;
  for (var key in layers) features.push(layers[key].toGeoJSON());
  console.log(drawnItems)
});
```

### Full JavaScript example:

```
var L = require('leaflet');
require('leaflet-draw');
require('leaflet-providers');

L.Icon.Default.imagePath = 'node_modules/leaflet/dist/images/';

var map = L.map('map');
map.setView([47.63, -122.32], 11);
var layer = L.tileLayer.provider('Stamen.Watercolor');
layer.addTo(map);

var drawnItems = L.geoJson();
map.addLayer(drawnItems);

var drawControl = new L.Control.Draw({
  edit: { featureGroup: drawnItems }
});

map.addControl(drawControl);

var features = [];
map.on('draw:created', function (e) {
  drawnItems.addLayer(e.layer);
  var layers = drawnItems._layers;
  for (var key in layers) features.push(layers[key].toGeoJSON());
  console.log(drawnItems)
});

map.on('draw:edited', function (e) {
  var layers = drawnItems._layers;
  for (var key in layers) features.push(layers[key].toGeoJSON());
  console.log(drawnItems)
});
```