# Impervious Cover, Canopy Cover, and Impaired Waters in Connecticut

This project was created by Chloe Edwards as part of the UKY New Maps Plus Program.

## Project Contents

- [Data Source](#data-source)
- [Project Background](#project-background)
- [Purpose](#purpose)
- [Mapmaking Process](#mapmaking-process)
- [Map Summary](#map-summary)
- [Final Project Link](#final-project-link)


### Data Source

* Connecticut catchment basins with impervious cover percentage and stream flow lines retrieved from internal CT DEEP program data.
* Connecticut lakes, ponds, and ocean polygons retrieved from the [CT Geodata Portal](https://geodata.ct.gov/maps/9a8ee1e074df4c1c9aacd53d4f045750).
* Impaired river and stream segments retrieved from the [2022 Integrated Water Quality Report to Congress](https://portal.ct.gov/DEEP/Water/Water-Quality/Water-Quality-305b-Report-to-Congress).
* Canopy cover raster retrieved from [NOAA](https://coast.noaa.gov/digitalcoast/data/ccaphighres.html). 

* Initial data projection: EPSG:4326 and EPSG:2234
* Final map projection: EPSG:2234

### Project Background

The Impervious Cover Model describes the negative relationships between impervious cover in a watershed and indicators of stream health. 
Watersheds with approximately 10-20% impervious cover are expected to have degraded water quality, while watersheds with greater than 20-25% impervious cover are expected to not support aquatic life.
However, low impervious cover does not necessarily explain water quality parameters (i.e., low IC does not mean good water quality). Other variables are needed to explain water quality when impervious cover is low (Schueler et al, 2009).
Forest canopy cover is one parameter that can help explain water quality. A minimum threshold of 65% canopy cover has been suggested as important for maintaining healthy watersheds (Booth 2000).

![Impervious Cover Model](/graphics/IC-model.png)

### Purpose

The purpose of this map is to visualize watershed characteristics that contribute to stream water quality and streams that are designated as not fully supporting aquatic life.
Watershed catchments are symbolized according to their impervious cover and canopy cover percentage to make implications about water quality.
Stream segments are symbolized according to their Strahler order (width) to provide a sense of scale.
The 2022 aquatic life use assessments are displayed to demonstrate the relationship between watershed characteristics and water quality.

### Mapmaking Process

Based upon the earlier work we did symbolizing roads, I knew that I wanted to symbolize the Strahler order of CT streams. The Strahler number is a way of defining stream size based on the hierarchy of its tributaries. 
Initial stream nodes are assigned a value of 1. The conjunction of two 1 nodes creates a 2 node, and so on. 

![Strahler diagram](/graphics/Strahler.png)

I asked my supervisor at work if we had any datasets that included the Strahler order for CT streams, and she provided me with a dataset that included both stream lines and their individual catchments with associated data.
One of the parameters associated with each catchment was impervious cover percentage. Because this parameter is strongly predictive of stream quality and has been extensively studied, I decided that I wanted to map impervious cover in watershed catchments
and at least one other parameter.

In the first pass of my map, I began by symbolizing streams and their catchments according to Strahler order and impervious cover. I chose the impervious cover color thresholds based upon the revised Impervious Cover Model from Schueler et al, 2009.

![First map](/graphics/progress_1.PNG)

However, I knew that impervious cover wasn't the full story. I then began to research additional factors contributing to water quality, one of which is forest canopy cover. Based upon the Impervious Cover Model, watersheds with 10% and greater impervious cover experience some level of water quality impacts. I decided to symbolize canopy cover percentage for the watershed catchments that had less than 10% impervious cover - i.e., those that were not experiencing impacts and could be sensitive to degradation. I created a copy of the catchments shapefile with only the catchments that had less than 10% impervious cover. I wanted to work with a smaller dataset due to the processing power needed for the large raster dataset.

I used NOAA's high resolution canopy cover dataset to calculate percent canopy cover for each catchment within Connecticut. Within the raster, I set the values to 0 for absence of canopy and 1 for canopy data. Using the zonal statistics tool, I created two additional columns within the filtered catchments shapefile: a count on the number of pixels, and the sum of the value of the pixels (0 + 1). Because the sum column was only counting canopy cover pixels, this enabled me to calculate the percent canopy cover for each catchment (sum/count) and symbolize the catchments based upon that value.

![Zonal stats](/graphics/zonal.PNG)

Booth 2000 found that 65% canopy cover was supportive of healthy watersheds. I initially symbolized only this value (i.e., transparent for all values <65% and green for all values >65%). I then additionally decided to symbolize catchments with both 65-75% and >75% canopy cover. This was a somewhat arbitrary range chosen to show areas where canopy cover was closer to the threshold of 65% and possibly trending towards falling below that threshold.

![Second map](/graphics/progress_2.PNG)

I decided that I was happy with visualizing these parameters and began to fine-tune the colors and symbology to demonstrate where water quality was bad and where increased urbanization was likely occurring. Overall, I was trying to follow a green = good and red = bad color scheme because it is fairly intuitive. I wanted the overall impression to show:

1. Where water quality was likely very poor (yellow-orange-red colors).
2. Where gaps in the canopy are being created, and where impervious cover is likely increasing (light green to cerulean)
3. Where forest canopy cover is highly dense and continuous (dark green)

![Third map](/graphics/progress_3.png)

### Map summary

Overall, the relationship between impervious cover and stream water quality is very clear based upon this map. It additionally highlights areas that may be highly vulnerable to degradation - e.g. watersheds in the 5-10% impervious cover range that are also close to falling below the canopy cover threshold of 65%. One important takeaway could be the importance of meeting housing and development needs within areas that already have a high impervious cover percentage and avoiding developing areas that are currently maintaining healthy watersheds. 

## Final Project Link


Please view the [final map online](https://c-edwards-eco.github.io/map671final).