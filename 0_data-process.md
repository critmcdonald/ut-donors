Combining donor lists
================

Data preparation
----------------

-   We are starting with an Excel spreadsheet `data-raw/Donor_History_responsive - no id.xlsx`. It is a list of donations to the University of Texas over a 10-year period, acquired by UT Austin student Carlos Garcia through an open records request.
-   The spreadsheet has three sheets: "Part 1", "Part 2" and "Part 3"
-   Our goal here is to combine the three sheets into a single CSV file.

### Install package

These are the packages required for this notebook, commented out in case they are already installed.

``` r
# install.packages("tidyverse")
# install.packages("readxl")
# install.packages("lubridate")
# install.packages("rmarkdown")
```

### Load necesary packages

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.1.0     ✔ purrr   0.2.5
    ## ✔ tibble  1.4.2     ✔ dplyr   0.7.6
    ## ✔ tidyr   0.8.2     ✔ stringr 1.3.1
    ## ✔ readr   1.1.1     ✔ forcats 0.3.0

    ## ── Conflicts ────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(readxl)
library(lubridate)
```

    ## 
    ## Attaching package: 'lubridate'

    ## The following object is masked from 'package:base':
    ## 
    ##     date

### Import the three sheets as dataframes

``` r
part1 <- read_excel("data-raw/Donor_History_responsive - no id.xlsx", sheet = "Part 1")
part2 <- read_excel("data-raw/Donor_History_responsive - no id.xlsx", sheet = "Part 2")
part3 <- read_excel("data-raw/Donor_History_responsive - no id.xlsx", sheet = "Part 3")
```

### Merge the three dataframes

``` r
combined <- rbind(part1, part2, part3) %>% 
  mutate(DONATION_DATE = dmy(DONATION_DATE))
```

### Export as csv

``` r
combined %>% write_csv("data-done/donors.csv")
```
