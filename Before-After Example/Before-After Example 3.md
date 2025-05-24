---

title: "Before/After Example 3: Weather Data Retrieval Function"

---

## Initial Prompt
```
Write a function to get current weather for Mauritius.
```
## Initial AI-Generated Code (Before)

```python
def get_current_weather(city):
    # Only returns current snapshot
    return requests.get(f"https://api.openweathermap.org/...").json()
```
## My Analysis of the Initial Code
The initial code has several issues:

1.No ability to forecast

2.No option to choose time periods

3.Responses are not flexible

## My Follow-up Prompt
I'd like to modify this function with:

1. Allowing drop down to select any location. For example Port-Louis

2. Displaying himidity, temperature.wind

3. Return consistent formatted periods

## Improved AI-Generated Code (After)

```python
def get_weather(city, api_key):
    url = "https://api.openweathermap.org/data/2.5/weather"
    params = {"q": f"{city},MU", "appid": api_key, "units": "metric"}
    response = requests.get(url, params=params)
    return response.json()
```
## Why My Prompting Strategy Was Effective
My follow-up prompt was effective because:

1. **I identified specific problems** in the original code, it would crash if the API request failed(e.g due to invalid city)
2. **I requested specific improvements** with clear objectives (error handling, validation, etc.)
3. **I suggested a new feature** (forecast_days parameter) that would make the function more useful.
4. **I asked for proper documentation** which resulted in comprehensive docstrings
5. 
This approach guided the AI to generate a much more robust function that:
1. Handles errors gracefully
2. includes input validation
3. returns clean, structured data
4. Enhances maintainability

 The key to effective prompting was being specific about turning a basic function intto a user-friendly, production ready utility by guiding AI with precise, target improvements.  







