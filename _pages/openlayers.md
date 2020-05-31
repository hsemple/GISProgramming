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

    <!doctype html >
    <html lang = "en" >
    <head >
    <link rel = "stylesheet" href = "https://openlayers.org/en/v4.6.5/css/ol.css" type = "text/css" >
    <script src = "https://openlayers.org/en/v4.6.5/build/ol.js" >< /script> 
    </head>

    <style >
      .map {
        height: 600 px;
        width: 80 % ;
      } 
    </style> 

    <title > OpenLayers Example < /title>
    </head>


    <body >

    <h2 > My Map < /h2>

    <div id = "map" class = "map" >

    <script type = "text/javascript" >
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



### Extending the OpenLayers Application

In the previous unit, we created a simple web map that had only one layer, an Open Street Map base map. In this unit, we will add several of our own vector layers to the application. We will also add a couple of WMS layers from online sources.  Finally, we will add controls to the map to turn the layers on and off, and turn on the scale bar, and zoomslider.

 
The illustration below shows an OSM layer overlaid with a Michigan Geology layer. The code sample shows how it is accomplished.  Please make sure that you study the code in the Code Explanation below.



    <!doctype html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://openlayers.org/en/v4.6.5/css/ol.css" type="text/css">
    <script src="https://openlayers.org/en/v4.6.5/build/ol.js"></script>

    <title>OpenLayers Web App</title>

    <style>
    html, body{
    margin: 0px;
    padding: 0px;
    border: 0px;
    }

    #map {
    height:85%;
    width: 63%;
    margin: auto;
    }


    #container {
    margin: auto;
    width: 90%;
    }

    </style>

    </head>

    <body>

    <div id=“container”>

    <div id="map">

    <center><h1>  Interactive Web Map with Multiple Layers </h1> </center>

    </div>

    <script type="text/javascript">

    var osmlayer = new ol.layer.Tile({
    source: new ol.source.OSM()
    });


    // -- Load Michigan geology as a WMS layer --
    var arcGISTileLayer = new ol.layer.Tile({
      title: 'ArcGIS Tile',
      type: 'base',
      name: 'ArcGIS Map Tile',
      visible: false,
      source: new ol.source.TileArcGISRest({
        url: 'http://services.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer'})
      });
    arcGISTileLayer.setVisible(true);       


    // -- Load US geology layer as a WMS layer --
    var geology = new ol.layer.Tile({
        source: new ol.source.TileWMS({
          url: 'https://mrdata.usgs.gov/services/kb?',
        params:{'LAYERS': 'Geology', 'TILED': true},
        })
       });
      geology.setVisible(false);	  



    var us_faults = new ol.layer.Tile({
        source: new ol.source.TileWMS({
          url: 'https://mrdata.usgs.gov/services/sgmc?',
        params:{'LAYERS': 'State_Geologic_Map_Compilation', 'TILED': true},
        })
       });
      us_faults.setVisible(true); 	

    // -- Load shapefiles into Openlayers as geojson.  
    var parcels = new ol.layer.Vector({
    source: new ol.source.Vector({
    format: new ol.format.GeoJSON(),
    url: 'bedrock_geology.geojson',
    defaultProjection :'EPSG:4326', projection: 'EPSG:3857'
       })
    });

    var map = new ol.Map({
        target: 'map',
       renderer: 'canvas',
       layers: [osmlayer, geology, parcels],

    view: new ol.View({
        center: ol.proj.fromLonLat([-85.257728,43.649808]),
        zoom: 6
       })
    });

    </script>

    </div>
    </body>
    </html>


### Code Explanation

    <!Doctype html>
    <html lang="en">

The <!doctype > declaration is always the first line that appears on a html document.   It  is not an HTML tag. Rather, it indicates to the browser the version of HTML the page is written in.  In the example, !Doctype html means that the html version is html5.  Doctype for other versions are written differently.  For example, DocType for HTML Version 4.01 is written as:
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd"> 
You don’t need to edit the doctype. Just copy tit and paste it into your code.

  <html lang="en">

The lang attribute of the html tag declare the primary language of the web page. In this case, it is English.   

The Head Tag

<head>

The head tag contains information that the browser uses to effectively work with the web page. The <head> element can include a title for the web page, scripts, styles, meta information, etc.  Except for the title of the page, information within head tags is not visible to the person who is reading the web page.  


Meta Tag

<meta ……..">

Meta tags provide metadata about the web page to the browser. Metadata includes things like page description, keywords, author of the document, last modified, etc.  Each piece of information is referred to as an attribute. For example, <meta charset="UTF-8"> tells the browser that the letters, numbers and other symbols on the encoded in the UTF-8 character set. Other character set options include ASCII, ANSI, etc.  Metadata is always passed as name/value pairs, e.g.,
 <meta name="description" content="Free Web tutorials">


