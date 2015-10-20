#Geocoding in ArcGIS
##Resources


##Basics of Geocoding
###Preparing Your Address Table
[Formatting a Table for Use in ArcGIS](http://support.esri.com/EN/knowledgebase/techarticles/detail/30727)
Things ArcGIS Hates about Tables:
* Spaces or special characters (other than _ ) in field names
* Field Names that start with a number
* Empty Rows
* Merged Cells
* Formulas
* 

###Building an Address Locator
####Address Locator Style
[Commonly used address locator styles](https://desktop.arcgis.com/en/desktop/latest/guide-books/geocoding/commonly-used-address-locator-styles.htm)

####Reference Data


#####Streets
#####POI
#####Boundaries
###Running the Geocoding Job
##Using the locator.stanford.edu Address Locators
Over the summer, the Stanford Geospatial Center has been developing our internal geocoding infrastructure. We now have a BETA Geocoding Server, based upon Esri's ArcGIS Server technology. The server currently provides geocoding services for North American Street Addresses.

To access the Address Locator services:

* In ArcCatalog, or the Catalog Panel in ArcMap, expand the GIS Servers item  
* Double-click the Add ArcGIS Server item  
* Leave the default "Use GIS Services" option, click Next>
* For the 'Server URL' use: [http://locator.stanford.edu/arcgis](http://locator.stanford.edu/arcgis)
* **For 'User Name' use your SUNetID (prefixed with the 'WIN\' domain) as WIN\SUNetID**
* Enter the password associated with your SUNetID and check the option to Save Username/Password
* Click Finish
You should then be able to use the various Address Locator Services for bulk geocoding in ArcGIS.

The address locators inside the geocode folder include a Composite (capable of street addresses and postal codes) service for North America and separate services for U.S. Street Addresses and Postal Codes.

The address locators in the Rio folder include Address Locators built by The Spatial History Project at Stanford's Center for Spatial and Textual Analysis(CESTA). For more information about these geocoding services, see the Spatial History Project's Rio de Janeiro Historical Address Locator page.

For more information about the Geocoding Process in ArcGIS, see Esri's What is Geocoding? Guide.

###Running the job
