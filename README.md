# 520or90Data
The 520 or 90 project was a mobile application that was concepted and built at Startup Weekend in Seattle.  The aim of the application was to quickly help a driver determine what bridge is faster or cheaper in less than 10 seconds.  As part of operating the service for over 3 years, we've collected a large amount of travel data that others can use to get interesting information about Seattle's traffic.  For more information, feel free to contact me on Twitter: @gabosgab

## Data Schema
Data provided for travel times was sampled from Jan 2nd, 2012 to August 20th, 2015.  Not all closures were captured correctly as it was a manual process for entry.  All data was collected from Washington State Department of Transportation public route travel data service. http://wsdot.com/traffic/api/?_ga=1.96098261.877723817.1445755577

### bridge_closures schema
Column    | Description
--------- | -----------
id        | The row id.
start     | The time the bridge closure begins. (Pacific Time)
end       | The time the bridge closure ends. (Pacific time)
bridge    | What bridge would be closed.

### bridge_histories schema
Column    | Description
--------- | -----------
id        | The row id.
timestamp | the timestamp of the sample. (Pacific time)
source    | Location where the vehicle would be originating from on the route estimate.
dest      | Location where the vehicle would be arriving to on the route estimate.
toll520   | The charge of the 520 toll at the timestamp given to travel from source to dest using SR-520.
fuel520   | The cost of fuel the average 4 door vehicle will consume traveling from source to dest taking SR-520.  This is calculated using market rates for fuel provided by Federal reports released weekly.
time520   | The time to travel from source to dest in minutes via SR-520.
fuel90    | The cost of fuel the average 4 door vehicle will burn traveling from source to dest taking I-90.  This is calculated using market rates for fuel provided by Federal reports released weekly.
time90    | The time to travel from source to dest in minutes via I-90.

### vAverageTravelTimesByDOW schema
This table is a summarization of the bridge_histories table by day of week, by 5 minute increments, by route.

Column     | Description
---------- | -----------
source     | Location where the vehicle would be originating from on the route estimate.
dest       | Location where the vehicle would be arriving to on the route estimate.
dow        | The day of the week starting from Sunday = 1, Saturday = 7
time       | The time of day on the day of the week
avgTime520 | The average time it takes in minutes to travel from source to dest via SR-520.
stdDev520  | The standard deviation on the time it takes to travel from source to dest via SR-520.
sampleSize | The number of samples observed for the day of week and time.
min520     | The minimum time observed to travel from source to dest via SR-520 at this day of week and time.
max520     | The maximum time observed to travel from source to dest via SR-520 at this day of week and time.
avgTime90  | Theaverage time it takes in minutes to travel from source to dest via I-90.
stdDev90   | The standard deviation on the time it takes to travel from source to dest via I-90.
min90      | The minimum time observed to travel from source to dest via I-90 at this day of week and time.
max90      | The maximum time observed to travel from source to dest via I-90 at this day of week and time.

## Data Formats Available

### 520or90-HistoricalData.sql.zip
This file contains two SQL tables dumped from MySQL with two tables: bridge_histories and bridge_closures.

### 520or90-HistoricalData.csv.zip
This file contains two CSV files, bridge_closures.csv and bridge_histories.csv

### 520or90-TravelTimesByDOW.csv.zip
This file contains a single CSV table, vAverageTravelTimesByDOW.csv

