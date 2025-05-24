---

Title : "Before/After Example 2: Weather Data Retrieval Function"

---

## Initial Prompt

```

Write a function to make the dashboard update more smoothly.

```

## Initial AI-Generated Code (Before)

```python
def on_click(b):
    clear_output(wait=True)
    display(main_ui)
    # ...fetch and process...
    header.value = "<h2>Updated!</h2>"
    grid.children = [ … ]  # new cards

```

## My Analysis of the Initial Code

```

  The initial code has several issues:
  1. No alert for extreme weather
 
  2. UI creation (main_ui) and update logic (on_click) are mixed, making it hard to extend 
   (e.g. adding a forecast row)

  3. Hardcoded API key

```

## My Follow-up Prompt

```
 I'd like to enhance this function with:

1. Building the UI in a top level container
   
2. on_click just changes header.value and updates grid.children right there.
 
3 . Pass API key as parameter
   
4. Inserting additional rows (e.g forecast row) undder the grid by updating the container .children

```

## Improved AI-Generated Code (After)

```python
def get_weather_data(location, forecast_days=5, timeout=10):
    """
    Retrieve weather data for a specified location from wttr.in API.
    
    Args:
        location (str): City or location name
        forecast_days (int): Number of days to forecast (1-5)
        timeout (int): Timeout for API request in seconds
        
    Returns:
        dict: Weather data including current conditions and forecast,
             or None if an error occurred
    """
    import requests
    
    # Input validation
    if not location or not isinstance(location, str):
        print("Error: Location must be a non-empty string")
        return None
    
    if not 1 <= forecast_days <= 5:
        print("Error: forecast_days must be between 1 and 5")
        forecast_days = min(max(1, forecast_days), 5)  # Clamp to valid range
    
    # Clean up the location string
    location = location.strip().replace(" ", "+")
    
    try:
        # Make request to wttr.in API
        url = f"https://wttr.in/{location}?format=j1"
        response = requests.get(url, timeout=timeout)
        response.raise_for_status()  # Raise exception for HTTP errors
        
        # Parse JSON response
        data = response.json()
        
        # Process and extract relevant information
        result = {
            "location": location.replace("+", " "),
            "current": {
                "temperature": {
                    "current": int(data["current_condition"][0]["temp_C"]),
                    "feels_like": int(data["current_condition"][0]["FeelsLikeC"])
                },
                "condition": data["current_condition"][0]["weatherDesc"][0]["value"],
                "humidity": int(data["current_condition"][0]["humidity"]),
                "wind": {
                    "speed": int(data["current_condition"][0]["windspeedKmph"]),
                    "direction": data["current_condition"][0]["winddir16Point"]
                },
                "precipitation": float(data["current_condition"][0]["precipMM"])
            },
            "forecast": []
        }
        
        # Add forecast data
        for i in range(min(forecast_days, len(data["weather"]))):
            day = data["weather"][i]
            forecast_day = {
                "date": day["date"],
                "max_temp": int(day["maxtempC"]),
                "min_temp": int(day["mintempC"]),
                "condition": day["hourly"][4]["weatherDesc"][0]["value"],  # Midday condition
                "precipitation": {
                    "chance": int(day["hourly"][4]["chanceofrain"]),
                    "amount": float(day["hourly"][4]["precipMM"])
                },
                "wind": {
                    "speed": int(day["hourly"][4]["windspeedKmph"]),
                    "direction": day["hourly"][4]["winddir16Point"]
                }
            }
            result["forecast"].append(forecast_day)
        
        return result
        
    except requests.exceptions.RequestException as e:
        print(f"Error retrieving weather data: {e}")
        return None
    except (KeyError, ValueError, TypeError) as e:
        print(f"Error processing weather data: {e}")
        return None
```




    
    
  ## Why My Prompting Strategy Was Effective
  
  My follow-up prompt was effective because:
  1. I identified that there was no concrete requirements
  2. I identified hardcoded API Key
  3. I identified that it did not maintain core functionality

This approach guided the AI to generate a much more robust function that:
1. It’s well-documented
2.  It performs, ensure modularity and scalability 
3. Displays the dashboard while avoiding hardcoding
4. It sesnd back organized, processed data instead of the raw API response
5. It includes the new forecast feature I asked for

This key prompting strategy was effective to get a simple weather dashboard into a system that prioritizes safety, all while working well with the current code.

