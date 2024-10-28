# PERCS
This repo is dedicated to enabling PERCS collaborators to easily access large datasets from the cloud using the geemap Python package, developped by Qiusheng Wu. 

<img width="688" alt="image" src="https://github.com/user-attachments/assets/89aed623-e40d-4ecf-b23c-5ad95a7fc907">

One of the challenges of sharing large spatial datsets is enabling them to be quickly visualised, while also easily shareable. This challenge is resolved by Google Earth Engine, and its ability to provide users the ability to upload their own raster and vector datasets. Google Earth Engine already plays host to relevant and important datasets such as Canada's annual frop inventory (AAFC) [link](https://code.earthengine.google.com/57b199c38650b51880cd884924fc62f4).

Several datasets have been uploaded to Earth Engine as part of the PERCS project, such as the City of Vancouver LiDAR landcover classification [link](https://code.earthengine.google.com/7adc53caba6f66b68c6d2ca5f8615409). A complete list of datasets uploaded so far can be found at [link](https://docs.google.com/spreadsheets/d/1_QopU1qFSOyDjQoQF8TCHs9Qjxr3jFTy-ueFWEWFIis/edit?usp=sharing). 

To download these datasets directly to your local machine, it is recommended to use the [geemap](https://docs.google.com/spreadsheets/d/1_QopU1qFSOyDjQoQF8TCHs9Qjxr3jFTy-ueFWEWFIis/edit?usp=sharing) Python package. It is possible to export images from Earth Engine in the default JavaScript API using the ['Exporting Images'](https://developers.google.com/earth-engine/guides/exporting_images) function, however it is necessary for these downloads to be processed using Google Drive which slows down the process. geemap offers a method for directly downloading images. 


