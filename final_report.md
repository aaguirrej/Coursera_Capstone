# Coursera IBM Coursera Data Science Capstone Final Report

### 1. Introduction where you discuss the business problem and who would be interested in this project.

**1.1 The Problem**

What type of restaurant to open in Downtown Toronto depending on the neighborhood? In order to open a restaurant of a certain type the idea is to explore the existing restaurants in the different Downtown Toronto's Neighborhoods. This will be based on restaurant types (i.e. Mexican, Sushi, French) available in each neighborhood and on ratings, price range and social activity of regular restaurant customers in those areas. 

**1.2 Audience / Business Objective** 

This would be of interest to entrepreneurs wanting to open a new restuarant, so that they can clearly define the type of restaurant to open based on the current competitive landscape in a given neighborhood.  This will increase the chances of success of such venture, for example, by not trying to open a sushi restaurant in an neighborhood already crowded by such type of restaurant or by incorrectly position a price range depending on the competing alternatives on each neighbourhood.

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

![Image 6](https://github.com/aaguirrej/Coursera_Capstone/blob/master/Screen%20Shot%202020-03-31%20at%209.12.41%20PM.png)

The correlation analysis shows that Rating Signals is highly correlated to Likes, Photos, Tips and Listed features. This means that Rating Signals can be used as a proxy for customer engagement and referral.

![Image 7](https://github.com/aaguirrej/Coursera_Capstone/blob/master/Screen%20Shot%202020-03-31%20at%209.17.12%20PM.png)

**3.3 Machine Learning Model**

The K-Prototypes clustering algorithm is applied to the feature dataset. The feature dataset contains both categorical and numerical variables and according to statistical literature K-Prototypes is more suitable in this case than using K-Mean.

The goal with K-Prototypes is to cluster the restuarants in the different Downtown Toronto's Neighbourhoods and get insights based on the features included in the dataset.

As a first step, the optimal number is calculated based on the K-Prototypes cost. The resulting curve's elbow indicates that K should be 3.

![Image 8](https://github.com/aaguirrej/Coursera_Capstone/blob/master/Screen%20Shot%202020-03-31%20at%209.21.07%20PM.png)

Second step is to apply the K-Prototypes Algorithm to the standarized feature dataset and obtain the resulting labels for each cluster (0,1,2)

![Image 9](https://github.com/aaguirrej/Coursera_Capstone/blob/master/Screen%20Shot%202020-03-31%20at%209.23.16%20PM.png)

### 4. Results section where you discuss the results.

For visualization purposes the resulting clusters are included as markers on a Toronto map. Each cluster is identified by its respective cluster label, which is used as a marker on the map(0,1,2).

![Image 10](https://github.com/aaguirrej/Coursera_Capstone/blob/master/Screen%20Shot%202020-03-31%20at%209.29.27%20PM.png)

The map shows how the different clusters are distributed in each neighbourhood. Most of the restaurants are located in Chinatown/Grange Park/Kensignton Market, Church and Wellesley and Central Bay Street.

Cluster 0 is the most representative on those neighbourhoods and overall. Cluster 1 is mainly present in Chinatown/Grange Park/Kensignton Market, Ryerson/Garden District, St James Town. Cluster 2 is predomently in Ryerson/Garden District, Harbourfront, Adeleaide/King/Richmond.

Ryerson/Garden District, Harbourfront, Design Exchange, Adeleaide/King/Richmond are neighbourhoods that include a good balanced mix of number of restaurants per cluster.

Looking at the distribution of cluster labels per Restaurant Category, it indicates that Restaurant (local cuisine), Japanese Restaurant and Italian Restaurant are the most common categories in Cluster 0. Cluster 1 is very similar only adding Sushi and Mexican restaurant categories. Cluster 2 includes mostly Mexican, Ramen, Restaurant (local), Japanese and Thai categories.

![Image 11](https://github.com/aaguirrej/Coursera_Capstone/blob/master/Screen%20Shot%202020-03-31%20at%209.32.43%20PM.png)

Looking at the distribution of cluster labels by Price Tier, Cluster 0 groups most of the 'Cheap' and 'Moderate' Price Tier restaurants. Cluster 1 has a good mix of Price Tiers. Cluster 2 doesn't include the 'Very Expensive' Price Tier.

![Image 12](https://github.com/aaguirrej/Coursera_Capstone/blob/master/Screen%20Shot%202020-03-31%20at%209.34.38%20PM.png)

For the cluster analysis, each cluster's characteristics is identified by looking at its Cluster Center (Centroid) for each feature and cluster.

Cluster 0:
Rating, Price Tier and Rating Signals for this cluster are all below average. For the Restaurant Categories the following are above average: Afghan, Asian, Caribbean, Chinese, Comfort Food, Dim Sum, Doner, Ethiopian, Falafel, Fast Food, Filipino, German, Greek, Indian, Italian, Korean, Mediterranean, Modern European, Molecular, Seafood, Vegan, Vietnamese.

Cluster 1:
This cluster has Price Tier high/above average and Rating Signals, Rating below average. For the Restaurant Categories the following are above average: Sushi, Local Restaurant, New American, Middle Eastearn, French, Dumpling, Italian.

Cluster 2:
Rating, and Rating Signals are well above average in this cluster, with a just below average Price Tier. For the Restaurant Categories the following are above average: American, Japanese, Mexican, Ramen, Thai

Rating Signals feature is used as a proxy for other related engagement features: Likes, Photos, Listed, Tips.

![Image 13](https://github.com/aaguirrej/Coursera_Capstone/blob/master/Screen%20Shot%202020-03-31%20at%209.36.09%20PM.png)

### 5. Discussion section where you discuss any observations you noted and any recommendations you can make based on the results.

Notes on the cluster's definitions:

The Italian restaurant category is shared between Cluster 0 and 1. It may be possible that the Italian Restaurants in Cluster 0 are mostly fast food related (serving pizzas, takeaway).

High levels of Rating Signals, Likes, Photos, Listed, Tips not only may show high customer engagement, but also indicate that customers like to share their experiences in a venue, which can be interpreted as an implicit recommendation to eat in a given restaurant.

In the chart below all clusters are visualized based on Rating (X axis), Restaurant Category (Y axis), Price Tier (hue) and Rating Signals (maker size). Cluster 1 and 2 show less variability in terms of Rating compared to Cluster 0. Cluster 0 aggregates most of the restaurants with low Price Tier and low Rating Signals. Cluster 2 has the lowest share of restaurants but with higher levels of customer engagements.

![Image 14](https://github.com/aaguirrej/Coursera_Capstone/blob/master/Screen%20Shot%202020-03-31%20at%209.39.30%20PM.png)

### 6. Conclusion section where you conclude the report.

By using an unsupervised machine learning algorithm like K-Prototypes, the Restaurants in Downtown Toronto can be classified in 3 clusters. As indicated in the Results Section, the different restaurant categories (Restaurant features) have been grouped into: Food Restaurants or Niche/Ethnic Restaurants (Cluster 0 Local and International Restaurants (Cluster 1) International Restaurants (Cluster 2).

The Rating Signals, Rating and Price Tier features are plotted below. As stated in the Discussion section, the scatter plot shows that:

Cluster 0 has the greatest variability in terms of Rating, low Rating Signals (less than 200) and Price Tear mostly between 1 and 2 (Cheap and Moderate). Cluster 1 has a high Rating over 7.4, average Rating Signal but high Price Tier . Cluster 2 has a over 300 Rating Signals, the highest of all cluster combined with a high Rating.

Based on the cluster analysis, each of the clusters can be defined as follows:

Cluster 0: Fast Food Restaurants or Niche/Ethnic Restaurants that mostly offer value for money.
Cluster 1: Best Rated Fancy Local and International Restaurants
Cluster 2: Best Rated and Recommended International Restaurants

This cluster analysis can be used by entrepreneurs trying to open a restaurant in Dowtown Toronto area. For example what type of restaurant should an entrepreneur open in Central Bay Street? Looking at the Neighbourhoods by Cluster Labels countplot, it could be a Cluster 0 or Cluster 1 type of restaurant, since it seems that there is room to grow on those types of restaurants compared to Church and Wellesley neighbourhood. If an entrepreneur wants to open a restaurant with high customer engagement and word of mouth (Cluster 2), then Garden District or Harbourfront would be the suggested Neighbourhoods, as long as the restaurant is a quality International Restaurant.

For deeper analysis some other considerations like demographics, real state and land use should be also be considered for a suitable location.

![Image 15](https://github.com/aaguirrej/Coursera_Capstone/blob/master/Screen%20Shot%202020-03-31%20at%209.42.50%20PM.png)
![Image 16](https://github.com/aaguirrej/Coursera_Capstone/blob/master/Screen%20Shot%202020-03-31%20at%209.43.00%20PM.png)

Author: Andres Aguirre
