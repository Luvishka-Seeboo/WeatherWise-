---

Title: Prompting Journey for Weather Data Retrieval Function

---

---
## Initial Prompt 1 
---
----------------------------------
Tool: ChatGPT
Date: 2025-05-22
----------------------------------


Me: Can you help me build a weather dashboard using Python and OpenWeatherMap API to show the weather in cities in Mauritius?
AI: Definitely! Let's break it into steps. The dashboard will include:

-A list of Mauritian cities (dropdown)

-Input for API key

-A button to fetch weather

-A visual layout with cards showing temperature, humidity, etc.

We’ll use:

-requests to get weather data

-ipywidgets for interactivity in a Jupyter Notebook

-Some HTML/CSS in widgets for styling

Let’s start with the data-fetching function.

```python
def get_weather(city, api_key):
    url = "https://api.openweathermap.org/data/2.5/weather"
    params = {"q": f"{city},MU", "appid": api_key, "units": "metric"}
    response = requests.get(url, params=params)
    return response.json()
```

---
## Initial Prompt 2
---
----------------------------------
Tool: ChatGPT
Date: 2025-05-22
----------------------------------
Me: I want to make a Colab weather dashboard—what libraries do I need, and how do I set up the initial display area?
AI: Use requests for API calls, ipywidgets for interactive controls, and IPython.display to manage output. First, import these and call display(...) at the end to render your main container.

import requests
import ipywidgets as widgets
from IPython.display import display, clear_output


Me: How do I pull current weather for a Mauritius city and parse it into clear labels?
Ai: Write a get_weather() that calls OpenWeatherMap, handles errors via raise_for_status(), and returns a dict mapping friendly keys to formatted values.

```python
url = "https://api.openweathermap.org/data/2.5/weather"
params = {"q": f"{city},MU", "appid": api_key, "units": "metric"}
```

---
## Initial Prompt 3
---
----------------------------------
Tool: ChatGPT
Date: 2025-05-22
----------------------------------
Me: I'm getting an error when calling the OpenWeatherMap API.

AI: Can you share the exact error message?

Me: Sure, it says: "requests.exceptions.HTTPError: 401 Client Error: Unauthorized".

```python
def get_weather_forecast(location, api_key):
    try:
        # Geocoding to get lat/lon
        geo_url = f"http://api.openweathermap.org/geo/1.0/direct?q={location}&limit=1&appid={api_key}"
        geo_response = requests.get(geo_url)
        geo_data = geo_response.json()

        if not geo_data:
            return None, f"❌ Location '{location}' not found. Please check spelling."

        lat = geo_data[0]['lat']
        lon = geo_data[0]['lon']
        city = geo_data[0]['name']
        country = geo_data[0]['country']

        # Get 5-day forecast
        forecast_url = f"https://api.openweathermap.org/data/2.5/forecast?lat={lat}&lon={lon}&units=metric&appid={api_key}"
         forecast_data = requests.get(forecast_url).json()
```

AI: That usually means the API key is missing or invalid. Are you passing your API key correctly in the request?

Me: I'm using this line: params = {"q": f"{city},MU", "appid": api_key, "units": "metric"}

AI: That looks correct syntactically. Can you double-check if your `api_key` variable actually contains your API key?

Me: Hmm, I might have left it blank during testing.

AI: That would explain it. Try printing `api_key` before the request to verify. Also, make sure you’re not using expired or incorrect credentials.

Me: Okay, I’ll check.

AI: If you're using a widget, make sure to click the “Show Weather” button after entering the API key. The value must be captured before the request executes.

Me: Got it. It’s working now. Thanks!

---
## Initial Prompt 4
---

----------------------------------
Tool: ChatGPT
Date: 2025-05-22
----------------------------------
Me: Now that you have fix the API error, can you buld the dashboard and make it more UI ?

Ai: We'll use ipywidgets for input controls and HTML-styled weather cards.

```python
import ipywidgets as widgets
from IPython.display import display, clear_output

# Style hover effect for cards
style = widgets.HTML("""
<style>
.card:hover {
  transform: translateY(-6px) scale(1.02);
  box-shadow: 0 12px 24px rgba(0,0,0,0.2);
}
</style>
""")
display(style)

def make_card(title, value, bg_gradient):
    return widgets.HTML(
        f"""
        <div class="card" style="background:{bg_gradient};border-radius:15px;
            padding:12px;text-align:center;color:white;
            box-shadow: 0 8px 16px rgba(0,0,0,0.2);">
            <div style="font-size:14px;">{title}</div>
            <div style="font-size:26px;font-weight:bold;margin-top:6px;">{value}</div>
        </div>
        """,
        layout=widgets.Layout(width='130px', height='100px')
    )
```

---
## Initial Prompt 5
---

----------------------------------
Tool: ChatGPT
Date: 2025-05-22
----------------------------------
Me: Now that my widgets and styles are ready, how do I assemble and render the full dashboard?

Ai: Create your banner, your controls box, then wrap them with header and grid in a top-level VBox, and finally display(main_ui).

```python
Me: Now that my widgets and styles are ready, how do I assemble and render the full dashboard?

Ai: Create your banner, your controls box, then wrap them with header and grid in a top-level VBox, and finally display(main_ui).

```python
# Hover CSS injection
style = widgets.HTML("""<style> .card:hover { transform:… } </style>""")
display(style)

# Input controls
api_key = widgets.Password(...)
city_dd  = widgets.Dropdown(...)
btn      = widgets.Button(...)
btn.on_click(on_click)

# Display areas
header = widgets.HTML(...)
grid   = widgets.HBox(...)

# Banner & controls container
banner   = widgets.HTML(...)
controls = widgets.VBox([api_key, city_dd, btn], …)
main_ui  = widgets.VBox([banner, widgets.HBox([...]), grid], …)

     display(main_ui)
```
