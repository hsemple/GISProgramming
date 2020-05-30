---
permalink: /open_source/
title: "Open Source Python GIS"
sidebar:
  nav: "docs" 
---



Once you have mastered basic concepts in Python, you are ready to take on working with the GIS libraries. Here is a list of some of the popular open source libraries used in the geospatial community. The list is in no paraticualr order. Selection of particular libraries depend on the task that needs to be carried out.   


* [Geopandas.](https://geopandas.org/#description) Great tool for easy reading and display of vector data.
* [GDAL/OGR.](https://gdal.org/) - A package used by many GIS applications for raster and vector processing. 
* [Rasterio.](https://rasterio.readthedocs.io/en/latest/) Simplifies working with raster datasets procssing
* [PyProj.0](https://pypi.org/project/pyproj/)  Widely used tool for cartographic transformations and geodetic computations
* [Cartopy.](https://scitools.org.uk/cartopy/docs/latest/index.html) Cartography library
* [Fiona.](https://pypi.org/project/Fiona/) Reads and write spatial data. 
* [Shapely.](https://pypi.org/project/Shapely/) Great for reading and writing spatial data.
* [GEOS.](https://pypi.org/project/geos/). Library for creating Google Earth overlays of tiled maps.
* [pyshp.](https://pypi.org/project/pyshp/) Reads and writes ESRI shapefiles
* [GeoDjango.](https://docs.djangoproject.com/en/3.0/ref/contrib/gis/) Used for building geospatial web applications 
* [EarthPy.](https://pypi.org/project/earthpy/) Simplifies processing of raster and vector data.
* [GeoPy.](https://geopy.readthedocs.io/en/latest/) Geocoding library
* [PySAL.](https://pysal.org/) Used for spatial statistical analysis. 
* [RSGISLib.](https://www.rsgislib.org/index.html#python-documentation) Remote Sensing Library
* [Geoplot.](https://geopandas.org/gallery/plotting_with_geoplot.html). Used for plotting maps and several GIS operations.

<br>
Below, you will find links and code snippets to common tasks in GIS that are made possible using these libraries.  

## Short Course and Tutorials
* [Short Course in manipulating Python Geospatial Libraries](https://automating-gis-processes.github.io/CSC18/lessons/L1/Intro-Python-GIS.html)
* [Intro to Coordinate Reference Systems in Python](https://www.earthdatascience.org/courses/use-data-open-source-python/intro-vector-data-python/spatial-data-vector-shapefiles/intro-to-coordinate-reference-systems-python/)
* [Plotting Coordinates](https://idlecoding.com/transverse-mercator-with-python/)
* [Table Joins](https://www.dataquest.io/blog/pandas-concatenation-tutorial/)
* [GIS data access and manipulation with Python](https://www.e-education.psu.edu/geog485/node/253) 

<br>

## Code Snippets

Displaying a Shapefile's Attribute Table and Geometry Using Geopandas

    import matplotlib.pyplot as plt
    import geopandas as gpd

    file = ".../Michigan_Counties.shp"
    df = gpd.read_file(file)

    #Display attribute table
    print (df)
 
    #Display shapefile
    df.plot()

    #or
    #df.plot(cmap='Set2', figsize=(10, 10));
    plt.show()
<br>
 

Plotting a Thematic Map

    import pandas as pd
    import geopandas
    import matplotlib.pyplot as plt
    gdf = geopandas.read_file("/Users/.../Michigan.shp")

    #Display the shapefile
    f, ax = plt.subplots(1, figsize=(10, 13))

    gdf.plot(ax = ax, column= 'MOBILEHOME', cmap='OrRd' , scheme='fisher_jenks', legend=True, edgecolor='black')

    ax.set_title("Moble Homes, Michigan", fontdict={'fontsize': '20', 'fontweight' : '3'})

    plt.show()

    #Save the map
    fig.savefig("/Users/.../map_export.png", dpi=300)
<br>
 

Plotting a Shapefile Using PyShp
The geopandas code is preferred over the code below but I include here for the insights it provides into the structure of shapefiles, i.e., parts and points, and how these are accessed and manipulated.  
  
    import shapefile as shp
    import matplotlib.pyplot as plt

    sf = shp.Reader("C:/Users/.../Michigan.shp")

    plt.figure(figsize = (10,8))

    # loop through each record in the shaperecords collection 
    for each_rec in sf.shapeRecords():
    for i in range(len(each_rec.shape.parts)): #Det the # of parts in each shape to loop through
         #Get the starting and ending values for each part
        i_start = each_rec.shape.parts[i]
        if i==len(each_rec.shape.parts)-1:
            i_end = len(each_rec.shape.points)
        else:
            i_end = each_rec.shape.parts[i+1]

        #Get the X,Y coordinates of the points in each part
        x = [i[0] for i in each_rec.shape.points[i_start:i_end]]
        y = [i[1] for i in each_rec.shape.points[i_start:i_end]]
        plt.plot(x,y, color = "green")
        
    plt.show()
    
 <br>
 

Displaying a Raster Using GDAL
 
    import numpy as np
    import gdal
    import matplotlib.pyplot as plt

    #Open raster and read number of rows, columns and bands
    ds = gdal.Open("/Users/.../TestDEM.tif")

    band1 = ds.GetRasterBand(1)

    raster_array = band1.ReadAsArray()
    plt.imshow(raster_array)
    plt.show()
  
 <br>
 

Displaying a Three-band Raster with GDAL

    import numpy as np
    from osgeo import gdal
    import matplotlib.pyplot as plt

    aerial = gdal.Open("/Users/.../aerial2.TIF")
    bnd1 = aerial.GetRasterBand(1)
    bnd2 = aerial.GetRasterBand(2)
    bnd3 = aerial.GetRasterBand(3)


    #Now turn each band into a ndarray:
    img1 = bnd1.ReadAsArray()
    img2 = bnd2.ReadAsArray()
    img3 = bnd3.ReadAsArray()    


    #Then stack them to have a 3 band image
    img = np.dstack((img1,img2,img3))

    plt.imshow(img)    
    plt.show()
 
 <br>
  
Displaying a Three-band Raster with  Rasterio

Rasterio is a popular open source Python library used for viewing and manipulating rasters.  Rasterio utilizes the gdal library to display rasters. With rasterio, viewing a raster can be done with just a few lines of code, like the example below. 

Rasterio has a show( ) method for displaying rasters. However, the library also uses pyplot’s imshow method to display the data.

 

    import rasterio
    from matplotlib import pyplot

    src = rasterio.open("C:/Users../N47E010.hgt")
    src_array = src.read(1)

    fig, ax = pyplot.subplots(1, figsize=(12, 12))
    img = ax.imshow(src_array) # Get the plot renderer object.

    fig.colorbar(img, ax=ax) #Associate the figure object with plot renderer and axes objects.
    ax.set_aspect('auto') #Let the axes object set the length of the colobar. 

    pyplot.show()
    
  

<br>
[Displaying True color and False color imagery with Rasterio](https://automating-gis-processes.github.io/CSC/notebooks/L5/plotting-raster.html)

