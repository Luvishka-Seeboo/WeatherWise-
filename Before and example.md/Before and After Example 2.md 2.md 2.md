---


Title : "Before/After Example 2: Weather Data Retrieval Function"

---

## Initial Prompt

```

Write a function to show current weather conditions for Mauritius.

```

## Initial AI-Generated Code (Before)

---


---
    def show_weather(city):

    data = get_weather(city, API_KEY)
    
    print(f"Temperature: {data['main']['temp']}°C")
```

  ## My Analysis of the Initial Code
  
  The initial code has several issues:
  1.No alert for extreme weather
  2.No unit consistency check
  3. Hardcoded API key

## My Follow-up Prompt
```
 I'd like to enhance this function with:

1. Add alerts for high temps (>35°C) and cyclones
2. Ensure all units are metric
3. Pass API key as parameter

```
## Improved AI-Generated Code (After)

```
def get_weather_with_alerts(city, api_key):
    """
    Fetch weather with safety alerts for Mauritius.
    
    Args:
        city (str): Mauritian city name
        api_key (str): Valid API key
        
    Returns:
        dict: Weather data with optional alerts field
    """
    data = get_weather_safe(city, api_key)
    if not data:
        return None
        
    alerts = []
    if data["temp"] > 35:
        alerts.append("🔥 Heat Warning: Temperatures above 35°C")
    if "cyclone" in data["condition"].lower():
        alerts.append("🌀 Cyclone Alert!")
        
        return {
        
        **data,
        "alerts": alerts if alerts else ["No severe weather"] }
```
    
    
  ## Why My Prompting Strategy Was Effective
  
  My follow-up prompt was effective because:
  1. I identified specific weaknesses like not extreme weather
  2. I identified hardcoded API Key
  3. I identified that it did not maintain core functionality

This approach guided the AI to generate a much more robust function that:
1. It’s well-documented
2.  It checks the inputs
3. It has solid error handling
4. It sends back organized, processed data instead of the raw API response
5. It includes the new forecast feature I asked for

This key prompting strategy was effective to get a simple weather printer into a system that prioritizes safety, all while working well with the current code.



    
