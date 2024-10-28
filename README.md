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

