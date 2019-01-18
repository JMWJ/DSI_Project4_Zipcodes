# Project 4 - The Client Project 

---
The ***objective*** of the client project is to ***use zipcodes to proxy home values and loss in event of disaster***. Our project consists of building a tool to return housing and population metrics in a given zipcode.  The user will feed the code with a comma delimited list of affected areas (zip codes, can be int or str format) as input, and retrieve the current property values.  

## Executive Summary
---
During times of disaster it is fairly difficult to predict the amount of economic loss that will occur. Economic loss is not limited to physical infrastructure during times of disaster; it also includes lost wages and other damages that are challenging to measure. For the purpose of this project, we use a proxy equation to estimate economic loss given a disaster level parameter (ranging 0-10) and a list of zipcodes. To make the information easily digestible a tool was built to display demographic information on a map with a pop up over the specific area of interest. This allows for users such as government entities to input a zipcode along with the disaster level parameter to understand the population within a area and the possible losses if various disasters were to strike the area. We believe the tool's value is that insurance companies and other government entities can use it to properly allocate resources that will be used for rebuilding a community after a disaster. Users can also enrich the data with their own information and feed it into the display tool.


## Interesting Packages Used
---
For our project we mainly leveraged [folium](https://pypi.org/project/folium/) and [uszipcode](https://pypi.org/project/uszipcode/) packages in Python to create the tool and to pull the additional demographic information based on zipcode.  Folium creates a rendering of a map based on lat/long values and then given a zipcode it will return a circle that you can hover over with a mouse to display demographic information.


### Limitations of Function for Demographic Information (function using folium)
---
 * Can't enter zip codes as int if they start with 0
 * Disaster levels need to be within the range of 0 - 10

## Data Information
---
For the home value data, we used the [Zillow Research](https://www.zillow.com/research/data/) page to download flat files of ***Median Home Values by Top and Bottom Tiers***.  The tier system in Zillow is divided into thirds given a ***geography*** parameter that allowed for us to pull data on the zipcode level.

Additionally, the Python package [uszipcode](https://pypi.org/project/uszipcode/) mentioned above has datasets within the package that returned high level metrics give a zip.  We used that data to create a dataframe that gets passed into the our display tool.

### Limitations of Data
Due to usage of Zillow Research data and the specificity of top and bottom tier informatino given a zipcode.  The number of zipcodes available to use that had populated values across top, bottom, overall tables were approximately 5k, 2.8k, and 10k respectively.  

Informtation on the zipcode level is not populated as well due to Zillow's limited number of fully populated zipcodes.  This is because Zillow will only have information for zips that list their housing values.  It is not a complete set of all homes within a given geographic location.

Zestimate API - Takes an extenstive amount of time to match each address within the Zillow database.  This also does not include the amount of time needed to clean data into the format Zillow wants for the API.   


### Data Dictionary of Data Set Used for Tool

|Column Name | Data Type | Brief Description |
|---|---|---|
|lat|float|Latitude|
|lng|float|Longitude|
|median_home_value|float|Median home values from uszipcode python|
|median_household_income|float|Median household income|
|occupied_housing_units|int|Occupied housing units|
|population|int|Population size|
|Zip|str|Zip code|
|City|str|City Name|
|State|str|State|
|Median_Home_Value_Z|float|Median home values from Zillow Dataset|
|Top_Tier_Median_Home_Value|float|Top third median home values from Zillow Dataset|
|Bottom_Tier_Median_Home_Value|float|Bottom third median home values from Zillow Dataset|

## How to Navigate Files and Folders
---
1. ***Code*** Folder, 5 Files, Organized with _NB suffix
  * NB1 - NB3 contains code to clean Zillow dataset: mostly dropping NULLS and columns.
  * NB4 is the function that creates a base demographic dataset using the Zillow zipcodes.
  * NB5 is the folium function that renders a map and circles that will display the demographic info based on zips that feed into it. 
  * NB6 is the Zillow API that will generate distribution of housing values for a given set of zips.
<br><br>

2. ***Data*** Folder, 4 files
  * All files with ***cleaned_*** suffix are datasets that contain cleaned Zillow data for merging in NB4 above
  * final_flat_for_folium.csv is the flat file passed into the folium function that has the Zillow data. 
<br><br>
3. ***Raw_data_files*** Folder, 4 files containing raw files used to generate cleaned data files in Data & Code folders above
<br><br>
4. ***zipcode*** Folder, 2 files containing zipcode database created in SQLite for intial usage and other files that support the final Code folder.  


## Future Improvements
---
1. Find a data source that has complete housing information base on zipcodes
2. Enrich disaster economic loss function sliced by types of disasters.  
3. Enrich display with Zestimate API data

## Contributors
--
 * Mason Childress - masonrchildress@gmail.com
 * Katy Chow - kchow1989@gmail.com
 * Cesar Mendoza - tecougarali@gmail.com
 * Joey Ward - josephmwardjr@gmail.com
