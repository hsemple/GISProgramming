---
permalink: /openlayers/
title: "Introduction to Open Layers"
sidebar:
  nav: "docs"
---


OpenLayers is a JavaScript library that contain functions for creating interactive web maps.  Fortunately, the code samples can be understood with moderate effort.  Learn more about Open Layers by visiting their homepage (Links to an external site.).   You can also take a look at this site  (Links to an external site.)to see how a basic web mapping application is built using Open Layers.


###Build a Basic Open Layers Web Mapping Application

Follow the OpenLayers samples code belowand build your first interactive web maps. Once the code runs, study the code and try to understand what each line does. Explanations are provided via links.

 

 

Example 1

This is a simple interactive map that consists of just the base layer.  The base layer comes from Open Street Map and is in the form of a web service, which is a popular way of presenting data via web applications. ArcGIS Server may be used to convert layers into web services.

 

Copy the code, save it as a html file, then run it on your local computer.  If any error arises, trouble shoot it.  After the code runs successfully, you can upload it to people.emich.edu.


 

Code

<!doctype html>
<html lang="en">
<head>
<link rel="stylesheet" href="https://openlayers.org/en/v4.6.5/css/ol.css" type="text/css">
<script src="https://openlayers.org/en/v4.6.5/build/ol.js"></script>
</head>

<style>
.map {
height: 600px;
width: 80%;
}
</style>
<title>OpenLayers Example</title>
</head>

<body>
<h2>My Map</h2>

<div id="map" class="map">

<script type="text/javascript">
var map = new ol.Map({
target: 'map',
layers: [
new ol.layer.Tile({
source: new ol.source.OSM()
})
],
view: new ol.View({
center: ol.proj.fromLonLat([-66.879714, 10.474557]),
zoom: 4
})
});
</script>
</div>
</body>
</html>

You can also view the code explanation here.  nks to an external site.)Links to an external site.
