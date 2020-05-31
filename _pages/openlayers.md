---
permalink: /openlayers/
title: "Introduction to Open Layers"
sidebar:
  nav: "docs"
---


OpenLayers is a JavaScript library that contain functions for creating interactive web maps.  Fortunately, the code samples can be understood with moderate effort.  Learn more about Open Layers by visiting their [homepage.)(https://openlayers.org/)



###Build a Basic Open Layers Web Mapping Application

1. First, take a look at this [site](https://medium.com/attentive-ai/working-with-openlayers-4-part-1-creating-the-first-application-9ab27bbd7a62) to see how a basic web mapping application is built using Open Layers.


2. Copy the code, save it as a html file, then run it on your local computer.  If any error arises, trouble shoot it.Once the code runs successfully, study the code and try to understand what each line does. Explanations are provided via links.

 
#### Code to Create a Simple Open Layers Map

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

You can view the code explanation [here](https://openlayers.org/en/latest/doc/quickstart.html).  
