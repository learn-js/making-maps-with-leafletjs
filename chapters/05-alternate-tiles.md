# Using alternate tilesets

The Leaflet tutorials all use CloudMade tiles for the examples. Those tiles look great, but it's common to want a little more control over the style of the map.

For the examples in this chapter we'll build on the example created in chapter 3.

### In this chapter we'll take a look at these options for Leaflet tiles:
- Using [Stamen tiles](http://maps.stamen.com)
- Using [Mapbox tiles](https://www.mapbox.com)
- Using alternate [CloudMade tiles](http://maps.cloudmade.com/editor)

But first we'll do a quick refresher on the file structure to make sure you have everything set up.

## Get set up

If you already created the example project from chapter 3 and have it ready to go, cd into that directory and skip or skim this set up section. Otherwise, if you need to recreate the project or feel like you could benefit from going through the code again, check out this section before moving to the alternate tilesets.

Here is what your full index.html file should look like:

```
<!doctype html>
<html>
<head>
  <title>leaflet example</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="node_modules/leaflet/dist/leaflet.css">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div id="map"></div>
  <script src="bundle.js"></script>
</body>
</html>
```

Here is what should be in your style.css file:

```
#map {
  height: 300px;
}
```

And this is what your app.js file should look like:

```
// require leaflet.js
var L = require('leaflet');
 
// specify the path to the leaflet images folder
L.Icon.Default.imagePath = 'node_modules/leaflet/dist/images/';
 
// initialize the map
var map = L.map('map', {
  scrollWheelZoom: false
});
 
// set the position and zoom level of the map
map.setView([47.63, -122.32], 11);
 
// set an attribution string
var attribution = 'Map data &copy; <a href="http://openstreetmap.org">OpenStreetMap</a> contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="http://cloudmade.com">CloudMade</a>';
 
// set the tiles the map will use
var tiles = 'http://{s}.tile.cloudmade.com/!!! YOUR API KEY !!!/997/256/{z}/{x}/{y}.png';
 
// create a tileLayer with the tiles, attribution
var layer = new L.StamenTileLayer('watercolor');
 
// add the tile layer to the map
layer.addTo(map);
```

If you lost your CloudMade API key, you can find it by logging in to [cloudmade.com](http://cloudmade.com), or you can also make a new API key there.

The contents of your package.json file should be very similar to this:

```
{
  "name": "leaflet-basics",
  "description": "introduction to using leaflet with browserify",
  "version": "0.0.0",
  "main": "app.js",
  "scripts": {
    "start": "beefy index.js:bundle.js --live",
    "bundle": "browserify index.js -o bundle.js"
  },
  "author": "",
  "license": "MIT",
  "dependencies": {
    "leaflet": "~0.7.2"
  },
  "devDependencies": {
    "beefy": "~0.7.1",
    "browserify": "~3.24.10"
  }
}
```

The important parts of the package.json file are the `scripts`, `dependencies`, and `devDependencies` sections. Make sure that at least those fields are intact in your package.json file.

If you don't have a node_modules folder in your project directory, run this command to install the project dependencies:

```
npm install
```

Now we should be ready!

## Install the leaflet-providers module

In order to use these alternate tile providers, we're going to use a module named [leaflet-providers](https://github.com/leaflet-extras/leaflet-providers).

With this module we can use tile layers from:

- Mapbox
- CloudMade
- Stamen
- OpenStreetMap
- MapQuestOpen
- Esri
- OpenWeatherMap
- Nokia

Mapbox, CloudMade, and Nokia require registration. Learn more at the [leaflet-providers GitHub page](https://github.com/leaflet-extras/leaflet-providers).

### Install leaflet-providers

```
npm install --save leaflet-providers
```

## Using Stamen tiles

Stamen is a design company that makes all kinds of beautiful things, including maps.

Take a look at their [Toner](http://maps.stamen.com/toner/#14/37.7777/-122.4073), [Terrain](http://maps.stamen.com/terrain/#14/37.7777/-122.4073), and [Watercolor](http://maps.stamen.com/watercolor/#14/37.7777/-122.4073) map tiles. They're stunning. See more at [maps.stamen.com](http://maps.stamen.com).

For this example, we'll use the Watercolor tileset.

To use the Watercolor tiles, require the `leaflet-providers` module in your app.js file:

```
require('leaflet-providers');
```

> Note that we're not setting this module to a variable like with other modules. It's because the leaflet-providers module is a plugin to Leaflet that adds a `provider()` method to `L.tileLayer`. By requiring the module without setting it to a variable the module can modify variables in the global scope when required. 


Next, set the layer variable to the new Stamen Watercolor tiles:

```
var layer = L.tileLayer.provider('Stamen.Watercolor').addTo(map);
```

Your full app.js file should now look like this:

```
// require leaflet.js
var L = require('leaflet');
require('leaflet-providers');

// specify the path to the leaflet images folder
L.Icon.Default.imagePath = 'node_modules/leaflet/dist/images/';
 
// initialize the map
var map = L.map('map', {
  scrollWheelZoom: false
});
 
// set the position and zoom level of the map
map.setView([47.63, -122.32], 11);

// create a tileLayer with the tiles, attribution
var layer = L.tileLayer.provider('Stamen.Watercolor').addTo(map);
 
// add the tile layer to the map
layer.addTo(map);
```
Note that we removed these lines:

``` 
// set an attribution string
var attribution = 'Map data &copy; <a href="http://openstreetmap.org">OpenStreetMap</a> contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="http://cloudmade.com">CloudMade</a>';
 
// set the tiles the map will use
var tiles = 'http://{s}.tile.cloudmade.com/!!! YOUR API KEY !!!/997/256/{z}/{x}/{y}.png';
```

They are unnecessary because the `L.tileLayer.provider('Stamen.Watercolor')` method takes care of the tiles url and attribution string for us.

### Check out your Watercolor map!

If you run `npm start` and go to http://localhost:9966, you should see an awesome watercolor map! Looks good, right?


## Using Mapbox tiles

You'll want to use [Mapbox tiles](https://www.mapbox.com). They are beautiful.

```
L.tileLayer.provider('MapBox.YourUsername.MapID').addTo(map);
```

Here's an example map with new styles I made in about 5 minutes using the simple editor on mapbox.com:

```
var layer = L.tileLayer.provider('MapBox.sethvincent.h60m4iih');
```

Once you add in the above line to replace the CloudMade tileset, your app.js file should look like this:

```
// require leaflet.js
var L = require('leaflet');
require('leaflet-providers');

// specify the path to the leaflet images folder
L.Icon.Default.imagePath = 'node_modules/leaflet/dist/images/';
 
// initialize the map
var map = L.map('map', {
  scrollWheelZoom: false
});
 
// set the position and zoom level of the map
map.setView([47.63, -122.32], 11);

// create a tileLayer with the tiles, attribution
var layer = L.tileLayer.provider('MapBox.sethvincent.h60m4iih');
 
// add the tile layer to the map
layer.addTo(map);
```

When you make a map at mapbox.com, look for the map ID in your projects list after you log in, or, if you're editing a map, the ID is found be clicking the gear icon – it'll be at the top of that menu.

In an upcoming chapter we'll work on an example where you'll design completely custom tiles using Mapbox's desktop app [TileMill](https://www.mapbox.com/tilemill/), upload the tiles to the Mapbox servers, and use the tiles in a Leaflet map!

## Using alternate CloudMade tiles

Using alternate tiles from CloudMade is very similar using the leaflet-providers module. The main differences are that you must specify an `apiKey` and `styleID`.

Here's an example:

```
var layer = L.tileLayer.provider('CloudMade', {
  apiKey: '!!! YOUR API KEY !!!',
  styleID: '2172'
});
```

The `styleID` of `2172` is for a fairly pleasant tile theme named Orange Yellow.

To find and create new styles for CloudMade tiles go to [maps.cloudmade.com/editor](http://maps.cloudmade.com/editor).

You'll see the `styleID` in the bottom right corner of each thumbnail.

The full app.js file when using the CloudMade provider should look something like this:

```
// require leaflet.js
var L = require('leaflet');
require('leaflet-providers');

// specify the path to the leaflet images folder
L.Icon.Default.imagePath = 'node_modules/leaflet/dist/images/';
 
// initialize the map
var map = L.map('map', {
  scrollWheelZoom: false
});
 
// set the position and zoom level of the map
map.setView([47.63, -122.32], 11);

// create a tileLayer with the tiles, attribution
var layer = L.tileLayer.provider('CloudMade', {
  apiKey: '!!! YOUR API KEY !!!',
  styleID: '2172'
});
 
// add the tile layer to the map
layer.addTo(map);
```


### Other tilesets

Most likely these three tile providers will provide tiles that fit your needs, but if you're looking for more, check out the leaflet-providers repository on GitHub: [github.com/leaflet-extras/leaflet-providers](https://github.com/leaflet-extras/leaflet-providers).