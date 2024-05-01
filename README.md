# On-Time Flight Performance Analysis: Elko Regional Airport
For this project, I used MySQL Workbench, Lucidchart, and Microsoft Excel to create a database and analyze data that I created based on datasets from the National Centers for Environmental Information, Hadley Wickham’s nycflights13 package, and FlightAware’s live geospatial Flight Tracker. The Elko Regional Airport, a small airport in Elko, Nevada, wants to automate its data management system. The problem is that they want to track how weather conditions affect flight delays and present their findings to the National Centers for Environmental Information: National Oceanic and Atmospheric Administration. They have over 10,787 weather observations in total with approximately 15 airplanes departing from the Elko Regional Airport each day. Due to the large number of flights and weather conditions at the Elko Regional Airport, I had to create 12 records. Using Microsoft Excel, I created a shorter version where I come up with 12 fictional flights based on the actual times it takes for planes to reach any destination from Elko.

# Synopsis
The Elko Regional Airport, a small airport in Elko, Nevada, wants to automate its data management system. They want to organize their local climatological data to create a yearly presentation about their daily weather conditions and their effects on flight operations in 2023. The National Centers for Environmental Information: National Oceanic and Atmospheric Administration is their audience. Throughout 2023, there are 10,787 weather observations in total. These observations kept track of hourly weather conditions each month, such as humidity levels, lowest temperature, highest temperature, rain measurements, and snowfall measurements. Each day, about 15 airplanes depart from the Elko Regional Airport to nearby airports in Nevada and sometimes to out-of-state nearby destinations. Some of the flights were delayed while some were early.

I used a simplified version that I created of the Elko Regional Airport’s data from the more complex dataset provided on the National Centers for Environmental Information website. I generated a fictional dataset containing flight information and their destinations based on the table formatting of Hadley Wickham’s nycflights13 package and FlightAware’s live geospatial Flight Tracker. Since there are thousands of data rows throughout 2023, I only included 12 random flight observations to speed up the data insertion process.

The data included are weather conditions and flight information. The first part of the data includes information about 6 randomly chosen fictional flights based on information from Hadley Wickham’s nycflights13 package live data from FlightAware. From FlightAware, I only changed the airlines and tailnumbers. I only took the departure and arrival times for each destination to get a reasonable estimated time for a plane to fly from one destination to the next. To add realism to the small flight dataset, I included real destinations and the actual time it takes for planes to reach some of these destinations. Using the tail number and airline information provided on Airfleets.net, I based the formats of the tail numbers used in airlines in the United States.

Each date of flight departure has different weather conditions that may affect an airplane’s chance of having a flight delay. I added information about weather conditions for each flight data based on real climatological data from the National Centers for Environmental Information. Based on the information, there may be flight delays no matter the weather conditions.

# Table Columns
## Planes
-	`PlaneID`: The primary key that identifies each plane.
- `TailNumber`: A unique string, mixed with letters and numbers, on the tail of each plane used to identify the plane. This identifier is 6 characters long.
- `PlaneModel`: The aircraft model of the plane.

## Airports
-	`AirportID`: The primary key and 3 character FAA code of an airport.
- `AirportName`: The full name of an airport.
- `Location`: The city and state where the airport is located.

## Flights
-	`FlightID`: The primary key that identifies each flight.
-	`TailNumber`: A foreign key from the Planes table.
-	`FlightDate`: The date of the flight.
-	`ScheduledDeparture`: A plane's scheduled departure time from an airport in 24-hour format.
-	`Departure`: A plane's actual departure time from an airport in 24-hour format.
- `ScheduledArrival`: A plane's scheduled arrival time from an airport in 24-hour format.
-	`Arrival`: A plane's actual arrival time from an airport in 24-hour format.
-	`Origin`: The airport a plane is flying from in this flight.
-	`Destination`: The airport a plane is flying to in this flight.
-	`CarrierName`: The name of the airline involved in this flight.

## Airlines
-	`AirlineID`: The primary key that identifies each airline.
-	`CarrierName`: The full name of an airline company.

## Weather
-	`WeatherID`: The primary key that identifies each weather condition.
-	`TemperatureID`: The average dry bulb temperature of a given day.
-	`WindSpeed`: The average wind speed of a given day.
-	`DewPoint`: The average dew point level of a given day.
-	`Humidity`: The average humidity level of a given day.
-	`Rainfall`: Inches of rainfall.
-	`Snowfall`: Inches of Snowfall.

