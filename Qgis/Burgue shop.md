# Where should I open a new frachise?


## 1. The Problem
Tomas has a samll Burguer shop and he wants to open and franchise, because your business is doing well, so he hired me to help him to choose the best place to open your nhew Burguer Shop. In our first meet I tell you that we need mapping the 
concorrece, and it's easy in a samll city or in a small neighborhood, but he wants to search a place in Orlando indepent of a neighborhood, and he wants the raiting of each Burguer shop in rating site beacause it's will be important to select the best place. 
I agreed with him and I said that was been important known about the size and the purchasing power of population in each neighborhood. 

## 2. How can I get the localization of each Burger Shop in Orlando?
To this problem I gonna use scrap techinics of web maps site, like bing, google maps. A extension of google chrome is perfect for this job, Maps Scraper & Business Leads Finder. Install in your chrome than use the search bar to execute a search, in this case specificaly we wana find all burguer shops in Orlando City, Florida. The result of your search is put in a excel or csv file read to download to your on enviroment. So in this case a clean the columns of the data e just use the latitude, longitude and the raiting values of each Burguer shop, in my case the return 332 diferent Burguer Shop. After clean the data I create my project into QGIS.

## 3. Qgis, geoprocessing to geomarketing.
Fisrt we have to understand about the sorce of our project, in this case I need to use a Sistem Coordenate Referece in meters, beacause will be necessary create maps with inteporlation, specifically Kernel density maps. This kind of geoprcessing use interpolation based in distance, and when we talk about distance the best reference is meter, because is easier to calculate. 
For this project I use EPSG: 3747 to setting all of the enviroment, the excel file of Maps Scraper processing retruns the latitude and longitude in Geografic coordenate system, so it was necessary to reproject the data. The figure 1 is the result of the first step of this job and it's show all 332 Burguer Shop collected into scrap process.

![figure 1](image/burguer_map_location.png) 


## 4. Interpolation, Kernel Density maps (Heatmaps)
Now we know where are the Burguer shops, but a better visualization of this data is a density map. To do that I wil use the Kernel density map, it's a method based on distance of each element, in this case the element is the burguer shop localization. There are two important parameters of this method, one is the radio that will be used to calculate the distance of each element, the second is the pixel size, in this case the radio is 10.000 meters and the pixel size is a matrix of 5 x 5 meters. The result of this interpolation is avaiable on figure 2.

![figure 2](image/densitymap_distance.png) 
