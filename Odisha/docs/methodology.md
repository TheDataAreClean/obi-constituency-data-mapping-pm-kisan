## QGIS Steps

QGIS version 3.18.3-Zürich has been used for the analysis.

- Open a new Project on QGIS and open the village boundary file for Odisha. The file has data as per the Census of India, 2011
- Correct for [*invalid geometry*](https://www.qgistutorials.com/en/docs/3/handling_invalid_geometries.html) in the village boundary file
- Add a [*delimited text layer*](https://gis.stackexchange.com/questions/273143/adding-delimited-text-layer-in-qgis) to import [.csv](https://en.wikipedia.org/wiki/Comma-separated_values) file *PM_Kisan_merged* from the *data* folder and perform [table join](https://www.qgistutorials.com/en/docs/performing_table_joins.html) add the columns in *PM_Kisan_merged* file to the village layer against the column 'V_NAME' or 'V_NO' common in both
- Add [*Centroid*](https://gis.stackexchange.com/questions/45243/how-to-determine-the-centroid-of-polygons) to the Village polygons. A new layer with the all the centroids gets created.
- Create [*Spatial Index*](https://gis.stackexchange.com/questions/265434/creating-spatial-index-for-geopackage-using-qgis) to the *Centroid* layer. Spatial indexes are created for speeding up geometry queries. It helps in speeding up the display in QGIS of database layers when zoomed in.

- Open the boundary file for Odisha Assembly Constituency (AC) and correct for invalid geometry following the same steps as mentioned in the second point
- Join the Assembly Constituency and the village Centroid layers by using [*Join Attributes by Location*](https://www.qgistutorials.com/en/docs/3/performing_spatial_joins.html) command with *'contains'* condition. A new *Joined layer* is created.
- Export the *Joined layer* in [.csv format](https://en.wikipedia.org/wiki/Comma-separated_values) in order to use it fo further analysis.
