Fish Analysis
================
Ellen Bledsoe
2025-04-03

# Fish Length Analysis

Analysis fish length data from Gaeta et al.

### Set-Up

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ✔ purrr     1.0.4     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
fish <- read_csv("data_raw/Gaeta_etal_CLC_data.csv")
```

    ## Rows: 4033 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): lakeid, annnumber
    ## dbl (4): fish_id, length, radii_length_mm, scalelength
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
glimpse(fish)
```

    ## Rows: 4,033
    ## Columns: 6
    ## $ lakeid          <chr> "AL", "AL", "AL", "AL", "AL", "AL", "AL", "AL", "AL", …
    ## $ fish_id         <dbl> 299, 299, 299, 300, 300, 300, 300, 301, 301, 301, 301,…
    ## $ annnumber       <chr> "EDGE", "2", "1", "EDGE", "3", "2", "1", "EDGE", "3", …
    ## $ length          <dbl> 167, 167, 167, 175, 175, 175, 175, 194, 194, 194, 194,…
    ## $ radii_length_mm <dbl> 2.697443, 2.037518, 1.311795, 3.015477, 2.670733, 2.13…
    ## $ scalelength     <dbl> 2.697443, 2.697443, 2.697443, 3.015477, 3.015477, 3.01…

``` r
fish %>% 
  group_by(lakeid) %>% 
  summarize(min_scale_length = min(scalelength, na.rm = T),
            max_scale_length = max(scalelength, na.rm = T))
```

    ## # A tibble: 16 × 3
    ##    lakeid min_scale_length max_scale_length
    ##    <chr>             <dbl>            <dbl>
    ##  1 AL                2.70              8.71
    ##  2 AR                2.01              6.71
    ##  3 BO                1.43              7.23
    ##  4 BR                2.07              7.95
    ##  5 CR                3.87              5.86
    ##  6 DY                1.68              6.28
    ##  7 FD                2.70              7.36
    ##  8 JN                1.89              7.74
    ##  9 LC                2.46              6.19
    ## 10 LJ                2.40              4.50
    ## 11 LR                2.47              6.52
    ## 12 LSG               0.773             7.14
    ## 13 MN                2.68              7.97
    ## 14 RD                2.28              7.08
    ## 15 UB                1.89              6.80
    ## 16 WS                0.628            11.0
