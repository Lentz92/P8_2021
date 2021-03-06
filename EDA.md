EDA
================
Nicki Lentz
23/2/2021

-   [Import data](#import-data)

# Import data

``` r
#skip først 6 linjer for at fjerne basal info der alle står i 1 kollone
df <- read_csv("../data/Testdata_Catapult/Hop_IMU.csv", skip = 6)


df <- df %>%
  separate(col = 1, into = c("type", "ticks", "datetime", "timestamp"), sep = ";") %>% 
  mutate(timestamp = as.numeric(hms(timestamp))) %>% 
  select(-c(type, datetime)) %>% 
  mutate_if(is.character,as.numeric)

#Create lowpass butterworth filter
bf <- signal::butter(n = 2, W = 12 / (100/2), type = "low") #W = fc / (fs/2)


df_filtered <- df %>% 
  mutate(across(contains("."), ~ signal::filtfilt(bf, .x)))
```

``` r
df_filtered_long <- df_filtered %>% 
  select(c(timestamp, Acceleration.forward, Acceleration.up, Acceleration.side)) %>% 
  filter(Acceleration.up <= 10 & Acceleration.up >= -10) %>% 
  pivot_longer(!timestamp, values_to = "acceleration",
               names_to = "key")


df_filtered_long %>% 
  ggplot(aes(x = timestamp, y = acceleration)) + 
  geom_line() + 
  facet_wrap(~key, scale = "free") +
  labs(title = "filtered data")
```

![](EDA_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->
