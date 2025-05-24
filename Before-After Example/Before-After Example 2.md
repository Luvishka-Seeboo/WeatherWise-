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
def build_dashboard():
    # — Style injection (once) —
    style = widgets.HTML("""<style> .card:hover { transform: translateY(-6px) scale(1.02); } </style>""")

    # — Inputs —
    api_key = widgets.Password(description="API Key:", layout=widgets.Layout(width='340px'))
    city_dd  = widgets.Dropdown( options=[…], description="City:", layout=widgets.Layout(width='340px'))
    btn      = widgets.Button(description="Show Weather", button_style='info', layout=widgets.Layout(width='160px'))

    # — Display areas —
    header = widgets.HTML("<h3>Enter API key & select a city</h3>", layout=widgets.Layout(padding='8px'))
    grid   = widgets.HBox([], layout=widgets.Layout(justify_content='space-around', padding='12px'))

    # — Layout —
    banner   = widgets.HTML("<div style='…'>🇲🇺 Mauritius Weather</div>")
    controls = widgets.VBox([api_key, city_dd, btn], layout=widgets.Layout(padding='10px', border='1px solid #ddd'))
    ui       = widgets.VBox([style, banner,
                             widgets.HBox([controls, header]),
                             grid],
                            layout=widgets.Layout(width='760px'))

    # Attach references for updates
    ui.api_key = api_key
    ui.city_dd  = city_dd
    ui.btn      = btn
    ui.header   = header
    ui.grid     = grid
    return ui

# Build it once
dashboard = build_dashboard()
display(dashboard)

# Refined handler
def on_click(b):
    key = dashboard.api_key.value.strip()
    city = dashboard.city_dd.value

    if not key:
        dashboard.header.value = "<h3 style='color:red;'>❌ Enter API key!</h3>"
        dashboard.grid.children = []
        return

    w = get_weather(city, key) or {}
    if not w:
        dashboard.header.value = "<h3 style='color:red;'>❌ Could not fetch weather</h3>"
        dashboard.grid.children = []
        return

    # Update header & cards in place
    icon = w["Icon"]
    dashboard.header.value = f"<h2>{w['City']} — {w['Condition']}</h2>"
    dashboard.grid.children = [
        make_card("Temp", w["Temp"],      "linear-gradient(…)")
        # …other cards…
    ]

# Wire up once
dashboard.btn.on_click(on_click)

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

