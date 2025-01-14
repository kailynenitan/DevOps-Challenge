# Weather Dashboard
Building a weather data collection system using AWS S3 and OpenWeather API

This project was built using the weather dashboard code from Day 1 of the DevOpsAllStarsChallenge https://youtu.be/A95XBJFOqjw?si=h0Q0_22oy2ROqT3u

## Features of Dashboard
- Fetches real-time weather data for multiple cities
- Displays temperature (°F), humidity, and weather conditions
- Automatically stores weather data in AWS S3
- Supports multiple cities tracking
- Timestamps all data for historical tracking

## Technical Architecture
- **Language:** Python 3.x
- **Cloud Provider:** AWS (S3)
- **External API:** OpenWeather API
- **Dependencies:** 
  - boto3 (AWS SDK)
  - python-dotenv
  - requests

```
## Project Structure
weather-dashboard/
  src/
      __init__.py
      weather_dashboard.py
  .env
  .gitignore
  requirements.txt
  README.md
  ```

## Setup Instructions
1. Clone the repository:
```
git clone https://github.com/ShaeInTheCloud/30days-weather-dashboard.git
```

2. Install dependencies:
 ```
pip install -r requirements.txt
```

3. Configure environment variables in .env:
In the 30days-weather-dashboard directory:
```
touch .env
```
In the .env file:
```
OPENWEATHER_API_KEY=your_api_key
AWS_BUCKET_NAME=your_bucket_name
```

4. Configure AWS credentials:
```
aws configure
```

5. Run the application:
 ```
python src/weather_dashboard.py
```

