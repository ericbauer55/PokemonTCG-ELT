# Pokemon Trading Card Game (TCG) -- Extract Load & Transform Pipeline
**Why This Project:** This is a self-directed learning project to build a data pipeline for a childhood favorite--Pokemon cards! I grew up with this trading card game and hold a particular nostalgia for older cards as well as an excitement for new ones. I often spent summer days re-organizing my collections around different card attributes like rarity, energy color and trainers/energies/pokemon (I thought the former 2 were useless unless the art was cool). This was my first experience with the `GROUPBY` operation and data features--I was doomed to work with data from a young age it seems.

## 1. Business Requirements
When designing a data pipeline, the business context and use cases are critical. A personal project for Pokemon is no different--though some requirements are intended as plausible constraints rather than derived from a stakeholder.

Accordingly, I will define three user personas that this data pipeline will ultimately serve through as-of-yet-unbuilt analytics layers:
- :chart_with_upwards_trend: **Pokemon Card Retailer**: this user wants to understand the market conditions for an inventory of raw (i.e. "ungraded") cards as well as recommendations for future acquisitions.
- :100: **Casual Pokemon Card Collector**: this user has "Gotta Catch 'em All!" and wants to understand the current state of their collection and how to optimally acquire missing cards. They share similar needs as a **Retailer** persona.
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

### Note on Prices: Raw vs. Graded
There are two main pricing categories of Pokemon cards--raw cards and graded cards. Raw cards are cards pulled from booster packs or sold in deck boxes. These are the cards that a casual collector or high-volume retailer will interface with. All of these raw cards can undergo a ["grading"](https://www.reddit.com/r/Pokemoncardappraisal/comments/k53fey/grading_cards_the_basics/) process with a company that certifies the authenticity and condition of the card. Grades range from 1 (poor condition) to 9 (near-mint condition) to 10 (gem mint). Nowadays, cards are printed and packaged in high volumes, so the grade is as much a mark of how well it has been cared for as it is how well it was manufactured.. The process of sending cards away to be graded costs money and time, and it is usually reserved for "highly-collectible" cards that are worth the certification cost. Additionally, anyone can grade a card, but only companies like PSA or BGS--typical for Pokemon and Magic: The Gathering cards, respectively--are reputable enough for the certification to enhance the value of a card. 

For this project, we will ignore the pricing data for graded cards. Their usefulness extends to a more advanced collector and a retailer with a business model focused on individual cards. Sites like [TCGFish](https://tcgfish.com/) offer more advanced data collection on graded cards, while sites like [TCGPlayer](https://www.tcgplayer.com/) offer raw card prices.

## 2. Technical Requirements
## 2a. Extraction Process
There are nearly 100 different card sets released since the English base set hit the shelves in 1999. There are also epochs of sets correlating with the releases of Pokemon generations and new games. [The card game has undergone different evolutions during this time.](https://www.pokemon.com/us/pokemon-news/pokemon-tcg-scarlet-violet-brings-changes-to-the-pokemon-trading-card-game?) Collecting the data for all of the cards released since then could be a gargantuan task; however, others have been tracking cards on websites for quite a while. Website like TCGPlayer act as online marketplaces where sets and cards are logically indexed for searching, listing and purchasing cards. So, now the question is...

### To Scrape or to Use an API?
The answer to this question is almost certainly to *use an API*, though it depends on cost/rate-limits/availability. For instance, [TCGPlayer's API](https://developer.tcgplayer.com/) is no longer being supported as the site focuses on core offerings. This means that in order to acquire its nicely indexed data, I would need to build a scraper bot. From a respectful standpoint, this scraping is allowed by the generous terms of the sites [robots.txt](https://www.tcgplayer.com/robots.txt) page--though it requests 10 second periods between requests. The process of acquiring backfill data would take a long time at this rate. Luckily the attributes of Pokemon cards rarely (if at all) change once printed, and it is only the price data that changes regularly. To estimate the scraping effort for daily price updates on all cards, we can estimate ~180 cards per set at 100 sets at 10 seconds per request ~= 180,000 seconds (50 hours). This clearly does not allow for daily price updates--even as a ballpark estimate. The update rate of prices is proportional to each card's liquidity, however. Thus the sampling rate for scraping card prices can be proportional to the recent sales frequency of each card.

The complexity of this scraping approach depends on whether the website dynamically serves the content or statically serves the content. A dynamic website needs [`Selenium`](https://selenium-python.readthedocs.io/), a Python library for headless running a browser user-agent. A lower effort solution of `BeautifulSoup` and `requests` Python libraries would wokr if the site serves static content. In either case, the stability of the scraper depends on the front-end HTML structure. Changes to the user interface on the website risks crashing the scraper and potentially lost data during the HTML re-parsing.

**A Solution Appears:** 

## 2b. Load Process

## 2c. Transform Process

## 2d. Orchestration





