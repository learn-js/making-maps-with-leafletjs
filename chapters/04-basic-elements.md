# Basic elements of a Leaflet.js map
There are a few basic elements that you’ll use on regular basis for drawing on a map. Here’s a look at how to make each one of those:

## UI Layers

### popups

To get started learning popups, let’s make the map show a popup with the latitude and longitude of place we click on the map.

To create a popup, use the `L.popup()` method:


```
var popup = L.popup();

```

Next we need to listen for the `click` event on the map:


```
map.on('click', onClick);

```

We’ve passed a function named `onClick` to the event listener, so let’s create that function:


```
function onClick(e){
    popup
    .setLatLng(e.latlng)
    .setContent("You clicked the map at " + e.latlng.toString())
    .openOn(map);
}

```

### markers

To create a marker, use the `L.marker()` method:


```
var marker = L.marker([47.63, -122.32]);
marker.addTo(map);

```

The above code will add a marker to the center of your map, as we're using the some lat/long for this marker as the map view.

Let's add a popup to that marker.

First, set some html content to a variable:


```
var markerHtml = 'this is a marker. pretty great, right?';

```

Next, bind a popup to the marker:


```
marker.bindPopup(markerHtml);

```

Now when you click on the marker, the popup will show up the the html you specified. 

To make the popup open up by default, try this:


```
marker.bindPopup(popupContent).openPopup();

```

Now when you look at your map again, you'll see that the popup is open by default.

## Vector layors

Vectory layers are the things you can draw on top of the map. Some of the basic types: lines, rectangles, circles, and polygons. In this section we'll make one of each of those vector layer types.

### Lines

We'll use the `L.polyline` method for drawing lines on the map. it takes an array of lat/long coordinates, and an [options object](http://leafletjs.com/reference.html#polyline-options). This method extends the base `L.Path` method, so you can also use any [path options](http://leafletjs.com/reference.html#path-options).

Here's an example:


```
var polylinePath = [
  [47.607204675859045, -122.3298454284668],
  [47.60182268729636, -122.32521057128906],
  [47.60095457276622, -122.32349395751952],
  [47.5998260023411, -122.32237815856934],
  [47.59842248977284, -122.32124090194701],
  [47.59655590441905, -122.32023239135741],
  [47.59175167310035, -122.32126235961914],
  [47.588278460128734, -122.32057571411133],
  [47.58329978624572, -122.31997489929199],
  [47.579478622338286, -122.3192024230957],
  [47.57756793579513, -122.3196315765381]
];

var polyline = L.polyline(polylinePath);
polyline.addTo(map);

```

This is a line along part of the I-5 highway in the Seattle area. Try it out in your map. Try changing the path to see what lines you can make. Remember that we made that popup that shows the lat/long when you click on the map. Use that to come up with coordinates that you want to place in your lat/lng array.

### Rectangles

Creating a rectangle is very similar to creating a polyline, but takes two coordinates that represent two corners of the rectangle.

Here's an example that loosely outlines Lake Union in Seattle:


```
var rectBounds = [[47.64614, -122.34555], [47.6274, -122.32839]];

var rectangle = L.rectangle(rectBounds);
rectangle.addTo(map);

```

### Circles

When creating a circle, we use the `L.circle` method and give one lat/lng coordinate as the center point, followed by the radius.

Here's an example with a circle centered on the Seattle neighborhood Fremont (also known as the center of the universe):


```
var circle = L.circle([47.65136, -122.35087], 300)
circle.addTo(map);

```

### Polygons

A polygon can be any arbitrary shape, good for outlining buildings, parks, etc. To create a polygon, we use `L.polygon`.

Here’s an example that roughly outlines the downtown Seattle area:


```
L.polygon([
  [47.61311, -122.34967],
  [47.61594, -122.33156],
  [47.60466, -122.32169],
  [47.60211, -122.33551]
]).addTo(map);

```

### What’s next
This gets you started with leaflet.js. You’ve learned about getting a map to show up on a page and drawing basic shapes. Just by composing shapes and popup markers in this way you can make a useful map very easily.
