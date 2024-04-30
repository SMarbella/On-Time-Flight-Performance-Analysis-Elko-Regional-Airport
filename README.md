# On-Time Flight Performance Analysis: Elko Regional Airport
For this project, I used MySQL Workbench, Lucidchart, and Microsoft Excel to create a database and analyze data that I created based on datasets from the National Centers for Environmental Information, Hadley Wickham’s nycflights13 package, and FlightAware’s live geospatial Flight Tracker. The Elko Regional Airport, a small airport in Elko, Nevada, wants to automate its data management system. The problem is that they want to track how weather conditions affect flight delays and present their findings to the National Centers for Environmental Information: National Oceanic and Atmospheric Administration. They have over 10,787 weather observations in total with approximately 15 airplanes departing from the Elko Regional Airport each day. Due to the large number of flights and weather conditions at the Elko Regional Airport, I had to create 12 records. Using Microsoft Excel, I created a shorter version where I come up with 12 fictional flights based on the actual times it takes for planes to reach any destination from Elko.

# Synopsis
The Elko Regional Airport, a small airport in Elko, Nevada, wants to automate its data management system. They want to organize their local climatological data to create a yearly presentation about their daily weather conditions and their effects on flight operations in 2023. The National Centers for Environmental Information: National Oceanic and Atmospheric Administration is their audience. Throughout 2023, there are 10,787 weather observations in total. These observations kept track of hourly weather conditions each month, such as humidity levels, lowest temperature, highest temperature, rain measurements, and snowfall measurements. Each day, about 15 airplanes depart from the Elko Regional Airport to nearby airports in Nevada and sometimes to out-of-state nearby destinations. Some of the flights were delayed while some were early.

I used a simplified version that I created of the Elko Regional Airport’s data from the more complex dataset provided on the National Centers for Environmental Information website. I generated a fictional dataset containing flight information and their destinations based on the table formatting of Hadley Wickham’s nycflights13 package and FlightAware’s live geospatial Flight Tracker. Since there are thousands of data rows throughout 2023, I only included 12 random flight observations to speed up the data insertion process.

The data included are weather conditions and flight information. The first part of the data includes information about 6 randomly chosen fictional flights based on information from Hadley Wickham’s nycflights13 package live data from FlightAware. From FlightAware, I only changed the airlines and tailnumbers. I only took the departure and arrival times for each destination to get a reasonable estimated time for a plane to fly from one destination to the next. To add realism to the small flight dataset, I included real destinations and the actual time it takes for planes to reach some of these destinations. Using the tail number and airline information provided on Airfleets.net, I based the formats of the tail numbers used in airlines in the United States.

Each date of flight departure has different weather conditions that may affect an airplane’s chance of having a flight delay. I added information about weather conditions for each flight data based on real climatological data from the National Centers for Environmental Information. Based on the information, there may be flight delays no matter the weather conditions.

# Table Columns
## Planes
-	`PlaneID`: The primary Key field that identifies each plane.
- `TailNumber`: A unique string, mixed with letters and numbers, on the tail of each plane used to identify the plane. This identifier is 6 characters long.
- `PlaneModel`: The aircraft model of the plane.

## Airports
-	`AirportID`: The primary key and 3 character FAA code of an airport.
- `AirportName`: The full name of an airport.
- `Location`: The city and state where the airport is located.

# Retrieved data from
- Flight Tracker. FlightAware, 2024. https://www.flightaware.com/live/airport/KEKO
- Local Climatological Data (LCD). National Centers for Environmental Information: National Oceanic and Atmospheric Administration, 2023. https://www.ncei.noaa.gov/access/search/data-search/local-climatological-data?startDate=2023-01-03T00:00:00&endDate=2023-01-03T23:59:59&bbox=40.889,-115.821,40.783,-115.715&pageNum=1
- Plane Pictures. Airfleets.net, 2024. https://www.airfleets.net/photo/search.htm
- Wickham, Hadley. Flights that Departed NYC in 2013. Github, 2022. https://cran.r-project.org/web/packages/nycflights13/nycflights13.pdf

# Objectives
The Elko Regional Airport wants to automate its data management system and determine whether or not different weather conditions affect on-time flight performance. The goals of the analysis is to develop a relational database model, generate tables based on the data about the weather and flights, and use the SQL language to query the data to answer questions.