In the code, the line  <meta name="viewport" content="width=device-width, initial-scale=1"> tells the browser to scale to the viewport or viewing area of the device that is being used to view the web page, e.g., laptop, tablet, smart phone. 


The link tag
Link tag links to documents external to the web page.  

<link rel="stylesheet" href="http://openlayers.org/en/v3.18.2/css/ol.css" type="text/css">

In the code sample above, the link tag is linking to an external stylesheet, i.e., a document that contains CSS code.  This particular stylesheet is maintained by the OpenLayers’ organization.  The CSS code in the stylesheet is used by the browser to style the OpenLayers objects that appear on the web page, e.g., the location and size of zoom buttons, scale bar, etc.,


Script Tags
Script tags are used to embed Javascript and other scripts into the html of the web page.  In many cases, web designers have to refer to certain JavaScript classes, however, the classes themselves contain many lines of codes making it impractical to put the codes directly into the web page. To provide access to these classes, certain organizations maintain the classes on their website, and developers wishing to use the classes on their web page, simply reference the classes on the organization’s web site using a URL.  When your web page loads, your browser access the JavaScript libraries of classes using the provided URL and holds the classes in memory.  You can also download the JavaScript libraries and maintain them on your own website.   

The code below links to an OpenLayers JavaScript library that needs to be used on your web page. You do not have to edit this line. Just copy and paste it into the head of your html document. Notice that the last part of the code indicates that the script will hold JavaScript code in text format.
 
 <script src="http://openlayers.org/en/v3.18.2/build/ol.js" type="text/javascript"> </script>



The Title Tag
The title tag is part of the head of the web page. It contains the title of the page, which normally appears at the top center of the page.  You can edit the title to include whatever you want.
 
<title>OpenLayers 3 Web App</title>


Style Tag
The style tag encloses CSS codes, which controls the styling of the web page. You can put CSS tags directly into your web page using the style tags to enclose them.   This is called inline CSS. Alternatively, you can put the CSS codes in a separate page and use a link tag to reference the page. The separate CSS page is called an external sheet.

CSS consists of one or more blocks of codes each controlling the style of some element of the web page.  Each CSS block consists of one or more selectors and a declaration block contained within curly brackets. 

#map {
height:85%;
width: 63%;
margin: auto; 
}

In the CSS code block above, “map” is the selector. It refers to the html div element on the web page that has an id called “map”. The # symbol in front of map indicates that the CSS should be applied only to the specific element with id = “map”.  In some cases, you will see a dot in front of the selector. This indicates that the declaration applies to all instances of the map elements that appear on the page. 

Each declaration has property name and a value, separated by a colon, e.g., height:85%;  Notice the declaration ends with a semi-colon.   

The CSS below appears as part of the sample code for the OpenLayers application. Notice that the first code block has two selectors, html and body.  This means that both elements will have the same style. 

Actually <html> is the root element of the web page and <body> is a descendant contained within it. However, they both refer to the same physical space on the browser, hence they are styled simultaneously.  Not all web designers agree with this practice.


<style> 
html, body{
margin: 0px; 
padding: 0px; 
border: 0px; 
}


#map {
height:85%;
width: 63%;
margin: auto; 
}

#container {
margin: auto;
width: 90%;
}
</style>


The Body Tag

<body>
<div id=“container”>
<div id="map">

After the closing style tag, we encounter the body tag.  HTML tags that follow the body tag will create effects visible to the user.  Notice the two div tags, the container div and the map div.  

 The “container” tag sets up a div that will contain all elements in the body of the page. Most web pages have a container div tag that can be used to easily reposition all other elements on the web page.  The closing tag for container div is placed at the very bottom of the web page just before the closing body tag.  

The map div will be used to hold the OpenLayers map that will appear on your web page.  Notice that each div has an “id”. The “id” uniquely identifies the div in the html document.    

If you look at the code in the style tag, you will see entries for styling both the container and map divs.  For both divs, you will see code for setting the height and width of the divs.  


Header Tags
<center><h1> My First Interactive Web Map </h1> </center>
</div>

The html code above provides the main header of the web page. The <h1>   </h1> tags are used for creating headers while the center tag is used to center the header.



JavaScript in the Body of the Web Page
When building web pages, you can also put JavaScript within the body tags, but the JavaScript must be enclosed within script tags, e.g., <script>   </script> tags.  The script tags alert the browser that it is about to encounter JavaScript.   In OpenLayers applications, you will frequently encounter JavaScript within the body tags.  

