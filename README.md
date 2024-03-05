import urllib.parse
import urllib.request
import json
import time

class WeatherChecker:
    def __init__(self, api_key):
        self.api_key = api_key
        self.base_url = 'http://api.weatherapi.com/v1/'

    def get_weather_by_city(self, city_name):
        url = f'{self.base_url}current.json?key={self.api_key}&q={city_name}'
        req = urllib.request.Request(url)
        try:
            with urllib.request.urlopen(req) as response:
                data = response.read()
                return json.loads(data)
        except urllib.error.URLError as e:
            print(f"Error fetching weather data: {e}")
            return None

def main():
    api_key = 'your_api_key_here'
    weather_checker = WeatherChecker(api_key)
    
    while True:
        city_name = input("Enter city name: ")
        weather_data = weather_checker.get_weather_by_city(city_name)
        if weather_data:
            print(weather_data)
        time.sleep(15)  # Auto-refresh every 15 seconds

if __name__ == "__main__":
    main()
