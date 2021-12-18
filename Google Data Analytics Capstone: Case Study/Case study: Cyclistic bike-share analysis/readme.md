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
- Add columns that list the month and day of each ride.
- Calculate the "ride_length" and add a new column
- Remove trips that the ride length is <= 0 or more than one day
