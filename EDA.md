EDA
================
Nicki Lentz
23/2/2021

-   [Import data](#import-data)

# Import data

``` r
jump <- read_csv("../data/Testdata_Catapult/Hop_IMU.csv", skip = 6)
head(jump)
```

    ## # A tibble: 6 x 14
    ##   `Period;Ticks;D~ Acceleration.fo~ Acceleration.si~ Acceleration.up
    ##   <chr>                       <dbl> <chr>            <chr>          
    ## 1 Hop;0;23-02-202~                0 989295959472656  0              
    ## 2 Hop;1;23-02-202~                0 972355961799622  0              
    ## 3 Hop;2;23-02-202~                0 955899953842163  0              
    ## 4 Hop;3;23-02-202~                0 947671949863434  0              
    ## 5 Hop;4;23-02-202~                0 934119999408722  0              
    ## 6 Hop;5;23-02-202~                0 921051979064941  0              
    ## # ... with 10 more variables: Rotation.roll <chr>, Rotation.pitch <chr>,
    ## #   Rotation.yaw <chr>, Facing <chr>, imuOrientation.forward <chr>,
    ## #   imuOrientation.side <dbl>, imuAcceleration.forward <chr>,
    ## #   imuAcceleration.side <dbl>, imuAcceleration.up <chr>, `Acceleration
    ## #   Magnitude` <chr>
