# Geochemical soil analyses using Google Earth Engine
## 1 - Introduction
This paper explore a possibility to analyses geochemistry dataset of soil samples using [google earth engine](https://earthengine.google.com/). The google earth engine is a plataform that you can combine satellite images, javascript algorithms and real world applications, in your code plataform make it's possible up load any file. SO this exemple I will use a geochemistry dataset of soil samples avaiable free on the [Geological Survey of Brazil](https://geosgb.sgb.gov.br/geosgb/downloads.html), and you can do the same download, see the figure 1 to find easelly the Bacia_do_Rio_Doce.csv file.


![figure 1](image/download.png) 

Figure 1 - Download page of Geological Survey of Brazil. Choose Planilha (csv) - Bacia do Rio Doce file.

## 2 - Objectives
This dataset has chemical analyses of different elements, like iron and cupper and other more, first we gonna plot that samples on Landsat 8 image, than we analyse the values of gold and cupper using data view technices avaiable on the plataform. The last part we gonna calculate index for cupper, the gossan index and create a Kringing interpolation to iron an cupper.

## 3 - The Dataset
The dataset represent a collection of samples in a hidrographic Basin, in case Doce Basin, locate in Minas Gerais Province, Southeast of Brazil. It's has values of latitude and longitude, with the name of the basin  and the chemical values of each element analysed for sample. 

![figure 2](image/dataset.png) 
Figure 2 - Dataset Table. 


For this work is necessary use a SHP file (ESRI) that contains the geometry of all Brazilian Limits and the columns names and codes. We gonna extract the geometry of Doce Basin using this file. This file is avaiable [here](https://metadados.snirh.gov.br/geonetwork/srv/por/catalog.search#/metadata/f50527b9-24ed-41d5-b063-b5acfb25e10d) on Water Nacional Agency of Brazil.

## 4 - Vizualising the dataset on G.E.E

First step is upload the datasets into GEE using the assets space to organize this documents, than let's start to code. Each dataset will be a varaible. The region of interest (roi) is the varaiable that store the shapefile, than let's select the cloumn to filter especifically the Rio Doce basin geometry. After, it's necessary to create a contour of the geometry, using a empty variable that represent a Image with no bytes, than let's paint the empty variable using the paint() function passing the roi as a feature collection and determine the color and the width. 
Using the aggregate_array() function in a expecific column that conatins the name of all Basin, it's possible get the exactaly name of Rio doce Basin in the dataset. Knowing that the name of Rio doce Baisn is Doce, let's apply a filter() function in roi FeatureCollection, and this filter is boolean filter that's we needs to choice the column tha has the name of the basins and the other parameter is the value that wants to filter, in this case, "Doce". The result of this filter is store in doce_basin variable, and now let's create a empty image using the doce_basin variable as FeatureCollection and do the same process applied to the roi FeatureCollection contour. To finish this part let's plot on the map using the Map.addLayer() function and the results are in figure 3. 


To execute this first step just following the script bellow.

```
// Set the region (roi)

var roi = ee.FeatureCollection("users/contatobetterdecisions/GEOFT_DNAEE_SUBBACIA")
            
// Filter selection --  Get the name of rio deoce basin  == Doce
var data_value = roi.aggregate_array('DNS_NM')
print('All basins', data_value)

// Select Doce Basin

var doce_basin = roi.filter(ee.Filter.eq("DNS_NM", "Doce"))


// Create a contour of all Hidrografic Basins
var empty = ee.Image().byte()
var contour = empty.paint({
  featureCollection: roi,
  color:1, 
  width:2
})


// Create a contour of Doce basin
var empty_doce = ee.Image().byte()
var contour_doce = empty_doce.paint({
  featureCollection: doce_basin,
  color:2, 
  width:2

// Add contour om map

Map.addLayer(contour, {palette:["blue"]}, "Hidrografic Basins of Brazil")
Map.addLayer(doce_basin,{},"Rio doce Basin" )
Map.addLayer(contour_doce, {palette:["red"]}, "Rio doce Basin")


})
```
![figure 3](image/basinBrazil.png) 
Figure 3 - Hidrographic Basin of Brazil (blue), Hidrographic Doce Basin (red)

The second step is upload the csv file that contains all of soil samples and your respectives values of chemical analyses for each element and we use the asset space to store the file. This dataset has latitude and longitude columns, so it's necessary give this information when you configuring the csv file enviroment on GEE assets, it's explained in figure 4, but it's very simple, choose Assets table set, than click on New button, choose CSV file, on the next window configure the Asset ID, chance projects to users, now click on SELECT button and choose the csv file. The last part is the most important, go to Advanced otpions and put on X column the value of longitude and on the Y column the value of latitude, you need to use the same name of your dataset, than click on UPLOAD button and finish the process. Now you have a FeatureCollection with geospatial data. 


![figure 4](image/figure4.png)
Figure 4 - Upload a csv file with latitude and longitude columns


Let's continue and go back to the code editor. Now we need to read the csv file into GEE, the dataset is a FeatureCollection again and use the path of the csv file as parameter. To understand the dataset is necessary print the data on console, to get the number of rows and the name of the columns (figure 5). This dataset has 74 columns and 540 rows, but now let's filter the dataset and get only the cupper and iron columns and plot this geometry point as a feature in the map(figure 6). 

```
// Read the csv file 

var dataset = ee.FeatureCollection("users/contatobetterdecisions/Bacia_do_Rio_Doce_sedimento")

print(dataset)

print("Size of dataset", dataset.size())


// Now let's add the table 

Map.addLayer(dataset,{color: "black"}, "Soil samples")


// Now let's select only gold and cupper columns.

var fe_cu_sample = dataset.select(["fe_pct","cu_ppm"])

print("Size of dataset" , fe_cu_sample.size())


```

![figure 5](image/json.png)

Figure 5 - GEE print console of Json dataset. 74 Columns and 540 rows.

![figure 6](image/samples.png)

Figure 6 - Spatial distribution of samples. 

Now let's plot a histogram of the distribution these elements using ui.Chart.feature.histogram() function. The parameters is a featureCollection and porperty name, the figure 7 represent the distribution of iron and the figure 8 represent the distribution of cupper. Analising the cupper values it's possible to conclude that most important interval variabel to 1.6 to 21 ppm, and max value is 45 ppm, the 121 ppm values is outlier. When we analising the iron histgram we conclude that the principal interval goes to 1.6 to 6 ppm, and existis some outliers values in 17 ppm. 

![figure 7](image/histogram_iron.png)

Figure 7 - Histogram of iron ditribution

![figure 8](image/histogram_cupper.png)

Figure 8 - Histogram of cupper distribution









