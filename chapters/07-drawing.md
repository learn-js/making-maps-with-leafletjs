# Drawing shapes on a Leaflet map

In this tutorial we'll cover how to create a map with Leaflet.js that you can draw shapes on!

## Getting started

To get started we'll create the folder and files needed, and install dependencies.

### Make a project directory

```
mkdir leaflet-draw-example
cd leaflet-draw-example
```

Create the directory for the project with `mkdir`, then enter the directory using `cd`.

### Create necessary files

```
touch index.js index.html style.css
```

Use `touch` to create the necessary files for the project.

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

We'll install the 3 dependencies for the project using `npm`.

## Basic CSS & HTML

The HTML and CSS for this project is fairly minimal, we'll mostly focus on the JavaScript required to get started with a drawing project.

### Add rule to style.css

```
html,
body {
  margin: 0px;
  height: 100%;
  width: 100%;
}

#map {
  height: 100%;
  width: 100%;
}
```

These CSS styles ensure that the map fits the full width and height of the browser window.

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

Note that the css is being pulled directly from the dependencies in the node_modules folder. This means that you should add the entire node_modules folder to a .gitignore file if you're using git.

## Edit index.js

### Require the leaflet modules

```
var L = require('leaflet');
require('leaflet-draw');
require('leaflet-providers');
```

Note that leaflet-draw and leaflet-providers are being added to the global scope when they are required without setting them to a variable. This makes it so they can add methods to Leaflet's `L` object.

### Set Leaflet images path

```
L.Icon.Default.imagePath = 'node_modules/leaflet/dist/images/';
```

Leaflet needs to know that the images are in this folder.

### Create map

```
var map = L.map('map');
```

Create the map using the `L.map` method.

### Set the latitude, longitude, and zoom of the map

```
map.setView([47.63, -122.32], 11);
```

The `map.setView` method sets the latitude, longitude, and zoom level.

### Use `L.tileLayer.provider()` method to add Stamen Watercolor tiles and add tile layer to map

```
var layer = L.tileLayer.provider('Stamen.Watercolor');
layer.addTo(map);
```

The Watercolor tileset from Stamen is super pretty, so it's a fun example to use. Note that the `provider` method was added because we required the leaflet-providers module.

### Initialize a geoJson layer to save the features drawn on the map

```
var drawnItems = L.geoJson()
map.addLayer(drawnItems);
```

This initializes a `drawnItems` object which we'll use to track the features you draw on the map.

### Create draw controls and add them to the map

```
var drawControl = new L.Control.Draw({
  edit: { featureGroup: drawnItems }
});

map.addControl(drawControl);
```

Adding leaflet-draw controls to the map is pretty easy. By default we'll be able to draw polygons, circles, rectangles, lines, and points.

### Create features array for storing an array fo GeoJSON features

```
var features = [];
```

The features array is something you might use for storing all the GeoJSON layers for sending back to a server.

### Listen for the `draw:created` event
```
map.on('draw:created', function (e) {
  drawnItems.addLayer(e.layer);
  var layers = drawnItems._layers;
  for (var key in layers) features.push(layers[key].toGeoJSON());
  console.log(drawnItems)
});
```

Every time a feature is drawn on to the map, the `draw:created` event will fire, and we'll store the layer in both `drawnItems` and `features`.

Instead of using `console.log()`, this is where you might send a request to your server to save the features.

### Listen for the `draw:edited` event
```
map.on('draw:edited', function (e) {
  var layers = drawnItems._layers;
  for (var key in layers) features.push(layers[key].toGeoJSON());
  console.log(drawnItems)
});
```

Every time a feature is edited on the map, the `draw:edited` event will fire, and we'll update the layer in both `drawnItems` and `features`.

Instead of using `console.log()`, this is where you might send a request to your server to save the features.

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