# Fnac.com Scraper: Prices, EAN, Stock, Sellers & Reviews

Scrape fnac.com products from any search, category or product URL, or by keyword with brand, category, price, seller and stock filters. Get price, list price, discount, EAN, SKU, brand, stock, marketplace sellers, ratings, reviews, specs and images. No API key needed.

This repo shows how to call the [Fnac.com Scraper: Prices, EAN, Stock, Sellers & Reviews](https://apify.com/fayoussef/fnac-data-scraping?fpr=youssef) Apify Actor from your own code: a Python and a JavaScript example, the input they send, and a sample of the output. Everything runs in the Apify cloud, so there is nothing to host, scale or maintain on your side.

- **Run it in the browser:** [fayoussef/fnac-data-scraping on Apify](https://apify.com/fayoussef/fnac-data-scraping?fpr=youssef)
- **Guide and docs:** [automationbyexperts.com/apify/fnac-data-scraping](https://automationbyexperts.com/apify/fnac-data-scraping)
- **Actor ID for the API:** `fayoussef/fnac-data-scraping`

## Use cases

- [Scrape Fnac laptop prices, EAN and stock in France](https://apify.com/fayoussef/fnac-data-scraping/examples/fnac-laptop-prices-france?fpr=youssef): Exports every laptop in the fnac.com Tous les ordinateurs portables category with current price, crossed-out list price, discount, EAN, SKU, brand, stock status, marketplace sellers, ratings and the full spec table. Ready for price monitoring and EAN matching against Amazon.fr or Cdiscount.
- [Find Lenovo and HP laptops under 600 EUR sold by Fnac](https://apify.com/fayoussef/fnac-data-scraping/examples/fnac-lenovo-hp-laptops-under-600?fpr=youssef): Searches fnac.com for laptops, keeps only new Lenovo and HP models under 600 EUR that are sold by Fnac and in stock, cheapest first. Each result has the price, list price, discount, EAN, stock status, rating and full specifications. Change the brands or budget to track any laptop deal.
- [Casques Bluetooth Sony vendus par Fnac, les mieux notés](https://apify.com/fayoussef/fnac-data-scraping/examples/fnac-casques-sony-bluetooth-vendus-par-fnac?fpr=youssef): Recherche les casques et écouteurs Bluetooth Sony sur fnac.com, garde uniquement ceux vendus par Fnac et les classe par note client. Chaque produit comprend le prix, le prix barré, la remise, l'EAN, la disponibilité, la note, les avis et les caractéristiques. Changez la marque ou le mot-clé pour suivre n'importe quel produit audio.
- [Meilleures ventes de romans policiers Fnac avec EAN](https://apify.com/fayoussef/fnac-data-scraping/examples/fnac-romans-policiers-meilleures-ventes?fpr=youssef): Recherche les romans policiers dans la catégorie Livres de fnac.com, classés par meilleures ventes. Chaque livre comprend le prix, l'EAN (ISBN), l'auteur, la disponibilité, la note, les avis et le résumé. Idéal pour les libraires et éditeurs qui suivent les prix et le classement Fnac. Changez le mot-clé pour suivre n'importe quel genre.

## Quick start

1. Create a free [Apify account](https://console.apify.com/sign-up?fpr=youssef) and copy your API token from [Settings > Integrations](https://console.apify.com/settings/integrations).
2. Set it as an environment variable: `export APIFY_TOKEN=...` (PowerShell: `$env:APIFY_TOKEN="..."`).
3. Edit [`input.json`](input.json) and run one of the examples below.

### Python

```bash
pip install apify-client
python examples/python/run_actor.py
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("fayoussef/fnac-data-scraping").call(run_input={'start_urls': [{'url': 'https://www.fnac.com/Tous-les-ordinateurs-portables/Ordinateurs-portables/nsh154425/w-4'}],
 'max_depth': 3})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

### JavaScript / Node.js

```bash
npm install apify-client
node examples/javascript/run_actor.mjs
```

```javascript
import { ApifyClient } from "apify-client";

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor("fayoussef/fnac-data-scraping").call({
    "start_urls": [
        {
            "url": "https://www.fnac.com/Tous-les-ordinateurs-portables/Ordinateurs-portables/nsh154425/w-4"
        }
    ],
    "max_depth": 3
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

### cURL (plain HTTP)

Runs the Actor and returns the dataset items in one synchronous call:

```bash
curl -X POST "https://api.apify.com/v2/acts/fayoussef~fnac-data-scraping/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d @input.json
```

Synchronous calls time out after 300 seconds. For larger runs use the client libraries above, or start the run with `POST /v2/acts/fayoussef~fnac-data-scraping/runs` and read the dataset when it finishes.

## Sample output

One record, from [`sample-output.json`](sample-output.json). Export the full dataset as JSON, CSV, Excel or HTML from the Apify Console, or read it through the API as shown above.

```json
{
  "url": "https://www.fnac.com/PC-portable-HP-EliteBook-840-G8-14-Intel-Core-i5-16-Go-RAM-256-Go-SSD-Argent-Reconditionne-Grade-B/a22470972/w-4",
  "product_id": "22470972",
  "name": "PC portable HP EliteBook 840 G8 Full HD 14\" Intel® Core™ i5 16 Go RAM 256 Go SSD Argent Reconditionné",
  "brand": "HP",
  "brand_url": "https://www.fnac.com/HP/m58980/w-4",
  "ean": "3701637874862",
  "sku": "9329650",
  "mpn": "50061",
  "product_type": "PC Portable",
  "price": 429,
  "original_price": 699,
  "currency": "EUR",
  "discount_pct": "-39%",
  "promotion_label": "Offre Fnac*",
  "eco_tax": 4.3,
  "availability": "conditional_4_to_12_days",
  "in_stock": true,
  "condition": "new",
  "is_refurbished": true,
  "seller": "FNAC.COM",
  "seller_type": "fnac",
  "other_sellers": [
    {
      "name": "KIATOO",
      "price": 409,
      "condition": "used",
      "condition_detail": "Correct",
      "seller_rating": 4.1,
      "seller_sales": 4468,
      "shipping_cost": 0,
      "delivery": "Livré entre le 19/09 et le 22/09"
    }
  ],
  "offers_new_count": 0,
  "offers_used_count": 3,
  "rating": 4.5,
  "rating_count": 4,
  "review_count": 4,
  "categories": [
    "Informatique",
    "Ordinateurs portables",
    "Par marque",
    "PC Portable HP"
  ],
  "characteristics": {
    "Marque du processeur": "INTEL",
    "Modèle du processeur": "Intel Core i5 1145G7",
    "Processeur": "Intel® Core™ i5 1145G7"
  },
  "image": "https://static.fnac-static.com/multimedia/Images/FR/MDM/b0/ef/bb/29093808/3756-1/tsp20260903173707/PC-portable-HP-EliteBook-840-G8-Full-HD-14-Intel-Core-i5-16-Go-RAM-256-Go-D-Argent-Reconditionne.jpg",
  "images": [
    "https://static.fnac-static.com/multimedia/Images/FR/MDM/b0/ef/bb/29093808/3756-1/tsp20260903173707/PC-portable-HP-EliteBook-840-G8-Full-HD-14-Intel-Core-i5-16-Go-RAM-256-Go-D-Argent-Reconditionne.jpg"
  ],
  "page_template": "fnac-nextjs",
  "scraped_at": "2026-09-11T18:20:45Z"
}
```

## Pricing

Pay per use on Apify: you are charged per event (results produced), with no subscription to this Actor. The current rate is shown on the [Actor's Store page](https://apify.com/fayoussef/fnac-data-scraping?fpr=youssef). Free-plan runs are capped; an [Apify plan](https://apify.com/pricing?fpr=youssef) unlocks full runs.

## More Actors by AutomationByExperts

- [wallapop Scraper (Spain,Italy,Portugal)](https://github.com/automationbyexperts/wallapop-scraper)
- [Bulk AI Image Generator (NO API KEY)](https://github.com/automationbyexperts/bulk-ai-image-generator)
- [Bulk LLM Runner GPT, Claude, Perplexity, Kimi (No API Key)](https://github.com/automationbyexperts/bulk-llm-runner)
- [AutoTrader Canada Car Scraper: Prices, VIN, Mileage & Dealers](https://github.com/automationbyexperts/autotrader-canada-scraper)
- [Spitogatos.gr Scraper: Greek Property Listings & Agent Phones](https://github.com/automationbyexperts/spitogatos-scraper)
- [Canada411 Scraper: Business Phones, Addresses](https://github.com/automationbyexperts/canada411-scraper)
- [Full catalog of our web scraping APIs](https://github.com/automationbyexperts/web-scraping-apis)

## Support

Questions, bugs or a custom scraper: open an issue here, use the Issues tab on the [Apify page](https://apify.com/fayoussef/fnac-data-scraping?fpr=youssef), or email youssefarhan24@gmail.com.

## License

The example code in this repo is MIT licensed. The Actor itself runs on Apify under its own terms.
