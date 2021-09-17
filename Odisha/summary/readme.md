## Summary

The PM-Kisan data set has 53786 village codes (‘vill_code’). All the codes are unique.
- Out of these 53786 village codes in the PM-Kisan data set, only 51141 matches with the village codes in the GIS village level boundary data set. The villages code for the remaining 2645 values aren’t present in the GIS village level boundary data set as this dataset is from 2011 census and since then number of villages have changed.

The GIS village level boundary data set has 51310 village codes (‘V_CODE’). Out of which 51303 are unique codes.
- Out of these 51310 village codes in the GIS village level boundary data set, only 51148 matches with the village codes in the PM-Kisan data set. The villages code for the remaining 162 values aren’t present in the GIS village level boundary data set. Further after removing duplicates, 51141 unique village codes are there.

The centroid of each village boundary was generated on QGIS and then the join attributes by location function was used with taking the Assembly Constituency (AC) boundary as the base file and thereafter choosing the ‘contains’ function.
This then generates a new layer with Assembly Constituencies containing the respective centroids
- After performing the village centroid and AC join, the output contains 51311 rows, out of which 51301 unique ‘V_CODE’.In the 51311 unique V_CODE, 3 values are NaN which means the cell contains no value.

- Out of 51311, there are 51146 unique ‘vill_code’ or 'PM_Kisan_merged_vill_code'. There are 165 values of NaN, containing the 3 NaN values from V_CODE and 162 values that were not matching as mentioned in the second point above. This 51146 un

- Further, there are 2 codes that have been missed out from the 51148 unique village codes that were matching between GIS village level boundary data set and PM-Kisan data set. This could be possibly because of some error in the AC boundary file and might have missed out these 2 village centroids.

Therefore the final AC-level estimates are made on the basis of 51138 values. There were 51139 values in the table, out of which which 1 village code is redundant as it has NaN value.  is approximately 95.12 % of the villages from the PM-Kisan data set.
