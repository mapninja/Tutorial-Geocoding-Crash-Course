# Geocoding in ArcGIS
## Resources


## Basics of Geocoding
* Street Addresses
* Placenames
* Administrative Boundaries
* Esoteric Localities
* High-risk and PHI Geocoding

## Geocoding Services to discuss
* [locator.stanford.edu](https://locator.stanford.edu/arcgis/rest/services)  
* [stanford.maps.arcgis.com](https://stanford.maps.arcgis.com/)  
* [Census.gov geocoder](https://www.census.gov/geo/maps-data/data/geocoder.html)  

## Geocoding APIs:
 * [Geonames.org](https://www.geonames.org/)
 * [Geolocate](http://www.geo-locate.org/)

## Specialty Geocoding APIs:
 * [Yandex](https://tech.yandex.com/maps/doc/geocoder/desc/concepts/limits-docpage/) - Geocoding and Routing API for Russia, Eastern Europe and Western Asia.  
 * [MapMyIndia.com](https://www.mapmyindia.com/api/) - Geocoding and Routing API (plus many others!) for India

## Preparing Your Address Table
[Formatting a Table for Use in ArcGIS](http://support.esri.com/EN/knowledgebase/techarticles/detail/30727) 
 
### Things GIS hates about your tables:  
* Spaces or special characters (other than _ ) in field names  
* Field Names that start with a number  
* Empty Rows  
* Merged Cells  
* Excel Formulas

### Specifics on tabular data for geocoding
* Most geocoding services prefer street addresses in a single field, with City, State, Postal Codes, etc... in separate fields.  
* For placenames, concatenate administrative units, as follows:

```Dallas, TX, USA```
 
 
# Excercises


## Geocoding with OpenRefine and an API
### OpenRefine
Get it at OpenRefine.org

GREL Reference for learning Google Refine Language

### Example Data 
Here is a dataset to use for the excercise:
 


## Using the locator.stanford.edu Address Locators  
### Example Data  
We'll use one file from the **[data](https://github.com/mapninja/Tutorial-Geocoding-in-ArcGIS)** (at [https://github.com/mapninja/Tutorial-Geocoding-in-ArcGIS](https://github.com/mapninja/Tutorial-Geocoding-in-ArcGIS) ) for this exercise: 

* Evictions_94102.csv



The Stanford Geospatial Center has been developing our internal geocoding infrastructure. We now have a BETA Geocoding Server, based upon Esri's ArcGIS Server technology. The server currently provides geocoding services for North American Street Addresses.

To access the Address Locator services:

1. In ArcCatalog, or the Catalog Panel in ArcMap, expand the GIS Servers item    
2. Double-click the Add ArcGIS Server item    
3. Leave the default "Use GIS Services" option, click Next>  
4. For the 'Server URL' use: [http://locator.stanford.edu/arcgis](http://locator.stanford.edu/arcgis)  
5.  **For 'User Name' use your SUNetID (prefixed with the 'WIN\' domain) as WIN\SUNetID**  
6.  Enter the password associated with your SUNetID and check the option to Save Username/Password  
7.  Click Finish  


### Running the geocoding job  
1. Drag and drop the US_StreetAddress Address Locator from your Server Connection in the Catalog Panel, into the Map Document to make it the default. 
2. Drag the Evictions_94102.csv into the Map Document and open it to examine the attributes, paying attention to the field names for the address fields.
3.  Right-click on Evictions_94102.csv and select **Geocode addresses...** and then click OK to use the default you set, before. 
4. Set the appropriate fields in the Address input fields options
5. Open the Geocoding options and examine them, but accept the server defaults.
6. Click OK to run the geocoder.
6. Click Rematch to explore the options, try to manually match any unmatched records and Close the Rematch Dialog.
7. Right-click and Zoom to the Geocoding Result layer
8. Add a Basemap for context.  

## Building an Address Locator with ArcMap
### Example Data  
We'll use two files from the **[data](https://github.com/mapninja/Tutorial-Geocoding-in-ArcGIS)** (at [https://github.com/mapninja/Tutorial-Geocoding-in-ArcGIS](https://github.com/mapninja/Tutorial-Geocoding-in-ArcGIS) ) for this exercise: 
 
* US_county_1930_conflated.shp - the reference data we will use to build our geocoder
* photogrammar_image_count.csv

### Prepare the reference data

1. Open ArcMap and bring the US_county_1930_conflated.shp data into an empty Map Document
2. Open the attribute table, create a new **Text** field called PLACE, with a length of 255
3. right-click on the new PLACE field header and ***Calculate Field***
4. Use the following code to concatenate the COUNTY and STATE fields, adding appropriate commas and 'USA':

```[NHGISNAM] &" County, " & [STATENAM]&", United States"```  

This should result in values like this:
```Adair County, Missouri, United States```
### Create the Address Locator
1. In the Catalog Panel of ArcMap, right-click on your 'data' folder and select **New>Address locator...**
2. Select Single Field as the locator type and set US_county_1930_conflated.shp as the reference data
3. Set the PLACE field as the ***keyfield** and run the tool. 
4. Right click on the resulting Address Locator and inspect the Properties to see what changes you can make. 
5. Set the 
5. Close the properties and drag the locator into the Map Document to make it the default locator.

### Running the Geocoding Job  
1. Bring the photogrammar_image_count.csv table into ArcMap, right-click and select **Geocode Addresses** and click OK
2. Change to Single and Select **Column 1** as the **key**
3. Click on Geocoding Options and:
 4. Change the Spelling Sensitivity and Minimum Match Score to 50
 5. Uncheck Match if Candidates tie
 6. Check the option to write the Reference ID
7. Click OK, twice, to run the geocoder.
8. Click Rematch to explore the options, there, then click Close.
8. Use a Spatial Join to add the Geocoding Results attributes to the original US_county_1930_conflated.shp file





