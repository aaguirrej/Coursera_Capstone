# Coursera IBM Coursera Data Science Capstone Final Report

### 1. Introduction where you discuss the business problem and who would be interested in this project.

**1.1 The Problem**

What type of restuarant to open in Downtown Toronto depending on the neighborhood? In order to open a restaurant of a certain type the idea is to explore the existing restaurants in the different Downtown Toronto's Neighborhoods. This will be based on restaurant types (i.e. Mexican, Sushi, French) available in each neighborhood and on ratings, price range and social activity of regular restaurant customers in those areas. 

**1.2 Audience / Business Objective** 

This would be of interest to entrepenuers wanting to open a new restuarant, so that they can clearly define the type of restaurant to open based on the current competitive landscape in a given neighborhood.  This will increase the chances of success of such venture, for example, by not trying to open a sushi restaurant in an neighborhood already crowded by such type of restaurant or by incorrectly position a price range depending on the competing alternatives on each neighbourhood.

### 2. Data where you describe the data that will be used to solve the problem and the source of the data.

**2.1 Data Sources**

Wikipedia page to get postal codes and names of each neighborhood.
GeoSpatial coordinates (latitude, longitude) for each neighborhood.
For this analysis the following data sources will be used:
Foursquare Places API to explore venues of each of the neighborhood.
Foursquare Places API to get venue details of each venue

**2.2 Data Description and Wrangling**

Geospatial/location, venues and venue details data sets will be used to analize the restaurant competitive landscape for Downtown Toronto.

**2.2.1 Geospatial/location**

Latitude and Longitude coordinates are needed to first define the location of each neighborhood. This is done by combining the neighborhood names that are part Downtown Toronto with their respectives geospatial coordinates. For simplicitiy the neighborhoods are grouped based on their respective postal codes. These neighborhood's coordinates are then going to be passed to Foursquare's Place API call (explore) to get all venue names and coordinates within a 500m radius.  

**2.2.2 Explore Venues** 

Only venues that have a "restaurant" value included in the Category field are going to be kept for further analysis. The following features are included in the dataset:

* Venue ID:  These IDs are used in the Foursquare API call to get venue details and will be used as a primary key field to merge or join datasets.
* Venue Name: Just used for reference when merging or joining datasets or for looking up their respective pages in foursquare website.
* Venue Latitude:  Latitude coordinate of the venue/restaurant
* Venue Longitue:  Longitude coordinate of the venue/restaurant
* Venue Category: Indicates the type of restaurant and the venue category, for example Sushi Restaurant, Chinese Restaurant. Type of restaurant refers to the type of cusine being served. In some instances the type of restaurant is not defined in the Venue Category field, so these restaurants can be considered as serving local Canadian food.

**2.2.2 Venue Details**

Venue Details dataset is obtained by passing all the Venue ID's from the previous step to the Venue details API call.  

The following fields are included in the data set:

* Restaurant ID: It's the Venue ID but renamed to Restaurant ID for this dataset
* Restaurant Name: It's the Restaurant ID but renamed to Restaurant ID for this dataset
* Rating: Value from 0-10 given by customers based on the quality of food/service	
* Rating Signals: Number of customers that submitted a rating
* Likes: Number of customers who liked the venue	
* Tips: Number of customers who submitted a tip (any comment about the restaurant)	
* Listed:	In how many user generated lists a restaurant is included
* Photos: Number of photos uploaded to the restuarant page in Forsquare	
* Price Tier: Value from 0-4 indicated if the price of the menu is cheap, moderate, expensive, very expensive

All the about fields are included as a measure of restaurant quality, price range and customer engagement/recommendation.  Factors to be considered depending on the location and type of restaurant.  These values will be used to cluster the different restaurants in other dimensions other than location or category.

As a side note in the API call results not all restaurants have a rating or/and price tier assigned.  In this case those restaurants are ignored for the analysis.


### 3. Methodology section which represents the main component of the report where you discuss and describe any exploratory data analysis that you did, any inferential statistical testing that you performed, if any, and what machine learnings were used and why.

**3.1 Data Import and Wrangling**

Postal codes and Neighbourhoods datasets are imported from Wikipedia, Latitudes and Longitudes from the Geospatial Coordinates file. The combined dataset is grouped by Postal codes and Borough. The dataset is then filtered by the Borough "Downtown Toronto" and its respective Neighbourhoods.

![Image 1](https://github.com/aaguirrej/Coursera_Capstone/blob/master/Screen%20Shot%202020-03-31%20at%208.41.18%20PM.png)

Data is extracted from Foursquare's API based on the provided Latitudes and Longitudes for each group of Neighborhoods. Venue ID, Venue Category will be used to filter the venues that contain any Restaurant value in Venue Category.

![Image 2](https://github.com/aaguirrej/Coursera_Capstone/blob/master/Screen%20Shot%202020-03-31%20at%209.00.47%20PM.png)

Next step is to obtain the Restaurant Stats dataset using the Venue ID of each restaurant in the API call. This dataset includes the following measures: Rating, Rating Signals, Likes, Listed, Photos, Tips and Price Tier. Only the Restaurants with Rating and Price Tier are included in the dataset.

![Image 3](https://github.com/aaguirrej/Coursera_Capstone/blob/master/Screen%20Shot%202020-03-31%20at%209.03.15%20PM.png)

Downtown Restuarants and Restaurant Stats Datasets are merged using the Venue ID as primary key.

![Image 4](https://github.com/aaguirrej/Coursera_Capstone/blob/master/Screen%20Shot%202020-03-31%20at%209.07.36%20PM.png)

One hot encoding for Restaurant Category's categorical values on the merged dataset.

![Image 5](https://github.com/aaguirrej/Coursera_Capstone/blob/master/Screen%20Shot%202020-03-31%20at%209.09.56%20PM.png)

**3.2 Exploratory Data Analysis**

Data visualization is performed for each feature (measures) of the X dataset. Histograms show that Likes, Listed, Photos and Rating Signals have similar distributions. Rating's distribution indicates that most of the restaurant ratings are between 7.0 and 8.5. Price Tier distribution shows that most of the restaurants are "Moderate" in terms of pricing.



### Results section where you discuss the results.
### Discussion section where you discuss any observations you noted and any recommendations you can make based on the results.
### Conclusion section where you conclude the report.