In the code snippet below, the script tag is used to introduce a new set of JavaScript to the browser.  

<script type="text/javascript">
var osmlayer = new ol.layer.Tile({
   source: new ol.source.OSM()
});


All programming languages use variables for storing data values. In JavaScript, if the keyword “var” precedes a word, it means that a variable will be created with the name of the word that follows var.  In our code, a variable called “osmlayer” will be created to hold a new map layer object. 

The new map layer will be constructed with the code:  “new ol.layer.Tile ({... });”.  

The code “new ol.layer.Tile ({...});” is called a constructor as it creates a new instance of a tiled layer. Tiled layers are images organized by grids, which display at various zoom levels.  Notice that “new ol.layer.Tile” takes on a source parameter, which is the code enclosed in the curly brackets.  The source parameter indicates the data source of the new layer. In this case, the data source is a new instance of the tiled OpenLayers basemap, which is called OSM.

When adding new layers, we always follow the same format. First, we use the constructor code to create a variable with a name of our choice. Secondly, we indicate the data source of the new layer. Of course depending on the type of layer we are creating, the syntax may change slightly. Also the syntax for the data source of the layer will change slightly depending on the data source. Your task is to look up the syntax and use them correctly.
 

Creating  a second layer
The next few lines of code create a second layer, which has as its data source a web map service. Let’s look at the code:

// -- Load Michigan geology as a WMS layer --
var geology = new ol.layer.Tile({
source: new ol.source.TileWMS({
  url: 'http://mrdata.usgs.gov/services/mi?',
  params: {
   'LAYERS': 'Michigan_Lithology',
   'VERSION': '1.1.1',
  'FORMAT': 'image/png',
  'TILED': true
    }
  })
});


The first line is a comment statement.  Comments are used in all programming languages to explain the code, making it more readable. In JavaScript, we use // when it is just a single line comment.

As in the previous example, the initial part of the constructor statement for this layer is “new ol.layer.Tile”.  The constructor has a source parameter, which indicates that the data source is a new instance of a WMS Tile.  These WMS Tiles have their own properties or parameters, which must be indicated.  In this case, we indicate the indicate the URL of the WMS, the version of the web map service, and format or the image that will be served, etc.



Creating the map and adding the layers

Now that the layers have been created, we need to create a map object and then add the layers to the map object. The code below creates the map object.

var map = new ol.Map({
    target: 'map',
    renderer: 'canvas',
    layers: [osmlayer, geology],

The constructor code “new ol.Map({... });” creates a new instance of an OpenLayer map and assigns it to a variable named map.  You can see that the constructor has several parameters, including target, renderer, and layers. So, to create the map, the OpenLayer Map class needs to be supplied with a target, which is the div that will hold the map, a renderer, which is the engine that will be used to draw the map, and a list of the layers that the map will hold.

OpenLayers’ default renderer engine is “canvas”.  Other renderers include “DOM” and “WebGL”.  The WebGL renderer is used to render 3D images. 

Note that “layers: [osmlayer, geology]” contains the names of the map layers you created earlier.  In some OpenLayers codes, you will see the layers you created earlier, being created within the layers’ parameters.


The View object
The Map object also takes a “View” object as a parameter. The View object is used for visualizing the map.  The view object is also responsible for centering the map on a particular coordinate pair. You can change the coordinate pair to center the map on a location of your choice. The view object also controls the zoom level. You can change the zoom level of the map to a zoom level of your choice.

view: new ol.View({
    center: ol.proj.fromLonLat([-85.257728,43.649808]), 
    zoom: 6
   }) 
});



Closing Tags

The tags below are closing tags for the JavaScript tag, the container div, the body tag, and the html tag.

</script>
</div>
</body>
</html>



Adding your own layers to OpenLayers
To add your water utility layers to OpenLayers 3, first you display the layers in ArcMap, then open ArcToolBox and export the layers to geojson format. GeoJSON is a popular format for handling geographic data on the web.  Many web mapping programs can parse it, including OpenLayers and Google Maps API.

I use QGIS to export shapefiles to GeoJSON format.   Once the files are converted to geojson, you can upload them to people.emich.edu. You will also reference them in your code, as shown below:

       var roads = new ol.layer.Vector({
        source: new ol.source.Vector({ 
        format: new ol.format.GeoJSON(),  
	 url: 'roads.geojson',  	
        });	

Notice that the geojson is being declared as a Vector, and not as a Tile. The data source is vector. The URL is the URL of the geojson layer. In this case, because the geojson is in he same folder with the web page, we simply write the name of the file and along with its 

