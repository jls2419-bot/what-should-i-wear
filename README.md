# What Should I Wear?

## Original idea

I want to make a simple outfit helper for students or anyone who has trouble deciding what to wear before going out. Users enter their location and where they’re going, and the page uses today’s local weather to suggest an outfit with a short explanation.

When someone enters their location and plans, the experience should use today’s local weather to give them a practical outfit suggestion.

## Open the page

1. Open the `index.html` file in any modern web browser.
2. Enter a city and state (for example, `New York, NY`) or a ZIP code.
3. Select Class, Casual outing, or Formal event.
4. Select **Check weather & suggest**.
5. Wait for the live weather lookup. The result shows the resolved location, current and feels-like temperature, today’s high/low, weather condition, maximum rain chance, wind speed, and a matching outfit.

## Live weather data

This version requires an internet connection. It uses the [Open-Meteo Geocoding API](https://open-meteo.com/en/docs/geocoding-api) to resolve a city/state or ZIP code, then the [Open-Meteo Forecast API](https://open-meteo.com/en/docs) for live local weather. Weather is requested in Fahrenheit and the resolved location’s local timezone. No API key or installation is required.

## AI tool and selected prompts

I used OpenAI Codex to build and revise the project.

### Initial build

> Build a simple “What Should I Wear?” outfit helper. Let the user enter the temperature, choose whether it is raining, and select an occasion. Generate an outfit suggestion with a short explanation.

### Making the result clearer

> I tested the first version and found that the outfit result was not visually noticeable enough. Make the result card more prominent, automatically scroll it into view, add a short animation, and include a visual outfit preview.

### Adding live weather

> After testing, I found that manually entering the weather made the suggestions feel limited and repetitive. Replace those inputs with a location field and use today’s local weather to generate the outfit.

## Testing results

I first tested the page with 24°F, no rain, and Class selected. The outfit itself made sense because it suggested a warm sweater or hoodie, comfortable pants, and sneakers. However, the result appeared below the form and blended into the page, so I needed a few seconds to find it.

I revised the result card by adding stronger contrast, automatic scrolling, animation, and an outfit preview. After testing again, the result was much easier to notice. I later changed the manual weather inputs to a location search because the original recommendations felt too simple and repetitive. The final version successfully loads local weather and uses it with the selected occasion to generate the outfit.

## Reflection

The first version worked, but it did not fully match what I wanted. The main interaction was clear, but asking users to enter the weather themselves made the tool feel less useful. The result was also easy to miss. Testing helped me notice both problems. I first improved how the result appeared, and then changed the main interaction so the user could enter a location and receive a suggestion based on real weather.

Codex helped me create the code, connect the weather APIs, and turn my revision ideas into working features. I still had to decide what the tool should do, test whether it felt clear, and recognize when the recommendations were too repetitive. The final version is closer to my intention, but it still depends on an internet connection and an outside weather service. The recommendations also use general rules, so they cannot fully understand someone’s personal style, wardrobe, or how warm or cold they usually feel.
