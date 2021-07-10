# Coursera Capstone Week 4

## Part 2 Data Description:

#### 2.1 Data Source:
I will use Kaggle datasets and Foursquare location data in order to solve the problems. I will use the "San Francisco Crime Classification" dataset in Kaggle, and here is the link to it https://www.kaggle.com/kaggle/san-francisco-crime-classification. I will also use a multitude of libraries in order to perform computation, visualization, and other necessary things. 

#### 2.2 Data Information:
The Kaggle dataset has a lot of useful information that I will use. I will use the training dataset where I have the timestamp, category, description, day of the week, district, resolution, address, latitude, and longitude. I will also use the Foursquare location data, specifically the venue information, in order to solve the problems. This data is related to location and types of crimes which will help me solve the problems. 

#### 2.3 Data Usage:
I will use the Kaggle dataset's timestamp to determine the reported crimes in a certain year. I then will use the address, district, latitude, longitude, and folium libraries in order to map the number of crimes in San Fransico and put them into marker clusters. I will then use the Foursquare location data in order to find the nearest venue to the location of the crime. This will be visualized and it can be used to help police and tourists. 

The data will also be used to solve the second problem. I will use the dataset's timestamp, category, description, district, address, latitude, longitude, and other libraries in order to find the top 3 crimes in each district and compare each district to each other. I will first choose a year in order to limit the amount of data. I then will find the frequency of the type of crime in each district. I will then use K-Means in order to cluster the 10 districts and compare them. I will visualize the result on a map. This will help law enforcement figure out which is the most common crime, and prevent it. It will also aid tourists to help them watch out for specific dangers. 
