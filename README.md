# Pokemon Trading Card Game (TCG) -- Extract Load & Transform Pipeline
**Why This Project:** This is a self-directed learning project to build a data pipeline for a childhood favorite--Pokemon cards! I grew up with this trading card game and hold a particular nostalgia for older cards as well as an excitement for new ones. I often spent summer days re-organizing my collections around different card attributes like rarity, energy color and trainers/energies/pokemon (I thought the former 2 were useless unless the art was cool). This was my first experience with the `GROUPBY` operation and data features--I was doomed to work with data from a young age it seems.

## Business Requirements
When designing a data pipeline, the business context and use cases are critical. A personal project for Pokemon is no different--though some requirements are intended as plausible constraints rather than derived from a stakeholder.

Accordingly, I will define three user personas that this data pipeline will ultimately serve through as-of-yet-unbuilt analytics layers:
- :chart_with_upwards_trend: **Pokemon Card Retailer**: this user wants to understand the market conditions for an inventory of cards as well as recommendations for future acquisitions.
- :100: **Pokemon Card Collector**: this user has "Gotta Catch 'em All!" and wants to understand the current state of their collection and how to optimally acquire missing cards. They share similar needs as a **Retailer** persona.
- :trophy: **Tournament Player**: this user wants to build decks to win tournaments. The details of the cards and their interactions are important to list-building, with acquisition price being less of a consideration. They share a similar need as **Collectors** to understand the state of their collection and thus what decks can be built from it.

The needs for each persona are enumerated in the following table:

| # | Data Need | :chart_with_upwards_trend: **Retailer** | :100: **Collector** | :trophy: **Player** |
|---|-----------|-----------------------------------------|---------------------|---------------------|
| 1 | Know the state of their collection/inventory | :white_check_mark: | :white_check_mark:| :white_check_mark: |
| 2 | Know the value of their collection/inventory | :white_check_mark: | :white_check_mark:| :x: |
| 3 | When purchasing, know which cards are over/under-priced | :white_check_mark: | :white_check_mark:| :x: |
| 4 | When purchasing, know which cards have liquidity | :white_check_mark: | :x:| :x: |
| 5 | When selling, know how to price cards for sale | :white_check_mark: | :x:| :x: |
| 6 | Understand which card attributes drive price | :white_check_mark: | :x:| :x: |
| 7 | Understand which card attributes drive deck-inclusion | :x: | :x:| :white_check_mark: |
| 8 | Know the best decks that can be built from a personal collection | :x: | :x: | :white_check_mark: |
| 9 | Know the best decks that can be built from a new card set | :x: | :x: | :white_check_mark: |
| 9 | Know the best decks that can be built from a total card market | :x: | :x: | :white_check_mark: |
| 10 | Understand the market dynamics of price with meta deck inclusion | :white_check_mark: | :x:| :white_check_mark: |



