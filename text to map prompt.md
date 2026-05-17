I want to create an OpenClaw Telegram integration for generating Google Travel Maps by chat. It should include:

1. Create a map from natural language, e.g. “I’m going to Paris in a month, create [paris-map],” with default layers: Eat, Drink, Do.
2. Add places by chat with name, street/location, description, and automatic layer/icon rules: Eat = blue, dessert = pink; Drink coffee = brown, cocktails/beer = purple; Do = black.
3. If category details are missing, ask follow-up questions: Eat/Drink/Do, dessert or not, coffee or cocktails/beer.

For the most part, it's integrating with Google Maps Places API as a tool, and then figuring out the ruleset. 

Ensure to use best practices. Double check the already existing code. Changes to other parts of the code must not be made without permission.

Ask me for context if there are edge case flows that you can think of but are not sure what to do.

Use red/green test driven development. 

---
### action map

| User action                                             | Typical Google API hit              | Cost trigger? | Notes                                                                                                                                                                              |
| ------------------------------------------------------- | ----------------------------------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Create a map in my Google account                       | None                                | No            | This is just your own app/database unless you call a Google API. [](https://developers.google.com/maps/documentation/javascript/usage-and-billing)                                 |
| Create a layer                                          | None                                | No            | Layer organization is app-side metadata, not a Places API feature. [](https://developers.google.com/maps/documentation/javascript/usage-and-billing)                               |
| Type in a search box for a place                        | Place Autocomplete                  | Yes           | Each autocomplete flow uses Autocomplete requests/session pricing, depending on whether you use session tokens correctly.                                                          |
| Select a prediction from autocomplete                   | Place Details or place ID follow-up | Usually yes   | Selection alone is not the charge; the follow-up details request is commonly the terminating billed request.                                                                       |
| Search by free-text place name without autocomplete     | Text Search                         | Yes           | If you call Places Text Search instead of Autocomplete, that search request is billable. [](https://developers.google.com/maps/documentation/places/web-service/usage-and-billing) |
| Convert address to coordinates                          | Geocoding API                       | Yes           | Address-to-lat/lng is a separate billable API family. [](https://developers.google.com/maps/billing-and-pricing/pricing)                                                           |
| Add a marker to a layer using already-known lat/lng     | None                                | No            | Rendering or storing a marker is client/app-side; the expensive part was getting the location data.                                                                                |
| Add a description/note to the marker                    | None                                | No            | Your own text metadata does not hit Google unless you ask Google for generated/place content. [](https://developers.google.com/maps/documentation/javascript/usage-and-billing)    |
### common flows

If your flow is search → choose place → save to layer with your own description, the usual Google hits are: Autocomplete while typing, then Place Details after selection, then everything after that can be free if you only save the result to your DB. I would say this is the main flow. 

If your flow is paste address → convert to point → save to layer, the usual hit is Geocoding, and the actual “save to layer” step is still free. https://developers.google.com/maps/billing-and-pricing/pricing

If your flow is open map, click around, and drop markers manually, you usually pay for the map load if it is a Google interactive map, but not for each marker you add.
### what changes the bill

The biggest cost swing is whether you use autocomplete sessions correctly. With Autocomplete (New), Google groups requests using a session token, and billing depends on how the session terminates; for place-discovery flows terminated by Place Details, autocomplete requests in the session are billed under session pricing rather than as unrelated standalone lookups.

The second big swing is your Place Details field mask. Asking only for minimal fields costs less than asking for richer fields like ratings, reviews, current hours, and other higher-tier details.