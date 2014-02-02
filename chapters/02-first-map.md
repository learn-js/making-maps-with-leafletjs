
# The simplest possible map you can make

## Get a CloudMade account and API key

For a number of examples in this book we'll use map tiles from CloudMade. Create an account at [cloudmade.com](http://cloudmade.com/) and get an API key to use in these examples.

## Create an index.html file

Here's the full index.html file we're using in this example. As you can see there's a minimal amount of work involved in creating a basic map. If you're new to some of these concepts keep reading, we'll go over this code in detail.

```
<!DOCTYPE html>
<html>
  <head>
    <title>Simple Leaflet Example</title>

    <link rel="stylesheet" href="http://cdn.leafletjs.com/leaflet-0.6.4/leaflet.css" />
    <!--[if lte IE 8]>
      <link rel="stylesheet" href="http://cdn.leafletjs.com/leaflet-0.6.4/leaflet.ie.css" />
    <![endif]-->

    <style>
    html, body { height: 100%; margin: 0px; }
    #map { height: 100%; }
    </style>
  </head>
  <body>
    <div id="map"></div>

    <script src="http://cdn.leafletjs.com/leaflet-0.6.4/leaflet.js"></script>

    <script>
    var attribution = 'Map data &copy; <a href="http://openstreetmap.org">OpenStreetMap</a> contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="http://cloudmade.com">CloudMade</a>';

    var map = L.map('map').setView([48.98337, -123.05855], 13);
    
    L.tileLayer('http://{s}.tile.cloudmade.com/!!!APIKEY!!!/997/256/{z}/{x}/{y}.png', {
      attribution: attribution,
      maxZoom: 18
    }).addTo(map);

    var marker = L.marker([48.98337, -123.05855]).addTo(map);
    var markerHtml = 'This place is weird';
    marker.bindPopup(markerHtml);
    </script>
  </body>
</html>
```

## The full index.html file explained in detail

### Get started

Give your html file the HTML5 doctype, open the `<html>` and `<head>` sections, and give your page a title.

```
<!DOCTYPE html>
<html>
  <head>
    <title>Simple Leaflet Example</title>
```

### Add Leaflet style

Include the Leaflet.js stylesheets from the leafletjs.com servers. The `<!--[if lte IE 8]>` tag is used to include the css styles that are specifically for versions of Internet Explorer less than or equal to IE 8.

```
<link rel="stylesheet" href="http://cdn.leafletjs.com/leaflet-0.7.2/leaflet.css" />
```

### Add your own style

Here we're adding the least amount of css it takes to get the map to fill the screen.

```
<style>
  html, body { height: 100%; margin: 0px; }
  #map { height: 100%; }
  </style>
</head>
```

### Create the map container.
This opens the `<body>` section. The `#map` div is where we'll put the map using javascript.

```
<body>
  <div id="map"></div>

```

### Leaflet javascript library
Include the Leaflet.js library that's hosted on the leafletjs.com servers using this script tag.

```
<script src="http://cdn.leafletjs.com/leaflet-0.7.2/leaflet.js"></script>
```

### Your map script
We use an opening `<script>` tag, then set a variable named attribution to a string that contains all the copyright info we need to convey about the map. If you use different tiles or data you'll want to change the attribution to reflect the resources you use in your map.

```
<script>
var attribution = 'Map data &copy; <a href="http://openstreetmap.org">OpenStreetMap</a> contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="http://cloudmade.com">CloudMade</a>';
```

### Initialize the map
We're creating a map object and assigning it to the map div. `L.map()` takes the id of an html element as an argument, so we're passing in `map` to target the div we made.

`.setView()` takes the latitude and longitude that we want the map to center on as an array, and an integer for the zoom level.

```
var map = L.map('map').setView([48.98337, -123.05855], 13);
```

### Add tiles to the map

`L.tileLayer()` is used to add tiles to the map. We set our attribution variable to the attribution option, and tell the layer to max out zooming at level 18.

Make sure to replace !!!APIKEY!!! with the API key you got from Cloudmade.

The `.addTo(map);` method is used to finally put the tile layer on the map.


```
L.tileLayer('http://{s}.tile.cloudmade.com/!!!APIKEY!!!/997/256/{z}/{x}/{y}.png', {
  attribution: attribution,
  maxZoom: 18
}).addTo(map);
```

## Add a marker

The `L.marker()` method just takes an array with the latitude and longitude of the place you'd like the map to be positioned.

Next we create a variable named `markerHtml` witih some text we want to show in a pop-up.

With `marker.bindPopup()` we add a pop-up window to the marker, and pass in the markerHtml variable to get that text to show up in the pop-up. You can put any kind of html in a pop-up, not just text.


```
var marker = L.marker([48.98337, -123.05855]).addTo(map);
var markerHtml = 'This place is weird';
marker.bindPopup(markerHtml);
</script>
```

### That's about it

Here we close the `<body>` and `<html>` tags. And that's it for this example.

```
  </body>
</html>
```

Nice! Now we can get that map running on a server somewhere!

## Publish the map on GitHub Pages

Let's host the map on GitHub  pages, an awesome free service from GitHub that we can use for simple html sites.

First, create an account on [github.com](http://github.com) if you haven't already.

Next, create a new repository.

Give your repository a name.

Now clone the project repository onto your computer:

```
git clone git@github.com:__YOUR-USERNAME__/__YOUR-PROJECT-NAME__.git
```

You can copy the git url to clone from the right-hand sidebar of your project repository.

After cloning the repository, cd into it and make some changes:

```
cd __YOUR-PROJECT-NAME__
nano index.html
```

Add the contents of our map project to index.html.

After you've added the content, add them to the repo and commit the changes:

```
git add .
git commit -m 'include a brief, clear message about the changes'
```

Put your changes on a branch named gh-pages:

```
bit checkout -b gh-pages
```

Now, push your changes back to GitHub:

```
git push origin gh-pages
```

### Troubleshooting

If GitHub Pages shows a 404 error at first, don't worry. It can take as much as 15 minutes before the GitHub server builds and starts serving your site. Be patient when you first launch the site. Later when you make updates the live site will usually reflect the changes more quickly.
