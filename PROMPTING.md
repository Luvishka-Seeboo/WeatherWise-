---

Title: Prompting Journey for Weather Data Retrieval Function

---
## Initial Prompt 1
```

Write a function to retrieve weather data from OpenWeatherMap for Mauritius.

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

    ---

## Initial Prompt 2

```

Write a function to make the dashboard update more smoothly.

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
## Initial Prompt 3
```
Write a function to get current weather for Mauritius.
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

    
