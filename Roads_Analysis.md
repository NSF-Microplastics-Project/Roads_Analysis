---
title: "CalTrans Roads Analysis"
author: "Skyler Elmstrom"
date: "4/20/2021"
output:
  html_document:
    theme: lumen
    code_download: true
    keep_md: true
---



## Basic Total Road Length

```r
library(sf)
library(IETC)
library(tidyverse)

# Load Risk Regions
SFB.riskregions.z <- "https://github.com/NSF-Microplastics-Project/Risk_Region.shapefile/raw/main/Data/SFB_RiskRegions_20210304_SP.zip"
SFB.riskregions <- IETC::unzipShape(SFB.riskregions.z) # loads GitHub shapefile as an sf object

# Load Summary Table from ArcGIS Export
RoadSummary <- read_csv("Data/ArcGIS_SFBRoadsSummary_20210420.csv") %>% # Road length summary from ArcGIS model
  rename(len_km = SUM_Shape_Length) %>% # change name of km length column
  mutate(len_mi = len_km*0.621371) # add miles column
```


```r
RoadSummary
```

```
## # A tibble: 4 x 4
##    OID_ name              len_km len_mi
##   <dbl> <chr>              <dbl>  <dbl>
## 1     1 Coyote Creek      11159.  6934.
## 2     2 San Francisco Bay 15399.  9568.
## 3     3 San Pablo Bay     11603.  7210.
## 4     4 Suisun Bay         7290.  4530.
```


```r
write_csv(RoadSummary, "Data/Output/SFB_Roads_Summary")
```
