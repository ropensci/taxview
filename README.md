taxview
=======

[![Project Status: WIP – Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](http://www.repostatus.org/badges/latest/wip.svg)](http://www.repostatus.org/#wip)
[![Build Status](https://travis-ci.org/ropensci/taxview.svg?branch=master)](https://travis-ci.org/ropensci/taxview)

Summarise and visualize data sets from with respect to taxonomy

## install


```r
devtools::install_github("ropensci/taxview")
```


```r
library(taxview)
```

## use

get some data


```r
x <- system.file("examples/plant_spp.csv", package = "taxview")
```

prepare data: clean, etc.


```r
dat <- tibble::as_tibble(
 data.table::fread(x, stringsAsFactors = FALSE, 
   data.table = FALSE))
head(dat)
```

```
## # A tibble: 6 x 2
##                     name      id
##                    <chr>   <int>
## 1       Dianthus engleri 1531994
## 2   Anacolosa frutescens 1618138
## 3 Hymenophyllum plicatum  638568
## 4       Dolichos oliveri 1094718
## 5      Kalanchoe montana  441235
## 6      Caladenia plicata  672428
```

```r
dat_clean <- tv_clean_ids(x, ids = dat$id, db = "ncbi")
head(dat_clean)
```

```
##                 name         rank     id   query
## 1 cellular organisms      no rank 131567 1531994
## 2          Eukaryota superkingdom   2759 1531994
## 3      Viridiplantae      kingdom  33090 1531994
## 4       Streptophyta       phylum  35493 1531994
## 5     Streptophytina    subphylum 131221 1531994
## 6        Embryophyta      no rank   3193 1531994
```

prepare summary


```r
(sumdat <- tv_summarise(dat_clean))
```

```
<tv_summary>
 no. taxa: 129
 by rank: N (21)
 by rank name: N (594)
 within ranks: N (20)
```

visualize (NOT WORKING YET)


```r
tv_viz(sumdat)
```

## Meta

* Please [report any issues or bugs](https://github.com/ropensci/taxview/issues).
* License: MIT
* Get citation information for `taxview` in R doing `citation(package = 'taxview')`
* Please note that this project is released with a [Contributor Code of Conduct](CODE_OF_CONDUCT.md).
By participating in this project you agree to abide by its terms.
