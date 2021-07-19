# obi-constituency-data-mapping-pm-kisan

Repository for PM Kisan Yojna Village Mapping

Pm Kisan Documentation

The PM-Kisan data set has 53786 village codes (‘vill_code’). All the codes are unique. 
- Out of these 53786 village codes in the PM-Kisan data set, only 51142 matches with the village codes in the GIS village level shapefile data set. The villages code for the remaining 2645 values aren’t present in the GIS village level shapefile data set.

The GIS village level shapefile data set has 51310 village codes (‘V_CODE’). Out of which 51303 are unique codes.
- Out of these 51310 village codes in the GIS village level shapefile data set, only 51148 matches with the village codes in the PM-Kisan data set. The villages code for the remaining 162 values aren’t present in the GIS village level shapefile data set. Further after removing duplicates, 51141 unique village codes are there. 

The centroid of each village boundary was generated on QGIS and then the spatial join function was used with taking the Assembly Constituency (AC) shapefile as the base file and thereafter choosing the ‘contains’ function.
This then generates a new layer with Assembly Constituencies containing the respective centroids
- After performing the village centroid and AC join, the output contains 51257 rows, out of which 51254 unique ‘V_CODE’.In the 51257 unique V_CODE, 3 values are NaN which means the cell contains no value. 
- Out of 51257, there are 51085 unique ‘vill_code’. There are 165 values of NaN, containing the 3 NaN values from V_CODE and 162 values that were not matching as mentioned in the second point above.
- Further, there are 56 codes that have been missed out from the 51141 unique village codes that were matching between GIS village level shapefile data set and PM-Kisan data set. This could be possibly because of the error in the AC boundary file and might have missed out village centroids that are situated close to the state boundary.

Therefore the final AC-level estimates are made on the basis of 51085 values and that is approximately 95 % of the villages from the PM-Kisan data set.