# Junction Table
## FlightsWeather
- `FlightID`: The primary key from the Flights table and the foreign key of this table.
- `WeatherID`: The primary key from the Weather table and the foreign key of this table.

# Retrieved data from
- Flight Tracker. FlightAware, 2024. https://www.flightaware.com/live/airport/KEKO
- Local Climatological Data (LCD). National Centers for Environmental Information: National Oceanic and Atmospheric Administration, 2023. https://www.ncei.noaa.gov/access/search/data-search/local-climatological-data?startDate=2023-01-03T00:00:00&endDate=2023-01-03T23:59:59&bbox=40.889,-115.821,40.783,-115.715&pageNum=1
- Plane Pictures. Airfleets.net, 2024. https://www.airfleets.net/photo/search.htm
- Wickham, Hadley. Flights that Departed NYC in 2013. Github, 2022. https://cran.r-project.org/web/packages/nycflights13/nycflights13.pdf

# Objectives
The Elko Regional Airport wants to automate its data management system and determine whether or not different weather conditions affect on-time flight performance. The goals of the analysis is to develop a relational database model, generate tables based on the data about the weather and flights, and use the SQL language to query the data to answer questions.

# Step-By-Step Procedure Description
After I developed my data model, I generated my tables using SQL in MySQL Workbench, exactly copying the visual structures in Lucidchart. Using the SQL programming langauge to fill my empty tables, I copied the information from the fictional flight and weather data from my Excel Spreadsheet to MySQL. In some tables, such as the airports table, I added extra airports to demonstrate how an OUTER LEFT JOIN is different from an INNER JOIN.

I used a single-row subquery to show all the flights that are traveling to Salt Lake City International Airport. I used a multi-row subquery to show all the flights traveling to either Reno/Tahoe International Airport or Battle Mountain Airport in my subquery. For my aggregate function to group rows together, I used the COUNT function to count the number of flights and separates them by groups. I grouped the aggregates by their carriers and destinations. I used the NOT IN operator to return a list of flights that did not fly to either Salt Lake City International Airport or Reno/Tahoe International Airport. For the on-time flight performance, I created a column using the CASE statement that calculates whether a plane arrives early or late. I used the NOT EXISTS operator to return a list of flights that are behind both their departure and arrival schedules. I used the NOT NULL operator in a subquery to filter out rows that are NULL in either the Snowfall or Rainfall columns in the weather table.

# Charts Generated For This Project
The real world implications of this project is to track and trend the flight performance indicator of airplanes. All example flights are those that are originating from the Elko Regional Airport.

There are five main entities needed to model the database: Planes, Flights, Airports, Weather, and Airlines. For each flight, there are details about each plane linked to a tailnumber and its make. The origins and destinations consist of airports where an airplane can travel. Each airport ID is based on the FAA code of the airport, its location, and the airport’s full name. All airplanes in the dataset belong to an airline carrier. The Airline entity could have more details about an airline.

The reason why there is a many-to-many relationship between flights and weather is that a region can experience multiple weather conditions. Also, the weather conditions will differ from one airport to another, so a flight would go through different regions that have their own weather conditions. For example, in the originating airport, it could be a rainy day by the time an airplane departs, but in the destination airport, it could be a sunny day by the time the airplane arrives.

## Conceptual Model
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Conceptual%20Model.png)

## Logical Model
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Logical%20Model.png)

## Physical Model
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Physical%20Model.png)

# Examining The Tables
## Airlines
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Column%20Data%20Types%20Airlines.png)
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Filled%20Data%20Airlines.png)

## Airports
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Column%20Data%20Types%20Airports.png)
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Filled%20Data%20Airports.png)

## Flights
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Column%20Data%20Types%20Flights.png)
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Filled%20Data%20Flights.png)

## FlightsWeather
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Column%20Data%20Types%20FlightsWeather.png)
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Filled%20Data%20FlightsWeather.png)

## Planes
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Column%20Data%20Types%20Planes.png)
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Filled%20Data%20Planes.png)

## Weather
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Column%20Data%20Types%20Weather.png)
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Filled%20Data%20Weather.png)

# Data Exploration
## Joining The Junction Table Between Two Other Related Tables
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Joining%20The%20Junction%20Table%20Between%20Two%20Other%20Related%20Tables.png)

