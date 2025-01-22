# Weather-Forecast-Using-API
The weather app fetches real-time weather for a user-provided city using Python. The user enters a city name, and the geopy library converts it into geographic coordinates (latitude and longitude).
These coordinates are sent to the OpenWeatherMap API via a GET request using the requests library.
 The API responds with weather data in JSON format, which the app processes to extract temperature, weather condition, humidity, and wind speed. These details are displayed to the user in a readable format.
Errors like invalid city names or API issues are handled with clear messages to ensure smooth interaction.
Step 1: Importing Libraries
import requests
from geopy.geocoders import Nominatim
•	requests: Handles HTTP requests to fetch data from the OpenWeatherMap API.
•	geopy.geocoders.Nominatim: Converts the user's city name into geographical coordinates (latitude and longitude).
Step 2: Function Definition
def get_weather():
  # OpenWeatherMap API Key
api_key = "your_api_key"  # Replace with your actual API key
•	get_weather(): The main function to fetch and display weather data.
•	api_key: Your personal OpenWeatherMap API key. This authenticates your requests.

Step 3: Getting User Input and Location
à	geolocator = Nominatim(user_agent="weather_app")
à	city = input("Enter your city name: ")
à	location = geolocator.geocode(city)
•	Nominatim: Initializes the geolocator to convert city names into latitude and longitude.
•	input(): Prompts the user to enter a city name.
•	geolocator.geocode(city): Converts the city name into a location object containing latitude and longitude.

Step 4: Location Validation
à	if location:
à	lat, lon = location.latitude, location.longitude
à	print(f"City: {city} (Lat: {lat}, Lon: {lon})")
•	Checks if the location object exists (i.e., if the city name was valid).
•	Extracts the latitude and longitude (lat, lon) and displays them.

Step 5: Making an API Request
 url = f"http://api.openweathermap.org/data/2.5/weather?lat={lat}&lon={lon}&appid={api_key}&units=metric"
à	response = requests.get(url)
•	url: Constructs the API request URL with latitude, longitude, api_key, and metric units (for Celsius temperatures).
•	requests.get(url): Sends an HTTP GET request to OpenWeatherMap to fetch the weather data.

Step 6: Checking API Response
à	if response.status_code == 200:
à	data = response.json()
•	response.status_code: Checks if the request was successful (200 status code means OK).
•	response.json(): Parses the JSON response into a Python dictionary called data.

Step 7: Parsing Weather Data
à	city_name = data['name']
à	country = data['sys']['country']
à	temp = data['main']['temp']
à	weather = data['weather'][0]['description']
à	humidity = data['main']['humidity']
à	wind_speed = data['wind']['speed']
•	Extracts the following:
o	city_name: Name of the city.
o	country: Country code.
o	temp: Current temperature in Celsius.
o	weather: Weather description (e.g., clear, cloudy).
o	humidity: Humidity percentage.
o	wind_speed: Wind speed in meters per second.

Step 8: Displaying Weather Data
            print(f"\nWeather in {city_name}, {country}:")
            print(f"Temperature: {temp}°C")
            print(f"Condition: {weather.capitalize()}")
            print(f"Humidity: {humidity}%")
            print(f"Wind Speed: {wind_speed} m/s")
•	Displays the extracted weather data in a user-friendly format.

Step 9: Handling Errors
-->	else:
-->	print(f"Error {response.status_code}: Unable to fetch weather data.")
-->	else:
-->	print("City not found! Please try again.")
•	If API fails: Displays the HTTP error code (e.g., 404 for not found, 401 for invalid API key).
•	If location is invalid: Informs the user that the city name is incorrect or not found.

10. Running the App
-->	if __name__ == "__main__":
-->get_weather()
•	Ensures the get_weather() function is executed only when the script is run directly (not when imported as a module).

How It Works:
1.	Prompts the user for a city name.
2.	Converts the city into geographic coordinates using Geopy.
3.	Sends the coordinates to the OpenWeatherMap API to fetch weather data.
4.	Parses and displays the weather details, or shows errors if the city or API key is invalid.

