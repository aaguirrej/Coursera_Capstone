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

Latitude and Longitude coordinates are needed to first define the location of each neighborhood. This is done by combining the neighborhood names that are part Downtown Toronto with their respectives geospatial coordinates. For simplicitiy the neighborhoods are grouped based on their respective postal codes. These neighborhood's coordinates are then going to be passed to Foursquare's Place API call (explore) to get all venue names and coordinates in a 500m radius.  Only the venues that have a "restaurant" value included in the Category field are going to be kept for further analysis. In the API call each restaurant has its respective longitude and latitude coordinates.  





### Methodology section which represents the main component of the report where you discuss and describe any exploratory data analysis that you did, any inferential statistical testing that you performed, if any, and what machine learnings were used and why.

### Results section where you discuss the results.
### Discussion section where you discuss any observations you noted and any recommendations you can make based on the results.
### Conclusion section where you conclude the report.
