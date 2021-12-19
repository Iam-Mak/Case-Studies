# Case Study: How Does a Bike-Share Navigate Speedy Success?

### Cyclistic
In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that
are geotracked and locked into a network of 692 stations across Chicago. <br>
Cyclistic sets itself apart by also offering reclining bikes, hand tricycles, and cargo bikes, making bike-share more inclusive to people with
disabilities and riders who can’t use a standard two-wheeled bike. The majority of riders opt for traditional bikes; about
**8%** of riders use the assistive options. Cyclistic users are more likely to ride for leisure, but about **30%** use them to
commute to work each day. <br>

**Cyclistic’s** has three types of pricing plans: **single-ride passes, full-day passes,
and annual memberships**.Customers who purchase *single-ride* or f*ull-day passes* are referred to as **casual riders**. Customers
who purchase *annual memberships* are **Cyclistic members**.


Company’s future success depends on maximizing the number of annual memberships as annual members are much more profitable than casual riders.

We wants to understand how casual riders and annual members use Cyclistic bikes differently.

### Goal: Design marketing strategies aimed at converting casual riders into annual members. 

In order to do that, however, we need to better understand how annual members and casual riders differ, why
casual riders would buy a membership, and how digital media could affect their marketing tactics.

### Ask 
These questions will guide the future marketing program:
- 1. How do annual members and casual riders use Cyclistic bikes differently?
- 2. Why would casual riders buy Cyclistic annual memberships?
- 3. How can Cyclistic use digital media to influence casual riders to become members?

### Prepare 
**Data Source:** Previous 12 months (from 12/2020 to 11/2021) of Cyclistic trip data downloaded [here](https://divvy-tripdata.s3.amazonaws.com/index.html)
- 12 csv. Files
- 13 variables

### Process 
Check current data frames first to see what transformations need to be done before combining.<br>
Cleaning and preparing for Analysis
- Remove all latitude and longitude 
- Calculate the "ride_length" and add a new column (covert ride length data type to numeric) <br>  `total rows = 5479096 & total column = 10`  <br> `total casual riders = 2489347 & total member riders = 2989749`
- Remove trips that the ride length is <= 0 or more than one day (4986 rows removed) <br> `cleaned total rows = 5474110 ` 
- Add columns that list the month, day day of week and year of each ride.

### Analyze

#### 1. Stations 
#### top 10 popular stations
|  S no.       |stations   | station_count|
|--------|----------|---------|
| 1 |Streeter Dr & Grand Ave  |  163969|
| 2| Michigan Ave & Oak St     |   88698|
| 3 |Wells St & Concord Ln      |  86307|
| 4 |Millennium Park           |   83629|
| 5 |Clark St & Elm St         |  81013|
| 6| Wells St & Elm St         |  74092|
| 7 |Theater on the Lake       | 73946|
| 8 |Clark St & Lincoln Ave    |   66105|
| 9 |Wabash Ave & Grand Ave    |  65024|
|10 |Clark St & Armitage Ave      | 64756|


#### top 10 popular stations for casual riders 
|  S no.       |stations   | station_count|
|--------|----------|---------|
|1| Streeter Dr & Grand Ave |          133317|
| 2 |Millennium Park      |              67090|
 |3| Michigan Ave & Oak St |             60651|
 |4| Theater on the Lake   |             44065|
| 5 |Shedd Aquarium      |               43628|
| 6 |Wells St & Concord Ln  |            39067|
| 7 |Lake Shore Dr & Monroe St|          38712|
| 8 |Clark St & Lincoln Ave    |         34024|
 |9| Wabash Ave & Grand Ave    |         32816|
|10| Indiana Ave & Roosevelt Rd  |       32792|


#### top 10 popular stations for member riders
|  S no.       |stations   | station_count|
|--------|----------|---------|
|1 |Clark St & Elm St  |              49146|
 |2| Wells St & Concord Ln   |         47240|
|3 |Kingsbury St & Kinzie St  |       45718|
| 4| Wells St & Elm St     |           41926|
| 5 |Dearborn St & Erie St  |          39551|
 |6| Wells St & Huron St    |          37287|
 |7 |St. Clair St & Erie St   |        37039|
| 8| Broadway & Barry Ave     |        36059|
 |9| Clinton St & Madison St |         33273|
|10| Clark St & Armitage Ave  |        32785|

#### 2. Descriptive Analysis on Ride Length
| Min.     |  1st Qu.|    Median  |    Mean |  3rd Qu.  |    Max. |
|----------|---------|------------|---------|-----------|---------|
|  0.0167  |  6.8333 |  12.1167 |  19.6732 |  21.9667 |1439.9500|
