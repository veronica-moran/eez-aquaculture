# Potential Aquaculture in West Coast Exclusive Economic Zones
## Oysters and Pacific calico scallops

## Purpose

This repository contains a spatial analysis of potential aquaculture habitat within West Coast Exclusive Economic Zone (EEZ) regions. Species-specific sea surface temperature and depth requirements were used to estimate suitable habitat for oysters and Pacific calico scallops and compare total suitable area for EEZ regions.

## Data

### Data Access 

Temperature and depth suitable ranges for the Pacific calico scallop were obtained from the [SeaLifeBase website](https://www.sealifebase.ca/search.php?__cf_chl_tk=dcPyoh_45Iaw0CJFNn99f7C3VRL3d8fprSGSM7dbyY4-1794201298-1.0.1.1-X51KmLlZhcEOIGMnNls7ti8ydyLM.wHWBIRZtwkrn3U).

Sea surface temperature (SST) data, annual averages in Kelvin, for the years 2008-2012 was originally generated from [NOAA’s 5km Daily Global Satellite Sea Surface Temperature Anomaly v3.1](https://coralreefwatch.noaa.gov/product/5km/index_5km_ssta.php).

Bathymetry data was obtained from the [General Bathymetric Chart of the Oceans (GEBCO)](https://www.gebco.net/data-products/gridded-bathymetry-data#area).

Boundary data for the West Coast Exclusive Economic Zone was obtained from [Marineregions.org](https://www.marineregions.org/eez.php).

### Data Organization

EEZ-AQUACULTURE
└─── README.md
└─── eez-aquaculture.qmd
└─── .gitignore
    └───data
        └─── wc_regions_clean.shp
        └─── depth.tif
        └─── average_annual_sst_2008.tif
        └─── average_annual_sst_2009.tif
        └─── average_annual_sst_2010.tif
        └─── average_annual_sst_2011.tif
        └─── average_annual_sst_2012.tif

**Libraries:**

```r
library(tidyverse)
library(sf)
library(here)
library(tmap)
```

Project Variables
- Mean sea surface temperature from 2008–2012 (mean_sst)
- Bathymetry raster resampled to match the SST raster (depth_resampled)
- West Coast EEZ region boundaries (regions)
- Species-specific minimum and maximum SST (min_sst, max_sst)
- Species-specific minimum and maximum depth (min_depth, max_depth)
- Species name used in map output (species_name)
- Function used to calculate and map suitable habitat by EEZ region (suitable_eez())

Data Processing
Annual SST rasters were stacked and averaged, then converted from Kelvin to degrees Celsius. Bathymetry data were cropped and resampled to match the extent, resolution, and alignment of the mean SST raster. EEZ polygons were rasterized using region IDs, and raster cell areas were calculated in square kilometers.

Species-specific SST and depth ranges were used to reclassify raster cells as suitable or unsuitable. Cells meeting both temperature and depth requirements remained suitable, Suitable habitat area was summed within each EEZ region. The totals were joined to the EEZ polygons and mapped to compare suitable aquaculture habitat among regions.

## Author
Veronica Moran

Master of Environmental Data Science (MEDS), UC Santa Barbara

## References

[1] NOAA Fisheries. (n.d.). *Aquaculture*. National Oceanic and Atmospheric Administration. https://www.fisheries.noaa.gov/topic/aquaculture [Accessed November 7, 2026]

[2] National Centers for Coastal Ocean Science. (2021, October 19). *Aquaculture opportunity areas for federal waters of the United States Exclusive Economic Zone*. National Oceanic and Atmospheric Administration. https://coastalscience.noaa.gov/project/aquaculture-opportunity-areas-for-federal-waters-of-the-united-states-exclusive-economic-zone/ [Accessed November 7, 2026]

[3] Gentry, R. R., Froehlich, H. E., Grimm, D., Kareiva, P., Parke, M., Rust, M., Gaines, S. D., & Halpern, B. S. (2017). *Mapping the global potential for marine aquaculture*. *Nature Ecology & Evolution, 1*, 1317–1324. https://doi.org/10.1038/s41559-017-0257-9

[4] National Oceanic and Atmospheric Administration. (2026, September 23). *What is the EEZ?* National Ocean Service. https://oceanservice.noaa.gov/facts/eez.html [Accessed November 7, 2026]