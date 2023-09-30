Data Manipulation
================

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

\##Load the faslitter data

``` r
pols_df = read_csv("./hw2data/pols-month.csv") %>% 
 janitor::clean_names() %>% 
 separate(mon, into = c("year", "month", "day")) %>% 
 mutate(month = recode(month, `01` = "jan", `02` = "feb",`03` = "mar", `04` = "apr", `05` = "may", `06` = "jun", `07` = "jul", `08` = "aug", `09` = "sep", `10` = "oct", `11` = "nov", `12` = "dec" )) %>% 
 mutate(president = prez_dem + prez_gop) %>% 
 select(-day)
```

    ## Rows: 822 Columns: 9
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## dbl  (8): prez_gop, gov_gop, sen_gop, rep_gop, prez_dem, gov_dem, sen_dem, r...
    ## date (1): mon
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
snp_df = read_csv("./hw2data/snp.csv") %>% 
 janitor::clean_names() %>% 
 separate(date, into = c("year", "month", "day")) %>% 
 mutate(month = recode(month, `1` = "jan", `2` = "feb",`3` = "mar", `4` = "apr", `5` = "may", `6` = "jun", `7` = "jul", `8` = "aug", `9` = "sep", `10` = "oct", `11` = "nov", `12` = "dec" )) %>% 
 arrange(year, month) 
```

    ## Rows: 787 Columns: 2
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): date
    ## dbl (1): close
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
