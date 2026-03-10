# Thiessen-Polygon
This code was created original to implement Thiessen polygons for intermittent rain gauges by Paola Sabel and Hilary McMillan at San Diego State University, Department of Geography.

To use the code, you need three files:
1. A shapefile of your watershed outline
2. A shapefile of your rain gauges (they must be within the watershed boundary)
3. A csv file of precipitation data from the rain gauges.  The file format should be strictly as follows: a DateTime column and one column for each rain gauge with the header as 'RG#" where the # corresponds to the rain gauge number.  All gaps in precipitation should be marked as NaN.

The code will determine which rain gauges are active at the same time and create a column in your dataframe called which_gauge.  False indicates the gauge is active and true indicates the gauge is inactive.

Then the code will determine how many different active/inactive combinations there are and create a column in your dataframe called which_gauge_set.  This corresponds to the unique set of active gauges.

The code will then initialize standard thiessen polygon calculations for each gauge set by determining area fractions for each rain gauge.  After, the gauge set area fractions will be spatially joined with the precipitation data and a new column called weighted_precip will be added to the dataframe.  The weighted_precip column is the new precipitation value at each timestep as determined by multiplying the area fraction for each gauge in each gauge set by its recorded precipitation value.

Finally, the code will merge back in the DateTime column from the original csv file.

Two sets of figures will be created.  The first set is a map of the thiessen polygons for each gauge set.  The second is a map of the thiessen polygons for each guage set and includes a table of the area fractions used to calculate the weighted_precip.
