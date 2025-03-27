# Weather Data Retrieval and Storage

## Overview
This script fetches weather data from the Meteomatics API for multiple cities, processes it, and stores it in a PostgreSQL database. The weather parameters include temperature, humidity, and wind speed for a period of 7 days. The API provides various endpoints for retrieving forecast data, listing locations, and analyzing weather metrics.

## Features
- Converts city names to geographic coordinates.
- Fetches weather data for predefined locations.
- Processes and organizes API response data.
- Stores location and weather data in a PostgreSQL database.
- List all locations stored in the database.
- Retrieve the latest forecast for each location per day.
- Calculate the average temperature of the last three forecasts per location per day.
- Get the top N locations based on available weather metrics (temperature, humidity, wind speed)

## Technologies Used
- **Python**
- **APIs:** Meteomatics API
- **Database:** PostgreSQL
- **Libraries:**
  - `geopy` for geolocation
  - `pandas` for data processing
  - `sqlalchemy` and  for database connection
  - `psycopg2` for PostgreSQL connectivity
  - `requests` for API calls

## Installation & Setup
### Prerequisites
Ensure you have the following installed:
- Python 3.9+
- PostgreSQL


### Install Dependencies
```sh
pip install -r requirements.txt
```

### Configure API and Database Credentials
1. Create a `credentials.json` file in the project directory with the following structure:
```json
{
    "USERNAME_API": "your_api_username",
    "PASSWORD_API": "your_api_password",
    "DB_NAME": "your_db_name",
    "DB_USER": "your_db_user",
    "DB_PASSWORD": "your_db_password",
    "LOCAL_HOST_DB": "your_db_host",
    "DB_PORT": "your_db_port"
}
```

2. Ensure the PostgreSQL database is running and has the required tables (`location_info` and `weather_info`).

### Run the two Scripts separately

### For API data retrieval and DB store run
```sh
python Meteomatics_DB.py
```
### For DB data retrival and API Server
```sh
uvicorn DB_to_API:app --reload
```



## How It Works
1. **Converts city names to coordinates** using the `geopy` library.
2. **Retrieves weather data** from the Meteomatics API.
3. **Processes the data** to extract relevant parameters.
4. **Stores location details** in the `location_info` table.
5. **Stores weather forecast data** in the `weather_info` table.
6. **Retrieve data and run API** .

## API Endpoints

1. **List All Locations**

Endpoint: GET /list_locations
Description: Returns a list of all locations stored in the database.

2. **Latest Forecast per Location and Day**

Endpoint: GET /last_forecast_per_loc_and_day
Description: Fetches the most recent forecast for each location per day.

3. **Average Temperature of Last 3 Forecasts per Location per Day**

Endpoint: GET /last_three_forecast_temp_avg_per_loc_and_day
Description: Calculates the average temperature from the last three forecasts for each location per day.

4. **Top N Locations Based on Weather Metrics**

Endpoint: GET /top_metrics_per_location?n=<value>
Description: Retrieves the top N locations based on wind speed, temperature, and humidity.

## Known Limitations
- Geolocation retrieval might fail if city names are not properly recognized.
- Limited API calls for Geolocation and you might get an error.
- METEOmatic grant a free trial only for 14 days.
- Hardcoded city coordinates are used as a fallback in case geolocation fails.
- The API fetches data from the PostgreSQL database and does not directly call the Meteomatics API.
- Forecast updates depend on how frequently data is ingested into the database.

## Author
- **Nikolas Mpouzianas**

