# PERCS
This repo is dedicated to enabling PERCS collaborators to easily access large datasets from the cloud using the geemap Python package, developped by Qiusheng Wu. 

<img width="688" alt="image" src="https://github.com/user-attachments/assets/89aed623-e40d-4ecf-b23c-5ad95a7fc907">

One of the challenges of sharing large spatial datsets is enabling them to be quickly visualised, while also easily shareable. This challenge is resolved by Google Earth Engine, and its ability to provide users the ability to upload their own raster and vector datasets. Google Earth Engine already plays host to relevant and important datasets such as Canada's annual frop inventory (AAFC) [link](https://code.earthengine.google.com/57b199c38650b51880cd884924fc62f4).

Several datasets have been uploaded to Earth Engine as part of the PERCS project, such as the City of Vancouver LiDAR landcover classification [link](https://code.earthengine.google.com/7adc53caba6f66b68c6d2ca5f8615409). A complete list of datasets uploaded so far can be found at [link](https://docs.google.com/spreadsheets/d/1_QopU1qFSOyDjQoQF8TCHs9Qjxr3jFTy-ueFWEWFIis/edit?usp=sharing). 

To download these datasets directly to your local machine, it is recommended to use the [geemap](https://docs.google.com/spreadsheets/d/1_QopU1qFSOyDjQoQF8TCHs9Qjxr3jFTy-ueFWEWFIis/edit?usp=sharing) Python package. It is possible to export images from Earth Engine in the default JavaScript API using the ['Exporting Images'](https://developers.google.com/earth-engine/guides/exporting_images) function, however it is necessary for these downloads to be processed using Google Drive which slows down the process. geemap offers a method for directly downloading images. 

To use geemap, begin by installing the geemap package using the [PyPi](https://pypi.org/project/geemap) or [Conda forge](https://anaconda.org/conda-forge/geemap) method. To connect geemap with Earth Engine, it is also necessary to install the [Earth Engine Python API](https://developers.google.com/earth-engine/guides/python_install). One you have installed the packages and loaded them as librairies, connect to Earth Engine by running:

```
Map = geemap.Map()
Map
```
You will be prompted to grant permission to your Earth Engine account. Once you have done this, enter the code that is provided into your IDE, and proceed. 

For this tutorial, we will simmulate downloading landcover data from the Vancouver landcover classification to our local machine. To download an image, we have to specify a spatial extent over which we are downloading the image. We will download a small area in Richmond, denoted by the following geojson:
```
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {},
      "geometry": {
        "coordinates": [
          [
            [
              -123.0685876163603,
              49.197239615150295
            ],
            [
              -123.0685876163603,
              49.170427720086934
            ],
            [
              -123.02537876329515,
              49.170427720086934
            ],
            [
              -123.02537876329515,
              49.197239615150295
            ],
            [
              -123.0685876163603,
              49.197239615150295
            ]
          ]
        ],
        "type": "Polygon"
      },
      "id": 0
    }
  ]
}
```
You can load the above text in [geojson.io](https://geojson.io/#map=12.79/49.17904/-123.04251) to visualise the extent. 

You can load this polygon into earth engine using:
```
aoi = ee.Geometry.Polygon([
            [
              -123.0685876163603,
              49.197239615150295
            ],
            [
              -123.0685876163603,
              49.170427720086934
            ],
            [
              -123.02537876329515,
              49.170427720086934
            ],
            [
              -123.02537876329515,
              49.197239615150295
            ],
            [
              -123.0685876163603,
              49.197239615150295
            ]])
Map.addLayer(aoi, {}, "AOI")
```
This will create the area extent that we can use to download the imagery, as well visualise it. The middle parameter '{}' can be used to customise symbology. 

We can then proceed to load in our landcover data:
```
data = ee.Image('projects/ee-jeremyallen248/assets/PERCS/LCC2020')
```
We can visualise the different classes by creating a custom palette:
```
LCC2020_palette = [
'ffffff', 
'808080', 
'c0c0c0', 
'f0f0f0', 
'ffcc66', 
'006400', 
'00ff00', 
'8b4513', 
'7cfc00', 
'32cd32', 
'8b0000', 
'0000ff', 
'000000', 
'ffffff', 
'556b2f', 
'2e8b57'  
]
Map.addLayer(data,
{"min": 0, "max": 16, "palette": LCC2020_palette},
'LCC2020 classification')
Map.centerObject(data, 10)
```
To download the portion of the image corresponding to our AOI, we can clip the data our AOI using:
```
image = data.clip(aoi)
```

We can then export the clipped data ('image') by specifying our export parameters ('dir'), and using the geemap.ee_export_image function. 
```
cwd = os.getcwd()
dir = os.path.join(cwd, 'export.tif')
geemap.ee_export_image(
    image, filename=dir, scale=5, region=aoi, file_per_band=False
)
```
Your dowloaded image should now be located in your specified output directory. Congrats!




