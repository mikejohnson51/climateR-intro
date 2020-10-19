
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Gridded climate data with R

[These notes](https://mikejohnson51.github.io/climateR-intro/) are
prepared for the [UCSB ecodata science
club](https://eco-data-science.github.io/). The goal is to introduce the
concepts of gridded climate data, the process for remote data access,
and workflows for easy data retrieval in R. Specifically, we will cover
the following:

-----

### 1\. Multi-diminsional raster data model:

<img src="img/diminsions.png" width="937" style="display: block; margin: auto;" />
<br><br><br><br>

### 2\. Concepts & workflows for ingesting subsets of remote climate data

<img src="img/cookie-cutter.png" width="759" style="display: block; margin: auto;" />

<br><br><br><br>

### 3\. Example Implementations

The simplest example would answer a question like:

> “What was the temperture and rainfall rate in Florida on Janury
> 1st-3rd, 2010?”

``` r
library(AOI)
library(climateR)
library(rasterVis)

AOI  <- aoi_get(state = "FL")

rain <-  getGridMET(AOI, 
                  param = c("prcp", "tmax"), 
                  startDate = "2010-01-01", 
                  endDate = "2010-01-03")

levelplot(rain$prcp, par.settings = BTCTheme, main = "Rainfall (mm)")
levelplot(rain$tmax, par.settings = BuRdTheme, main = "Maximum Temperture (k)")
```

<img src="README_files/figure-gfm/unnamed-chunk-5-1.png" style="display: block; margin: auto;" /><img src="README_files/figure-gfm/unnamed-chunk-5-2.png" style="display: block; margin: auto;" />

Other examples covered will include:

  - time series extraction at points and sets of points,
  - working with ensemble data from climate projections;
  - basic zonal statistics and
  - raster animation…

<div class="figure" style="text-align: center">

<img src="img/ppt.gif" alt="Hurricane Harvey: Pixel vs. County view" width="49%" height="20%" /><img src="img/ppt2.gif" alt="Hurricane Harvey: Pixel vs. County view" width="49%" height="20%" />

<p class="caption">

Hurricane Harvey: Pixel vs. County view

</p>

</div>

If successful, you will not leave this session as experts at any of
these tasks but will have a grasp on the tools need to implement them
and an understanding of the data models behind them that will allow you
to tackle your own climate-related projects.

-----

### Required libraries

You will need the following libraries to reproduce the content in these
notes:

`sf`, `raster`, `rasterVis`, `ggplot2`, `remotes`, `exactextractr`,
`RNetCDF`, `tidyr`, `dplyr`

all of which are on CRAN and can be installed using
`install.packages()`.

For example:

``` r
install.packages('sf')
```

Additionally, you will need to install `climateR` and `AOI` from github
using `remotes` as they are not on CRAN:

``` r
remotes::install_github("mikejohnson51/AOI")
remotes::install_github("mikejohnson51/climateR")
```
