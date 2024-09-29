# Power BI - Flights Dashboard

This repository contains screenshots of a Power BI dashboard analyzing flight data. The dashboard provides insights on flight delays, airline performance, and other key metrics for airports and airlines.


## Screenshots

![FlightsDash1](https://github.com/user-attachments/assets/60985f6d-df4d-4d35-952d-87967bdd0491)

![FlightsDash2](https://github.com/user-attachments/assets/4a55c1a1-4c7b-4b3d-a168-af1bb226c310)

![FlightsDash3](https://github.com/user-attachments/assets/076ec618-b132-4233-b8b1-0ded6bc673f2)

## About the Project

The goal of the project was to create data visualizations in Power BI. The data source used in the project is the "2015 Flight Delays and Cancellations" dataset from the website www.kaggle.com, available at the following link:  
[https://www.kaggle.com/datasets/usdot/flight-delays?ref=hackernoon.com&select=flights.csv](https://www.kaggle.com/datasets/usdot/flight-delays?ref=hackernoon.com&select=flights.csv).  
The dataset consists of three files:  
● airlines.csv  
● airports.csv  
● flights.csv  
These files contain information about flights from various airlines in 2015.

The first step in preparing the data model was setting the column headers, defining data types, and removing unnecessary columns for the visualization. Below is a description of the input data used in the model.

## Table: airports
- **IATA_CODE** – Airport ID
- **AIRPORT** – Name of the airport
- **CITY** – City
- **STATE** – State
- **COUNTRY** – Country
- **LATITUDE** – Latitude
- **LONGITUDE** – Longitude

## Table: airlines
- **IATA_CODE** – Airline ID
- **AIRLINE** – Airline name

## Table: flights
- **MONTH** – Month
- **DAY** – Day
- **DAY_OF_WEEK** – Day of the week
- **AIRLINE** – Airline
- **FLIGHT_NUMBER** – Flight identifier
- **TAIL_NUMBER** – Aircraft identifier
- **ORIGIN_AIRPORT** – Origin airport
- **DESTINATION_AIRPORT** – Destination airport
- **SCHEDULED_DEPARTURE** – Scheduled departure time
- **DEPARTURE_TIME** – Actual departure time (WHEEL_OFF – TAXI_OUT)
- **DEPARTURE_DELAY** – Departure delay
- **TAXI_OUT** – Time between leaving the gate and takeoff
- **WHEELS_OFF** – Time when the aircraft leaves the ground
- **SCHEDULED_TIME** – Scheduled flight time
- **ELAPSED_TIME** – Total time of the flight including airport time (AIR_TIME + TAXI_IN + TAXI_OUT)
- **AIR_TIME** – Time in the air
- **DISTANCE** – Distance between two airports
- **WHEELS_ON** – Time of landing
- **TAXI_IN** – Time between landing and reaching the gate at the destination airport
- **SCHEDULED_ARRIVAL** – Scheduled arrival time
- **ARRIVAL_TIME** – Actual arrival time
- **ARRIVAL_DELAY** – Arrival delay (ARRIVAL_TIME – SCHEDULED_ARRIVAL)
- **DIVERTED** – Flight landed at a non-scheduled airport
- **CANCELLED** – Flight canceled
- **CANCELLATION_REASON** – Reason for flight cancellation
- **AIR_SYSTEM_DELAY** – Delay caused by air system
- **LATE_AIRCRAFT_DELAY** – Delay caused by the aircraft
- **SECURITY_DELAY** – Delay caused by security
- **WEATHER_DELAY** – Delay caused by weather conditions

An additional column, `Month_name`, was added to the `flights` table based on the `MONTH` column. Additionally, a `Date` table was created based on the `flights` table. The `COUNTRY_CITY_AIRPORT` hierarchy used in the model comes from the `airports` table.

## DAX rules used in the report:
- **NUMBER_OF_AIRLINES** = `COUNT(airlines[AIRLINE])` – Number of airlines
- **ARRIVAL_DELAY_AVG** = `AVERAGEX(flights, flights[ARRIVAL_DELAY])` – Average arrival delay
- **NUMBER_OF_AIRPORTS** = `COUNT(airports[AIRPORT])` – Number of airports
- **FLIGHT_COUNT_WITH_DELAY** = `CALCULATE(COUNT(flights[FLIGHT_NUMBER]),flights[ARRIVAL_DELAY] > 15)` – Number of flights with a delay greater than 15 minutes
- **FLIGHTS_WITH_DELAY_RATIO** = `flights[FLIGHT_COUNT_WITH_DELAY]/flights[NUMBER_OF_FLIGHTS]` – Ratio of delayed flights
- **NUMBER_OF_AIRCRAFTS** = `DISTINCTCOUNT(flights[TAIL_NUMBER])` – Number of unique aircraft
- **NUMBER_OF_FLIGHTS** = `COUNT(flights[FLIGHT_NUMBER])` – Total number of flights
- **TOTAL_DISTANCE** = `SUM(flights[DISTANCE])` – Total distance flown
- **TOTAL_DISTANCE_BY_AIRLINE** = `CALCULATE(SUM(flights[DISTANCE]),ALLEXCEPT(flights, flights[AIRLINE]))` – Total distance flown by each airline


Stay tuned for more projects and updates!

