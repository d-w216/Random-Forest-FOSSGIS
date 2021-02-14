# FOSSGIS-Random-forest
Comparison of two Supervised Classification Methods (Grass GIS: r.learn.ml/ SAGA GIS: ViGrA) and Comparison of two (temporal) different datasets (Heidelberg OpenStreetMap data 2015/2020; Sentinel data 2015/2020).


<h2>Preparation</h2>

*For successful execution, the specified versions of the programs and all packages must be installed!*


If not installed yet:

Download Saga Gis (latest version) from the Sourceforge site: https://sourceforge.net/projects/saga-gis/.

Download Grass Gis version 7.8.5 via OSGEO: https://trac.osgeo.org/osgeo4w/ (Since this process will install the necessary additional programming language in the appropriate form). 

Download QGIS version 4.16.3 via OSGEO: https://trac.osgeo.org/osgeo4w/

- Run the installer and select “Advanced Installation”. Click through the steps and keep the default values

- Stop at “Choose packages”

- Desktop; grass: GRASS GIS version (7.8.5-1)

__In Grass Gis__

- Create location with EPSG:32632

__Execute in Grass Gis Console:__

- easy_install pip (this way to install pip install only works if Grass Gis was downloaded via OSGEO)

- pip install jupyter

- pip install scikit-learn

- pip install pandas


<h2>Data acquisition</h2>

Geojson   - run batch [*osmQueries_2015*] script in Grass Shell. 

Geojson   - run batch [*osmQueries_2020*] script in Grass Shell. 

GeoTIff - Download raster data from *Heibox*.  

Heibox: 
- Sentinel-2 29.08.2015: https://heibox.uni-heidelberg.de/f/63b60d95b59341b6a99f/?dl=1
- Sentinel-2 23.07.2020: https://heibox.uni-heidelberg.de/f/7243e318528d47218184/?dl=1

<h2>Data preprocessing/Supervised Classification</h2>

<h3>Grass Gis</h3>

In Grass Gis Console execute:

- jupyter notebook

Open in browser

Navigate through folders to: randomForestGRASS.ipynb

Double click on the script

Adjust __wd_path__ and specify path to folder

__Note:__ Do not change the folder structure!

__Note:__ According to the targeted analysis (year) change the *year* variable.

__Note:__ The process will take a few minutes. Depending on your hardware, you might want to adjust some parameters: 
- r.random_() -> try to lower or increase the parameter "npoints" (number of points to be extracted)
- r.learn_ml_() -> try to lower or increase the parameter "n_estimator" (number of trees)

[*Kernel /Restart & Run All*]

[*Restart and Run All Cells*]

<h3>SAGA GIS</h3>

__In QGIS:__

In the Processing Toolbox:

- Click on [*Models*]

- Click on [*Opening existing Models*] 

- Open: model.model3

- Click on [*Run Model*] (F5) -> generate temporary layers

- [*Export*] (Points, clipped Raster) Results as Geojson and SAGA GIS Binary Grid 
 
Exporting in QGIS:

- Right mouse click on data in Layer view  

- Click [*Export*] 

- [*Save as*] Geojson/SAGA GIS Binary Grid 

__In Saga GIS:__

- Load the SAGA GIS Binary Grids and the Geojson result per drag and drop

- In [*Geoprocessing*]  

- Click on [*Find and run Tool*] 

- Search for [*Random Forest Classification (ViGrA)*]

In Random Forest Classification (ViGrA):

- Set Grid System to available option

- Load all SAGA GIS Binary Grids in Features

- Load Geojson in Training Areas

- Set Label Field to class

- Select [*Use Label as Identifier*] 

- Tree Count 100

- Click [*Okay*]

Export the Result 

- Right mouse click on data in Data view  

- Click [*Export*] 

- [*Save as*] Geotiff 