## Left Outer Join VS Inner Join
My left table includes the list of airports. Not all of them have a single flight. My right table includes details about the planes that flew to other destinations. The difference is that null values are included because the result includes everything from the left table. The LEFT OUTER JOIN includes all the airports in the dataset, especially when there are no flights. The INNER JOIN includes all the rows and airports all my flights and airports share in common.

### Left Outer Join
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Left%20Outer%20Join.png)

### Inner Join
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Inner%20Join.png)

## SQL Results Using A Single-Row Subquery
My subquery filters one airport from the list of airports and returns one row. The row contains the Salt Lake City International Airport. The output shows all the flights that are traveling to Salt Lake City International Airport.
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Single-Row%20Subquery.png)

## SQL Results Using A Multiple-Row Subquery
My subquery selects more than one airport from the list of airports and returns multiple rows. The row contains the Reno/Tahoe International Airport and the Battle Mountain Airport. My output shows all the flights traveling to either Reno/Tahoe International Airport or Battle Mountain Airport in my subquery.
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/Multiple-Row%20Subquery.png)

## SQL Results Using Aggregation By Using Multiple Columns
My SQL query calculates the number of flights per airline to each destination. To aggregate or group the columns, it uses the COUNT function to count the number of flights and separates them by groups. I grouped the aggregates by their carriers and destinations.
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/SQL%20Results%20Using%20Aggregation%20By%20Using%20Multiple%20Columns.png)

## SQL Results Using The NOT IN Operator In The Subquery
My query calculates the departure delay minutes and arrival delay minutes by subtracting the time differences between the scheduled departures and the actual departures and between the scheduled arrival and actual arrival. It creates two new columns with the calculated minutes. All positive numbers indicate an early departure and early arrival. All negative numbers indicate a late departure and late arrival. These numbers affect the flight performance indicator of an airline. My query selects all rows that are not in my subquery’s list. My subquery’s list consists of both Salt Lake City International Airport and Reno/Tahoe International Airport. The NOT IN operator indicates that the query should exclude everything inside the subquery’s list. It returns every flight except for the ones flying to the two airports.
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/SQL%20Results%20Using%20The%20NOT%20IN%20Operator%20In%20The%20Subquery.png)

## SQL Results Using a CASE Statement
From the calculated time difference between the scheduled arrivals and departures and the actual arrivals and departures, my query calculates whether a plane arrives early or late. Each case statement makes a calculation depending on the time differences and whether or not a plane was able to meet its scheduled departure and arrival times. For those that departed early, the case statement indicates that it is early and vice versa. For those that arrived early, the case statement indicates that it is early and vice versa. One plane included in the recorded data departed early but arrived late. No matter the amount of rainfall and snowfall, planes can still either be ahead of their schedule or behind their schedule.
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/SQL%20Results%20Using%20a%20CASE%20Statement.png)

## SQL Results Using The NOT EXISTS Operator
My query returns the list of flights that are behind both their departure and arrival schedules. The subquery returns a list of flights that are at least early in their departure, arrival, or both. The NOT EXISTS operator indicates that the query should return records that are not in the subquery’s list because they did not meet the criteria.
![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/SQL%20Results%20Using%20The%20NOT%20EXISTS%20Operator.png)

## SQL Results Using The NOT NULL Operator And Filtering Out 0's In The Inner Query
The results show that there were some days that experienced both rain and snow. If there are null records, it does not return these rows. My query selects the recorded weather conditions that are both snowy and rainy in Elko, Nevada in 2023. The first inner query selects the weather conditions that are rainy. The second inner query selects the weather conditions that are snowy. Combining both inner queries’ criteria gives multiple days that have snow and rain in Elko, Nevada.

![Image](https://github.com/SMarbella/On-Time-Flight-Performance-Analysis-Elko-Regional-Airport/blob/main/Graphs/SQL%20Results%20Using%20The%20NOT%20NULL%20Operator%20And%20Filtering%20Out%200's%20In%20The%20Inner%20Query.png)

# Conclusion
As a result, flight delays still occur no matter how clear the weather is or how much rain or snow covered the airports. On January 16, 2023, the weather conditions in Elko, Nevada had 0.08 inches of rainfall and 1 inch of snow. There was a plane on that day that had a delayed flight. However, on April 14, 2023, there was a plane on that day that had a delayed flight despite having no rain or snow in the area. No matter the amount of rainfall and snowfall, planes can still either be ahead of their schedule or behind their schedule.
