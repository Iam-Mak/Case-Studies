# [Case Study: How Does a Bike-Share Navigate Speedy Success?](https://coursera.org/share/15f5b45b498b937f6db43d8c6a73293d)

### Cyclistic
In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that
are geotracked and locked into a network of 692 stations across Chicago. <br>
Cyclistic sets itself apart by also offering reclining bikes, hand tricycles, and cargo bikes, making bike-share more inclusive to people with
disabilities and riders who can’t use a standard two-wheeled bike. The majority of riders opt for traditional bikes; about
**8%** of riders use the assistive options. Cyclistic users are more likely to ride for leisure, but about **30%** use them to
commute to work each day. <br>

![image](https://user-images.githubusercontent.com/92245436/152645111-c81132a4-0f28-499a-8458-6db775d97267.png)


**Cyclistic’s** has three types of pricing plans: **single-ride passes, full-day passes,
and annual memberships**.Customers who purchase *single-ride* or f*ull-day passes* are referred to as **casual riders**. Customers
who purchase *annual memberships* are **Cyclistic members**.


Company’s future success depends on maximizing the number of annual memberships as annual members are much more profitable than casual riders.

We wants to understand how casual riders and annual members use Cyclistic bikes differently.

### Goal: Design marketing strategies aimed at converting casual riders into annual members. 

In order to do that, however, we need to better understand how annual members and casual riders differ, why
casual riders would buy a membership, and how digital media could affect their marketing tactics.

## 1. Ask 
These questions will guide the future marketing program:
- 1. How do annual members and casual riders use Cyclistic bikes differently?
- 2. Why would casual riders buy Cyclistic annual memberships?
- 3. How can Cyclistic use digital media to influence casual riders to become members?

## 2. Prepare 
**Data Source:** Previous 12 months (from 01/2021 to 12/2021) of Cyclistic trip data downloaded [here](https://divvy-tripdata.s3.amazonaws.com/index.html)
- 12 csv. Files
- 13 variables

#### 2.2 Is Data ROCCC?
A good data source is **ROCCC** which stands for **Reliable, Original, Comprehensive, Current,** and **Cited**.

- **Reliable -** *High* - Reliable as it  has 5590394 rows and many riders
- **Original -** *High* - Data is Original
- **Comprehensive** - *High* - We have all needed parameters 
- **Current** - *High* - Data is up to date
- **Cited** - *High* - Source is verified


## 3. Process 
Check current data frames first to see what transformations need to be done before combining.<br>
Cleaning and preparing for Analysis
- Remove all latitude and longitude 
- Calculate the "ride_length" and add a new column (covert ride length data type to numeric) <br>  `total rows = 5595063 & total column = 10`  <br> `total casual riders = 2529005 & total member riders = 3066058`
- Remove trips that the ride length is <= 0 or more than one day (4669 rows removed) <br> `cleaned total rows = 5590394 ` 
- Add columns that list the month, day day of week and year of each ride.

## 4. Analyze

#### 1. Stations 
#### top 10 popular stations
|  S no.       |stations   | station_count|
|--------|----------|---------|
| 1 |Streeter Dr & Grand Ave  |  165976|
| 2| Michigan Ave & Oak St     |   89146|
| 3 |Wells St & Concord Ln      |  87436|
| 4 |Millennium Park           |   85042|
| 5 |Clark St & Elm St         |  81703
| 6| Wells St & Elm St         |  75012|
| 7 |Theater on the Lake       | 73857
| 8 |Clark St & Lincoln Ave    |   66659|
| 9 |Wabash Ave & Grand Ave    |  66517
|10 |Clark St & Armitage Ave      | 65860|


#### top 10 popular stations for casual riders 
|  S no.       |stations   | station_count|
|--------|----------|---------|
|1| Streeter Dr & Grand Ave |          134922|
| 2 |Millennium Park      |              68049|
 |3| Michigan Ave & Oak St |             60941|
 |4| Shedd Aquarium   |                  44778|
| 5 |  Theater on the Lake    |          44086|
| 6 |Wells St & Concord Ln  |            39332|
| 7 |Lake Shore Dr & Monroe St|          37844|
| 8 |Clark St & Lincoln Ave    |         34198|
 |9| Wabash Ave & Grand Ave    |         33213|
|10| Indiana Ave & Roosevelt Rd  |       32962|


#### top 10 popular stations for member riders
|  S no.       |stations   | station_count|
|--------|----------|---------|
|1 |Clark St & Elm St  |               49645|
 |2| Wells St & Concord Ln   |         48104|
|3 |Kingsbury St & Kinzie St  |        47203|
| 4| Wells St & Elm St     |           42658|
| 5 |Dearborn St & Erie St  |          39886|
 |6| Wells St & Huron St    |          38012|
 |7 |St. Clair St & Erie St   |        37763|
| 8| Broadway & Barry Ave     |        36290|
 |9| Clinton St & Madison St |         34265|
|10| Clark St & Armitage Ave  |        33018|

#### 2. Descriptive Analysis on Ride Length (in minutes)
| Min.     |  1st Qu.|    Median  |    Mean |  3rd Qu.  |    Max. |
|----------|---------|------------|---------|-----------|---------|
|  0.0167  |  6.7500 |  11.9833   |  19.4851  |  21.7500  |1439.9500  |

#### Compare ride length between members and casual riders
 |        |casual riders    |  member riders |
 |--------|-----------------|----------------|
 | mean |    26.87448   |  13.39778          | 
|  median |   15.95    |  9.60      |
|max |     1439.917|  1439.950     |
|min |  0.01666667   |  0.01666667     |

#### 3. By Day

 |   |  member_casual |day_of_week| number_of_rides | ride_length (mean)|ride_length (median) | 
 |--|-----------------|-----------|-----------------|-------------------|---------------------|
|1         |        casual       |           Mon |          285928    |        27.23302|    15.933333|
|2         |        member       |           Mon |          416112    |        13.00232|    9.200000 |
|3         |        casual       |           Tue |           274033   |        24.49926|    14.266667|
|4         |        member       |           Tue |           465417   |        12.60718|    9.133333 |
|5         |        casual       |           Wed |            278582  |        23.28661|   13.950000|
|6         |        member       |           Wed |           477066   |        12.66144|     9.216667|
|7         |        casual       |           Thu |          285667    |        23.16266|   13.766667|
|8         |        member       |           Thu |          451425    |        12.56334|    9.133333|
|9         |        casual       |           Fri |         363542     |        24.94070|   14.950000|
|10        |        member       |           Fri |         446315     |        13.09665|    9.433333|
|11        |        casual       |           Sat |         557135     |        29.20509|   17.783333|
|12        |        member       |           Sat |          432928    |        14.97082|   10.816667|
|13        |       casual        |           Sun |           480250   |        31.06556|   18.683333|
|14        |       member        |          Sun  |          375994   |         15.29637|   10.866667|

#### 4. By month

 |   |  member_casual |month| number_of_rides | ride_length (mean)|ride_length (median) | 
 |--|-----------------|-----------|-----------------|-------------------|---------------------|
|1         |        casual       |           Jan |          18090    |        21.38846|    12.266667|
|2         |        member       |           Jan |          78701    |        12.68486|    8.700000 |
|3         |        casual       |           Feb |           10072   |        30.33581|    16.033333|
|4         |        member       |           Feb |           39429  |        15.80857|    10.116667 |
|5         |        casual       |           Mar |            83876  |        31.42597|   18.683333|
|6         |        member       |           Mar |           144446   |        13.86716|     9.983333|
|7         |        casual       |           Apr |          136359   |        31.10665|   18.000000|
|8         |        member       |           Apr |          200578    |        14.51371|    10.400000|
|9         |        casual       |           May |         256480    |        31.63273|  18.716667|
|10        |        member       |           May |         274657     |        14.45722|   10.483333|
|11        |        casual       |           Jun |          370035    |        29.36513|   17.333333|
|12        |       member        |           Jun |           358829   |        14.41389|   10.616667|
|13        |       casual        |           Jul |           441446   |        27.51916|   16.683333|
|14        |       member        |           Jul |          380271  |         14.06131|   10.433333|
|15        |        casual       |           Aug |          412154    |        26.33230|    16.083333|
|16        |        member       |           Aug |          391576    |        13.87134|    10.150000 |
|17        |        casual       |           Sep |           363482   |        25.24353|    15.350000|
|18        |        member       |           Sep |           392143   |        13.52070|    9.783333 |
|19        |        casual       |           Oct |            256814  |        22.85920|   13.700000|
|20        |        member       |           Oct |           373887  |        12.24078|     8.650000|
|21        |        casual       |           Nov |          106735   |        18.72995|   11.233333|
|22        |        member       |           Nov |          252972    |        11.09886|    7.666667|
|23        |        casual       |           Dec |         69594    |        18.19083|   10.933333|
|24        |        member       |           Dec |         177768     |        10.82142|    7.616667|


## 5. Share 
#### Creating Data Visualizations

#### 1. Top 10 stations (casual riders)

![image](https://user-images.githubusercontent.com/92245436/148542472-45e6671b-5187-4b29-834d-59a042675e4f.png)


#### 2. Top 10 stations (members)


![image](https://user-images.githubusercontent.com/92245436/148542174-a6fba308-20a9-4e7c-9acf-bab454ed8a34.png)

#### 3. Top 10 start stations (casual riders)

![image](https://user-images.githubusercontent.com/92245436/148542751-7fa9df16-04cd-468d-95d2-843d5b459698.png)


#### 4. Average riding duration between members and casual riders


![image](https://user-images.githubusercontent.com/92245436/148539225-ed358d8b-5d31-4766-9af8-6b8b6f20f7da.png)

#### 5. Average riding duration of each day of week between members and casual riders

![image](https://user-images.githubusercontent.com/92245436/148540228-cd0045eb-bc1a-4142-b6af-d4a42d52ee8f.png)

#### 6. Average number of rides of each day of week between members and casual riders
![image](https://user-images.githubusercontent.com/92245436/148540433-3af80410-9b30-401c-8484-00bb7f0de801.png)

#### 7. Average number of rides by month (casual riders)
![image](https://user-images.githubusercontent.com/92245436/148541153-8a9f916f-5111-458e-88c6-27db394e1968.png)

#### 8. Average number of rides by hour (casual riders)
![image](https://user-images.githubusercontent.com/92245436/148541718-e61b88d7-9651-4aa0-bd10-eb72abe17e2d.png)


#### 9. Number of rides between members and casual riders by day of week across the year


![image](https://user-images.githubusercontent.com/92245436/148543151-ce25e300-553d-4e6e-b233-8c718457f309.png)


### Key Findings
- On weekends, casual riders' demand on bikes are larger than members.
- Casual riders prefer to take longer trips averaging 26 minutes per trip compared to members who average only 13 minutes.
- Average trip duration of casual riders is more than twice that of member rider over any given day of the week cumulatively.
- During the day, averagely, **12 PM to 7 PM** is the peak time when number of rides of casual riders are greater than 150K.
- Top three start stations for casual riders are **1) Streeter Dr & Grand Ave**, **2) Millennium Park** **3) Michigan Ave & Oak St**

## 6. Act
### 6.1 Recommendations
- Saturday is effective in case of casual riders whereas it is the most effective day for marketing and we can bring some discount or promotion package.
- In July there is a peak in numbers of rides so promotion and packages for membership is recommended at that time.
- We can introduce Weekend Pass for casual riders as we have more casual riders on weekend.
- Offer discounted pricing during non-busy hours so that casual riders might choose to use bikes more often and level out demand over the day.
- We can introduce Premium Pass service for Bike reservation during peek Biking seasons.
