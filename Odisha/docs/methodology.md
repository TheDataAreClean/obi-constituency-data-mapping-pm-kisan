# Methodology

## Objective

## States
 1. Odisha

## Scheme
 1. PM Kisan Yojna

## Premise
* CDL team extracted the map server link from Odisha Geo-portal. It contains all administrative and political boundary for Odisha. It can be accessed [here](https://github.com/CivicDataLab/maps-of-india/tree/main/odisha)
* The scheme indicators are downloaded from the scheme MIS dashboard for all Villages of Odisha
* Aggregate indicators for constituencies can be calculated by linking the two files using Village Code (V_CODE) and further spatially joining the two layers on QGIS

## Process

#### QGIS Steps

QGIS version 3.18.3-Zürich has been used for the analysis.

- Open a new Project on QGIS and open the village boundary file for Odisha. The file has data as per the Census of India, 2011
- Correct for [*invalid geometry*](https://www.qgistutorials.com/en/docs/3/handling_invalid_geometries.html) in the village boundary file
- Add a [*delimited text layer*](https://gis.stackexchange.com/questions/273143/adding-delimited-text-layer-in-qgis) to import [.csv](https://en.wikipedia.org/wiki/Comma-separated_values) file *PM_Kisan_merged* from the *data* folder and perform [table join](https://www.qgistutorials.com/en/docs/performing_table_joins.html) add the columns in [*PM_Kisan_merged*](https://github.com/cbgaindia/obi-constituency-data-mapping-pm-kisan/blob/main/Odisha/results/pm_kisan_merged.csv) file to the village layer against the column 'V_NAME' or 'V_NO' common in both
- Add [*Centroid*](https://gis.stackexchange.com/questions/45243/how-to-determine-the-centroid-of-polygons) to the Village polygons. A new layer with the all the centroids gets created.
- Create [*Spatial Index*](https://gis.stackexchange.com/questions/265434/creating-spatial-index-for-geopackage-using-qgis) to the *Centroid* layer. Spatial indexes are created for speeding up geometry queries. It helps in speeding up the display in QGIS of database layers when zoomed in.

- Open the boundary file for Odisha Assembly Constituency (AC) and correct for invalid geometry following the same steps as mentioned in the second point
- Join the Assembly Constituency and the village Centroid layers by using [*Join Attributes by Location*](https://www.qgistutorials.com/en/docs/3/performing_spatial_joins.html) command with *'contains'* condition. A new *Joined layer* is created.
- Export the *Joined layer* in [*.csv format*](https://en.wikipedia.org/wiki/Comma-separated_values) as [*ac_contains_village_centroids*](https://github.com/cbgaindia/obi-constituency-data-mapping-pm-kisan/blob/main/Odisha/data/qgis/ac_contains_village_centroids.csv) in order to use it fo further analysis.

#### Jupyter Notebook Steps

Python v3.6+ has been used for the analysis.
* Import the relevant python libraries and then import the CSV file [*pm-kisan-pay-data-odisha-with-amount*](https://github.com/cbgaindia/obi-constituency-data-mapping-pm-kisan/blob/main/Odisha/data/updated/pm-kisan-pay-data-odisha-with-amount.csv) and [*village_gis_list_2011_odisha*](https://github.com/cbgaindia/obi-constituency-data-mapping-pm-kisan/blob/main/Odisha/data/qgis/village_gis_list_2011_odisha.csv) extracted from QGIS.

* Check for duplicates in both the file and drop duplicates
* The number of villages in the [*pm-kisan-pay-data-odisha-with-amount*](https://github.com/cbgaindia/obi-constituency-data-mapping-pm-kisan/blob/main/Odisha/data/updated/pm-kisan-pay-data-odisha-with-amount.csv) file is more than in [*village_gis_list_2011_odisha*](https://github.com/cbgaindia/obi-constituency-data-mapping-pm-kisan/blob/main/Odisha/data/qgis/village_gis_list_2011_odisha.csv) file.
* Perform inner join with left_on = 'V_CODE' from [*odisha_gis_village_no_duplicates*](https://github.com/cbgaindia/obi-constituency-data-mapping-pm-kisan/blob/main/Odisha/results/odisha_gis_village_no_duplicates.csv) and right_on = 'vill_code' from [*pm-kisan-pay-data-odisha-with-amount*](https://github.com/cbgaindia/obi-constituency-data-mapping-pm-kisan/blob/main/Odisha/data/updated/pm-kisan-pay-data-odisha-with-amount.csv).
* Import [*PM_Kisan_merged*](https://github.com/cbgaindia/obi-constituency-data-mapping-pm-kisan/blob/main/Odisha/results/pm_kisan_merged.csv) file to QGIS and follow the steps above.
* Now import [*ac_contains_village_centroids*](https://github.com/cbgaindia/obi-constituency-data-mapping-pm-kisan/blob/main/Odisha/data/qgis/ac_contains_village_centroids.csv) to Jupyter Notebook and check for duplicates and drop duplicates.
* Now import the file without duplicates [*gis_centroid_no_duplicates*](https://github.com/cbgaindia/obi-constituency-data-mapping-pm-kisan/blob/main/Odisha/results/gis_centroid_no_duplicates.csv), and further *groupby* "AC_NAME" and "AC_NO" and sum the pay values. This generated Assembly Constituency (AC) wise values for PM Kisan pay data
* Perform inner join between [*ac_wise_pm_kisan_odisha*](https://github.com/cbgaindia/obi-constituency-data-mapping-pm-kisan/blob/main/Odisha/results/ac_wise_pm_kisan_odisha.csv) [*ac_pc_geofile_shapefile*](https://github.com/cbgaindia/obi-constituency-data-mapping-pm-kisan/tree/main/Odisha/data/updated). Finally *groupby* "PC_NAME" and "PC_NO" and sum the values. This generated Parliamentary Constituency (PC) wise values for PM Kisan pay data.


## Results

* [Assembly Constituency (AC) wise pay estimates for Odisha](https://github.com/cbgaindia/obi-constituency-data-mapping-pm-kisan/blob/main/Odisha/results/ac_wise_pm_kisan_odisha.csv)
* [Parliamentary Constituency (PC) wise pay estimates for Odisha](https://github.com/cbgaindia/obi-constituency-data-mapping-pm-kisan/blob/main/Odisha/results/pc_wise_pm_kisan.csv)
* [Summary](https://github.com/cbgaindia/obi-constituency-data-mapping-pm-kisan/tree/main/Odisha/summary)
