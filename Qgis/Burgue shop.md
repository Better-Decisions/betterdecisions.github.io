# Where should I open a new frachise?


## 1. The Problem
Tomas has a samll Burguer shop and he wants to open and franchise, because your business is doing well, so he hired me to help him to choose the best place to open your new Burguer Shop. In our first meet I tell you that we need mapping the 
concorrece, and it's easy in a small city or in a small neighborhood, but he wants to search a place in Orlando City, and he wants the raiting of each Burguer shop in rating site beacause it's will be important to select the best place. 


## 2. How can I get the localization of each Burger Shop in Orlando?
For this problem I gonna use scrap techinics of web maps site, like bing, google maps. A extension of google chrome is perfect for this job, Maps Scraper & Business Leads Finder. Install in your chrome than use the search bar to execute a search, in this case specificaly we wana find all burguer shops in Orlando City, Florida. The result of your search is put in a excel or csv file read to download to your on enviroment. So in this case a clean the columns of the data e just use the latitude, longitude and the raiting values of each Burguer shop, in my case the return 332 diferent Burguer Shop. After clean the data, i droped emails , teefone and adress of each burguer shop, and use only the name, the coordanates and raiting, then I create my project into QGIS.

## 3. Qgis, geoprocessing to geomarketing.
Fisrt we have to understand about the sorce of our project, in this case I need to use a  Coordenate Referece System in meters, beacause will be necessary create maps with inteporlation, specifically Kernel density maps. This kind of geoprcessing use interpolation based in distance, and when we talk about distance the best reference is meter. 
For this project I use EPSG: 3747 to setting all of the enviroment, the excel file of Maps Scraper processing retruned the latitude and longitude in Geografic coordenate system, so it was necessary to reproject the data. The figure 1 is the result of the first step of this job and it's show all 332 Burguer Shop collected into scrap process.

![figure 1](image/burguer_map_location.png) 


## 4. Interpolation, Kernel Density maps (Heatmaps)
Now we know where are the Burguer shops, but a better visualization of this data is a density map. To do that I wil use the Kernel density map, it's a method based on distance of each element, in this case the element is the burguer shop localization. There are two important parameters of this method, one is the radio that will be used to calculate the distance of each element, the second is the pixel size, in this case the radio is 10.000 meters and the pixel size is a matrix of 5 x 5 meters. The result of this interpolation is avaiable on figure 2.

![figure 2](image/densitymap_distance.png) 


So we can do the same interpolation with the same parameters, but now we will put a weight from ij a field, in this case the rating value. This information will help us to understand where are the bets rated Burguer Shop in Orlando city, and cross this information with the concentration and distribution of the Burguer Shops. The result of this analyses you can see on figure 3

![figure 3](image/density_raiting_map.png)

## 5. Conclusion
Now we have a important task, we need to see if we can locate a new Burguer Shop, so for this part is important compare our results. First let's see the distribution of Burguer Shops based on your rating, figure 4. Using the Bubble map we can concluded that the south and the east area is a good area to open a new Burguer Shop, because has few Burguer Shops, but the rating is good and it's indicate that exists specific clients.

![figure 4](image/bubbles_maps.png)

Using the comparative map (figure 5) I indicated the point 1 like a promissor area, it will be probably a increase area, and this area are between the south and esat axis, and has great burguer shops. 

![figure 5](image/Crossing_distance_rating.png)

So tomas had a great problem and using geoprocessing we could help you to find a new place for your neww Burguer Shop. 

