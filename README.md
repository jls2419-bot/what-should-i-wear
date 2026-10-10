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

## Recommendation rules in plain English

- The app uses the **feels-like temperature** for five bands: freezing (32°F or below), cold (33–49°F), cool (50–60°F), mild (61–75°F), and warm (76°F or above).
- The selected plan changes the base outfit. Class, casual, and formal choices use different tops, bottoms, and shoes.
- Current rain, drizzle, snow, or thunderstorms trigger weather protection even when the maximum precipitation chance is low. If no wet condition is currently reported, a maximum precipitation chance of 50% or more also triggers protection.
- Freezing precipitation gets an insulated waterproof coat. Cold precipitation gets a warm layer under a waterproof outer layer. Milder wet conditions use a rain shell or, for formal plans, a water-resistant trench or raincoat.
- Wind at 22 mph or more adds windproof outerwear. A high–low difference of 18°F or more adds a removable layer when precipitation is not already determining the outer layer.
- The “Why this suggestion?” text describes the temperature, temperature range, precipitation trigger, and wind only when each one affected the result. The page also reminds users to adjust layers for their own comfort.

## Recent review fixes

- Combined warmth with precipitation protection, so freezing rain or snow no longer produces only a thin rain shell.
- Distinguished current rain, snow, and thunderstorms from a forecast precipitation chance in the explanation.
- Added a sandal illustration for the warm casual leather-sandal recommendation and aligned formal wet footwear with the dress-shoe illustration.
- Used a neutral title when no outer layer is recommended.
- Kept preview captions tied to the same garment strings used in the written outfit list, and allowed long captions to wrap on small screens.

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

### Controlled rule tests performed for the recent review

The current `outfitFor()` function was executed with simulated weather objects. These were rule tests, not live browser or live weather tests. All 21 assertions passed:

- Freezing rain and freezing snow both produced an insulated waterproof coat and waterproof boots. The snow case named current snow, added waterproof gloves, and did not show an umbrella.
- Cold rain produced a warm layer under a waterproof outer shell.
- Current rain and current snow with a low (10%) precipitation chance still added protection and described the current condition rather than the chance.
- Clear conditions with a 70% maximum precipitation chance added protection and described the precipitation chance.
- Warm, dry casual conditions produced leather sandals with the sandal preview icon.
- Mild, dry, low-wind conditions with a small high–low range produced no outer layer and used the neutral title “A suggested outfit for your plans.”
- Class, casual, and formal cases produced different base outfits.
- The temperature boundaries 31, 32, 33, 49, 50, 51, 60, 61, 62, 74, 75, and 76°F matched the documented bands.

### Live API check performed

A read-only check of the Open-Meteo endpoints succeeded: the geocoding endpoint resolved New York, New York, and the forecast endpoint returned the current and daily fields the page requests, including apparent temperature, weather code, wind speed, high/low temperatures, and maximum precipitation probability. This confirms endpoint availability for that check; it does not replace testing the page in a user’s browser.

### Browser and mobile check

No rendered browser or mobile-sized preview was completed during this review because a local browser automation session was unavailable. The responsive CSS remains in place, and the preview captions were updated to wrap long text on narrow screens, but this should still be visually checked on a phone or a narrow browser window.

## Limitations

- Suggestions use general weather rules and cannot know how warm or cold an individual usually feels.
- The app cannot know which clothes, colors, or weatherproof items are available in a person’s wardrobe.
- It does not know how long someone will spend indoors versus outdoors, which can change whether an outer layer is useful.
- Live results depend on an internet connection and the availability and accuracy of Open-Meteo data.

## Reflection

The first version worked, but it did not fully match what I wanted. The main interaction was clear, but asking users to enter the weather themselves made the tool feel less useful. The result was also easy to miss. Testing helped me notice both problems. I first improved how the result appeared, and then changed the main interaction so the user could enter a location and receive a suggestion based on real weather.

Codex helped me create the code, connect the weather APIs, and turn my revision ideas into working features. I still had to decide what the tool should do, test whether it felt clear, and recognize when the recommendations were too repetitive. The final version is closer to my intention, but it still depends on an internet connection and an outside weather service. The recommendations also use general rules, so they cannot fully understand someone’s personal style, wardrobe, or how warm or cold they usually feel.
