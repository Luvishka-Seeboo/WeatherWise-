---

Title: "Before/After Example 1 : Weather Data Retrieval Function"

---
## Initial Prompt 
```

Write a function to retrieve weather data from OpenWeatherMap for Mauritius.

```
## Initial AI-Generated Code (Before)

```python
def get_weather(city, api_key):
    url = "https://api.openweathermap.org/data/2.5/weather"
    params = {"q": f"{city},MU", "appid": api_key, "units": "metric"}
    response = requests.get(url, params=params)
    return response.json()
```



## My Analysis of the Initial Code
The initial code has several issues:
1. No error handling for API failures
2. No validation for invalid API keys
3. Crashes if city doesn't exist.

 ## My Follow-up Prompt
 Thanks for the starting point. I'd like to improve this function with:
 1. Handle API errors(invalid invalid keys) gracefully.
 2. Validate the city in Mauritius
 3. Return None on failure with a descriptive error message.
    
## Improved AI-Generated Code (After)

```python
def get_weather_safe(city, api_key, timeout=5):
    """
    Safely fetch Mauritius weather data with error handling.
    
    Args:
        city (str): Mauritian city name
        api_key (str): OpenWeatherMap API key
        timeout (int): Request timeout in seconds
        
    Returns:
        dict: Weather data or None if error occurs
    """
    if not isinstance(city, str) or not city.strip():
        print("Error: City must be a non-empty string")
        return None
        
    try:
        url = "https://api.openweathermap.org/data/2.5/weather"
        params = {
            "q": f"{city.strip()},MU",
            "appid": api_key,
            "units": "metric"
        }
        response = requests.get(url, params=params, timeout=timeout)
        response.raise_for_status()
        data = response.json()
        
        # Validate response is from Mauritius
        if data.get("sys", {}).get("country") != "MU":
            print(f"Error: {city} is not in Mauritius")
            return None
            
        return {
            "city": data["name"],
            "temp": data["main"]["temp"],
            "condition": data["weather"][0]["description"]
        }
        
    except requests.exceptions.RequestException as e:
        print(f"API Error: {str(e)}")
        return None

```

## Why My Prompting Strategy Was Effective

My follow-up prompt was effective because:
1. Initially identified specific weaknesses (no error handling, no validation)
2. Made clear what was unacceptable about the original code
3.Example: Highlighted that it "crashes if city doesn't exist

This approach guided the AI to generate a much more robust function that:

1. Acknowledge real-world usage scenarios (network issues, bad inputs)
2. Implement Python best practices (type checking, request timeouts)
3. Maintain the original function's purpose while making it robust
4. Provide clear failure modes that would work well in the larger application

This method turned a weak function into a fully working one, all while ensuring it stuck to its main job.
