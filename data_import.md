Data Import
================

This document will show how to import data.

## Import the FAS Litters CSV

\###Notes about paths: We should use relative paths instead of absolute
paths because this makes a project more easily reproducible from any
computer, not just the original machine. I am using relative paths in
this document. Notice that I haven’t installed the entire janitor
package, but I want to be able to use the clean_names function. I can
use this style code to pull just this specific command.

``` r
litters_df = read_csv("data/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): Group, Litter Number, GD0 weight, GD18 weight
    ## dbl (4): GD of Birth, Pups born alive, Pups dead @ birth, Pups survive
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_df = janitor::clean_names(litters_df)
```

## Look at the dataset

``` r
litters_df
```

    ## # A tibble: 49 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>           <chr>      <chr>             <dbl>           <dbl>
    ##  1 Con7  #85             19.7       34.7                 20               3
    ##  2 Con7  #1/2/95/2       27         42                   19               8
    ##  3 Con7  #5/5/3/83/3-3   26         41.4                 19               6
    ##  4 Con7  #5/4/2/95/2     28.5       44.1                 19               5
    ##  5 Con7  #4/2/95/3-3     <NA>       <NA>                 20               6
    ##  6 Con7  #2/2/95/3-2     <NA>       <NA>                 20               6
    ##  7 Con7  #1/5/3/83/3-3/2 <NA>       <NA>                 20               9
    ##  8 Con8  #3/83/3-3       <NA>       <NA>                 20               9
    ##  9 Con8  #2/95/3         <NA>       <NA>                 20               8
    ## 10 Con8  #3/5/2/2/95     28.5       <NA>                 20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
head(litters_df)
```

    ## # A tibble: 6 × 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>         <chr>      <chr>             <dbl>           <dbl>
    ## 1 Con7  #85           19.7       34.7                 20               3
    ## 2 Con7  #1/2/95/2     27         42                   19               8
    ## 3 Con7  #5/5/3/83/3-3 26         41.4                 19               6
    ## 4 Con7  #5/4/2/95/2   28.5       44.1                 19               5
    ## 5 Con7  #4/2/95/3-3   <NA>       <NA>                 20               6
    ## 6 Con7  #2/2/95/3-2   <NA>       <NA>                 20               6
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
tail(litters_df)
```

    ## # A tibble: 6 × 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>         <chr>      <chr>             <dbl>           <dbl>
    ## 1 Low8  #79           25.4       43.8                 19               8
    ## 2 Low8  #100          20         39.2                 20               8
    ## 3 Low8  #4/84         21.8       35.2                 20               4
    ## 4 Low8  #108          25.6       47.5                 20               8
    ## 5 Low8  #99           23.5       39                   20               6
    ## 6 Low8  #110          25.5       42.7                 20               7
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
view(litters_df)
```

\##Learning assessment

Use relative paths

``` r
pups_df = read_csv("data/FAS_pups.csv")

pups_df = janitor::clean_names(pups_df)
```

\##Look at read_csv options Skip can be used to skip first few rows, in
case people have added unnecessary information there

``` r
litters_df=
  read_csv(
    file = "data/FAS_litters.csv",
    skip = 1 
  )
```

    ## New names:
    ## Rows: 48 Columns: 8
    ## ── Column specification
    ## ──────────────────────────────────────────────────────── Delimiter: "," chr
    ## (4): Con7, #85, 19.7, 34.7 dbl (4): 20, 3...6, 4, 3...8
    ## ℹ Use `spec()` to retrieve the full column specification for this data. ℹ
    ## Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## • `3` -> `3...6`
    ## • `3` -> `3...8`

What about missing data? Here is a quick way to make missing values
uniform in your dataset.

``` r
litters_df=
  read_csv(
    file = "data/FAS_litters.csv",
    na = c("NA", "", ".")
  )
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

What if we code ‘group’ as a factor variable?

``` r
litters_df = 
  litters_df=
  read_csv(
    file = "data/FAS_litters.csv",
    na = c("NA", "", "."), 
    col_types = cols(
      Group = col_factor()
    )
)
```

## Import an excel file

Import MLB 2011 summary data. Sheet and range (not included below) are
functions specific to read_excel. Range is helpful because you can pull
just a portion of the dataset.

``` r
mlb_df = read_excel("data/mlb11.xlsx", sheet = "mlb11")
```

## Import SAS data

``` r
pulse_df = read_sas("data/public_pulse_data.sas7bdat")
```

## Never use read.csv(). This will give you a dataframe rather than a tibble, which is what you get with read_csv. The latter is also more memory efficient, and that will become evident down the line.

``` r
litters_df = read.csv("data/FAS_litters.csv")
```

Never do this either:

``` r
litters_df$L
```

    ##  [1] "#85"             "#1/2/95/2"       "#5/5/3/83/3-3"   "#5/4/2/95/2"    
    ##  [5] "#4/2/95/3-3"     "#2/2/95/3-2"     "#1/5/3/83/3-3/2" "#3/83/3-3"      
    ##  [9] "#2/95/3"         "#3/5/2/2/95"     "#5/4/3/83/3"     "#1/6/2/2/95-2"  
    ## [13] "#3/5/3/83/3-3-2" "#2/2/95/2"       "#3/6/2/2/95-3"   "#59"            
    ## [17] "#103"            "#1/82/3-2"       "#3/83/3-2"       "#2/95/2-2"      
    ## [21] "#3/82/3-2"       "#4/2/95/2"       "#5/3/83/5-2"     "#8/110/3-2"     
    ## [25] "#106"            "#94/2"           "#62"             "#84/2"          
    ## [29] "#107"            "#85/2"           "#98"             "#102"           
    ## [33] "#101"            "#111"            "#112"            "#97"            
    ## [37] "#5/93"           "#5/93/2"         "#7/82-3-2"       "#7/110/3-2"     
    ## [41] "#2/95/2"         "#82/4"           "#53"             "#79"            
    ## [45] "#100"            "#4/84"           "#108"            "#99"            
    ## [49] "#110"
