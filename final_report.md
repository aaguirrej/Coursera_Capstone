# Coursera IBM Coursera Data Science Capstone Final Report

### 1. Introduction where you discuss the business problem and who would be interested in this project.

1.1 The Problem
What type of restuarant to open in Downtown Toronto depending on the neighborhood? In order to open a restaurant of a certain type the idea is to explore the existing restaurants in the different Downtown Toronto's Neighborhoods. This will be based on restaurant types (i.e. Mexican, Sushi, French) available in each neighborhood and on ratings, price range and social activity of regular restaurant customers in those areas. 

1.2 Audience / Business Objective 
This would be of interest to entrepenuers wanting to open a new restuarant, so that they can clearly define the type of restaurant to open based on the current competitive landscape in a given neighborhood.  This will increase the chances of success of such venture, for example, by not trying to open a sushi restaurant in an neighborhood already crowded by such type of restaurant or by incorrectly position a price range depending on the competing alternatives on each neighbourhood.

### 2. Data where you describe the data that will be used to solve the problem and the source of the data.

2.1 Data Sources
Wikipedia page to get postal codes and names of each neighborhood.
GeoSpatial coordinates (latitude, longitude) for each neighborhood.
For this analysis the following data sources will be used:
Foursquare Places API to explore venues of each of the neighborhood.
Foursquare Places API to get venue details of each venue

2.2 Data Description and Wrangling

Geospatial/location, venues and venue details data sets will be used to analize the restaurant competitive landscape for Downtown Toronto.

2.2.1 Geospatial/location

Latitude and Longitude coordinates are needed to first define the location of each neighborhood. This is done by combining the neighborhood names that are part Downtown Toronto with their respectives geospatial coordinates. For simplicitiy the neighborhoods are grouped based on their respective postal codes. These neighborhood's coordinates are then going to be passed to Foursquare's Place API call (explore) to get all venue names and coordinates in a 500m radius.  

2.2.2 Explore Venues 
Only venues that have a "restaurant" value included in the Category field are going to be kept for further analysis. The following fields are going to be included in the dataset:

Venue ID:  These IDs are used in the Foursquare API call to get venue details and will used as a primary key field to merge or join datasets.
Venue Name: Just used for reference when merging or joining datasets or for looking up their respective pages in foursquare website.
Venue Latitude:  Latitude coordinate of the venue/restaurant
Venue Longitue:  Longitude coordinate of the venue/restaurant
Venue Category: Indicates the type of restaurant and the venue category, for example Sushi Restaurant, Chinese Restaurant. Type of restaurant refers to the type of cusine being served. In some instances the type of restaurant is not defined in the Venue Category field, so this restaurants can be considered of serving local canadien food.

2.2.2 Venue Details
Venue Details data set is obtained by passing all the Venue ID's from the previous step to the API call for venue details.  

The following fields are included in the data set:
Restaurant ID: It's the Venue ID but renamed to Restaurant ID for this dataset
Restaurant Name: It's the Restaurant ID but renamed to Restaurant ID for this dataset
Rating: Value from 0-10 given by customers based on the quality of food/service	
Rating Signals: Number of customers that submitted a rating
Likes: Number of customers who liked the venue	
Tips: Number of customer who submitted a tip (comment about the restaurant)	
Listed:	
Photos: Number of photos uploaded to the restuarant page in Forsquare	
Price Tier: Value from 0-4 indicated if the price of the menu is cheap, moderate, expensive, very expensive

All the about fields are included as a measure of restaurant quality, price range and customer engagement.  Factors to be considered depending on the location and type of restaurant.  These values will be used to cluster the different restaurants in other dimensions other than location or category.

As a side note in the API call results not all restaurants have a rating or/and price tier assigned.  In this case those restaurants are ignored for the analysis.


### Methodology section which represents the main component of the report where you discuss and describe any exploratory data analysis that you did, any inferential statistical testing that you performed, if any, and what machine learnings were used and why.

### Results section where you discuss the results.
### Discussion section where you discuss any observations you noted and any recommendations you can make based on the results.
### Conclusion section where you conclude the report.
