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
The Stanford Geospatial Center has been developing our internal geocoding infrastructure. We now have a BETA Geocoding Server, based upon Esri's ArcGIS Server technology. The server currently provides geocoding services for North American Street Addresses.

To access the Address Locator services:

* In ArcCatalog, or the Catalog Panel in ArcMap, expand the GIS Servers item    
* Double-click the Add ArcGIS Server item    
* Leave the default "Use GIS Services" option, click Next>  
* For the 'Server URL' use: [http://locator.stanford.edu/arcgis](http://locator.stanford.edu/arcgis)  
* **For 'User Name' use your SUNetID (prefixed with the 'WIN\' domain) as WIN\SUNetID**  
* Enter the password associated with your SUNetID and check the option to Save Username/Password  
* Click Finish  

You should then be able to use the various Address Locator Services for bulk geocoding in ArcGIS.

The address locators inside the geocode folder include a Composite (capable of street addresses and postal codes) service for North America and Brazil, and separate services for U.S. and Brazilian Street Addresses.

The address locators in the Rio folder include Address Locators built by The Spatial History Project at Stanford's Center for Spatial and Textual Analysis(CESTA). For more information about these geocoding services, see the Spatial History Project's Rio de Janeiro Historical Address Locator page.

For more information about the Geocoding Process in ArcGIS, see Esri's What is Geocoding? Guide.




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
5. Close the properties and drag the locator into the Map Document to make it the default locator.

### Running the Geocoding Job  
1. Bring the photogrammar_image_count.csv table into ArcMap, right-click and select **Geocode Addresses** and click OK
2. Change to Single and Select **Column 1** as the **key**
3. Click on Geocoding Options and:
 4. Change the Spelling Sensitivity and Minimum Match Score to 50
 5. Uncheck Match if Candidates tie
 6. Check the option to write the Reference ID
7. Click OK, twice, to run the geocoder.





