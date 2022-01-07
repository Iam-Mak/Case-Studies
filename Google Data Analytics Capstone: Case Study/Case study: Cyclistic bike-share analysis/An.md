library(tidyverse)
library(lubridate)

df1 <- read.csv("D:\\Bike Share Dataset\\dec_20.csv")
df2 <- read.csv("D:\\Bike Share Dataset\\jan_21.csv")
df3 <- read.csv("D:\\Bike Share Dataset\\feb_21.csv")
df4 <- read.csv("D:\\Bike Share Dataset\\mar_21.csv")
df5 <- read.csv("D:\\Bike Share Dataset\\apr_21.csv")
df6 <- read.csv("D:\\Bike Share Dataset\\may_21.csv")
df7 <- read.csv("D:\\Bike Share Dataset\\jun_21.csv")
df8 <- read.csv("D:\\Bike Share Dataset\\jul_21.csv")
df9 <- read.csv("D:\\Bike Share Dataset\\aug_21.csv")
df10 <- read.csv("D:\\Bike Share Dataset\\sep_21.csv")
df11<- read.csv("D:\\Bike Share Dataset\\oct_21.csv")
df12 <- read.csv("D:\\Bike Share Dataset\\nov_21.csv")




df1 <- mutate(df1, start_station_id = as.character(start_station_id), 
                   end_station_id = as.character(end_station_id))
df2 <- mutate(df2, start_station_id = as.character(start_station_id), 
              end_station_id = as.character(end_station_id))
df3 <- mutate(df3, start_station_id = as.character(start_station_id), 
              end_station_id = as.character(end_station_id))
df4 <- mutate(df4, start_station_id = as.character(start_station_id), 
              end_station_id = as.character(end_station_id))
df5 <- mutate(df5, start_station_id = as.character(start_station_id), 
              end_station_id = as.character(end_station_id))
df6 <- mutate(df6, start_station_id = as.character(start_station_id), 
              end_station_id = as.character(end_station_id))
df7 <- mutate(df7, start_station_id = as.character(start_station_id), 
              end_station_id = as.character(end_station_id))
df1 <- mutate(df1, start_station_id = as.character(start_station_id), 
              end_station_id = as.character(end_station_id))
df8 <- mutate(df8, start_station_id = as.character(start_station_id), 
              end_station_id = as.character(end_station_id))
df9 <- mutate(df9, start_station_id = as.character(start_station_id), 
              end_station_id = as.character(end_station_id))
df10 <- mutate(df10, start_station_id = as.character(start_station_id), 
              end_station_id = as.character(end_station_id))
df11 <- mutate(df11, start_station_id = as.character(start_station_id), 
              end_station_id = as.character(end_station_id))
df12 <- mutate(df12, start_station_id = as.character(start_station_id), 
              end_station_id = as.character(end_station_id))

bike_rides <- rbind(df1,df2,df3,df4,df5,df6,df7,df8,df9,df10,df11,df12)


# Remove all latitude and longitude
bike_rides <- bike_rides %>% 
  select(-c(start_lat, start_lng, end_lat, end_lng))


bike_rides$started_at <- ymd_hms(bike_rides$started_at)
bike_rides$ended_at <- ymd_hms(bike_rides$ended_at)

bike_rides$ride_length <- difftime(time1 =bike_rides$ended_at,time2 =bike_rides$started_at,units = "mins")


# Inspect the new table created (multiple ways)
colnames(bike_rides) # list of column names
nrow(bike_rides) # how many roaws are in the data frame
dim(bike_rides) # dimensions of the data frame
head(bike_rides) # see the first 6 rows
str(bike_rides) # see list of columns and data types
summary(bike_rides) # statistical summary of the data (mainly for numeric data)


# How many observations fall under each rider type?
table(bike_rides$member_casual)

bike_rides$ride_length <- as.numeric(as.character(bike_rides$ride_length))


# Remove trips that the ride length is <= 0 or more than one day (24 * 60 = 1440 minutes)
# Make a copy for the cleaned data frame
 bike_rides_cl <- bike_rides[!(bike_rides$ride_length > 1440 | bike_rides$ride_length <= 0),]
 
 # Add columns that list the date, month, day, and year of each ride
