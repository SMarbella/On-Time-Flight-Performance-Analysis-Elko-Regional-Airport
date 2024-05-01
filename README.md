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



