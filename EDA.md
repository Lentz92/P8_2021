EDA
================
Nicki Lentz
23/2/2021

-   [Import data](#import-data)
-   [Integrate data](#integrate-data)

# Import data

``` r
#skip først 6 linjer for at fjerne basal info der alle står i 1 kollone
df <- read_csv("../data/Testdata_Catapult/Hop_IMU.csv", skip = 6)


df <- df %>%
  separate(1, into = c("type", "ticks", "datetime", "timestamp"), sep = ";") %>% 
  mutate(timestamp = as.numeric(hms(timestamp))) %>% 
  mutate_if(is.character,as.numeric)

#Filter
bf <- signal::butter(n = 2, W = 12 / (100/2), type = "low") #W = fc / (fs/2)

data_to_filter <- df %>% 
  select(contains("."))


df_filtered <- NULL
for (col in 1:length(data_to_filter)) {
  
  filtdata = signal::filtfilt(bf, data_to_filter[[col]])
  df_filtered = cbind(df_filtered, filtdata)
  
}
df_filtered <- as_tibble(df_filtered)
colnames(df_filtered) = colnames(df)
df_filtered["time"] <- df$timestamp

df_filtered %>% 
  ggplot(aes(time, Acceleration.side)) + 
  geom_line() + 
  labs(x = "time [s]", 
       y = "Acceleration",
       title = "Side movement")
```

![](EDA_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

# Integrate data