bike_rides_cl$date <- as.POSIXct(bike_rides_cl$started_at)

bike_rides_cl$month <- format(as.Date(bike_rides_cl$date), "%B")
bike_rides_cl$day <- format(as.Date(bike_rides_cl$date), "%d")
bike_rides_cl$year <- format(as.Date(bike_rides_cl$date), "%Y")
bike_rides_cl$day_of_week <- format(as.Date(bike_rides_cl$date), "%a")


# Combine start and end stations)


all_stations <- bind_rows(data.frame("stations" = bike_rides_cl$start_station_name,
"member_casual" = bike_rides_cl$member_casual), 
data.frame("stations" = bike_rides_cl$end_station_name,
"member_casual" = bike_rides_cl$member_casual))

# Removing entries with no station name
all_stations_cl <- all_stations[!(all_stations$stations == "" | is.na(all_stations$stations)),]


# Separate the data frame by rider type
all_stations_member <- all_stations_cl[all_stations_cl$member_casual == 'member',]
all_stations_casual <- all_stations_cl[all_stations_cl$member_casual == 'casual',]

# Get the top 10 popular stations all, members, and casual riders
top_10_station <- all_stations_cl %>% 
  group_by(stations) %>% 
  summarise(station_count = n()) %>% 
  arrange(desc(station_count)) %>% 
  slice(1:10)

top_10_station_member <- all_stations_member %>% 
  group_by(stations) %>% 
  summarise(station_count = n()) %>% 
  arrange(desc(station_count)) %>% 
  head(n=10)


top_10_station_casual <- all_stations_casual %>% 
  group_by(stations) %>% 
  summarise(station_count = n()) %>% 
  arrange(desc(station_count)) %>% 
  head(n=10)
  
# Top 20 start stations for casual riders
bike_rides_cl %>% 
  group_by(start_station_name, member_casual) %>% 
  summarize(number_of_rides = n(), .groups = 'drop') %>% 
  filter(start_station_name != "", member_casual != "member") %>% 
  arrange(-number_of_rides) %>% 
  head(n=20)
  
  
  #ride_length
  summary(bike_rides_cl$ride_length)
  
  
  # Compare ride length between members and casual riders
aggregate(bike_rides_cl$ride_length ~ bike_rides_cl$member_casual, FUN = mean)

aggregate(bike_rides_cl$ride_length ~ bike_rides_cl$member_casual, FUN = median)

aggregate(bike_rides_cl$ride_length ~ bike_rides_cl$member_casual, FUN = max)

aggregate(bike_rides_cl$ride_length ~ bike_rides_cl$member_casual, FUN = min)


# By Day

# Put days of the week in order
bike_rides_cl$day_of_week <- ordered(bike_rides_cl$day_of_week, 
                                    levels = c("Mon", 
                                               "Tue", "Wed",
                                               "Thu", "Fri", "Sat", "Sun"))
aggregate(bike_rides_cl$ride_length ~ bike_rides_cl$member_casual + bike_rides_cl$day_of_week, FUN = mean)

aggregate(bike_rides_cl$ride_length ~ bike_rides_cl$member_casual + bike_rides_cl$day_of_week, FUN = median)

bike_rides_cl %>% 
  group_by(member_casual, day_of_week) %>% 
  summarise(number_of_rides = n(), .groups = 'drop') %>% 
  arrange(day_of_week)
  
df["Column Name"][df["Column Name"] == "Old Value"] <- "New Value"
bike_rides_cl["month"][bike_rides_cl["month"] == " "] <- "October"
  
#By Month

bike_rides_cl$month <- ordered(bike_rides_cl$month, 
                              levels = c("January", "February", "March",
                                         "April", "May", "June",
                                         "July", "August", "September",
                                         "October", "November", "December"))

aggregate(bike_rides_cl$ride_length ~ bike_rides_cl$member_casual + bike_rides_cl$month, FUN = mean)

aggregate(bike_rides_cl$ride_length ~ bike_rides_cl$member_casual + bike_rides_cl$month, FUN = median)

View(bike_rides_cl %>% 
  group_by(member_casual, month) %>% 
  summarise(number_of_rides = n(), .groups = 'drop') %>% 
  arrange(month))
  