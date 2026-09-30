# Fnac.com Scraper: Product Prices, EAN, Stock, Marketplace Sellers & Reviews (France)

[![Run on Apify](https://img.shields.io/badge/Apify-Run%20the%20Actor-00A67E?logo=apify&logoColor=white)](https://apify.com/fayoussef/fnac-data-scraping?fpr=youssef)
![EAN](https://img.shields.io/badge/EAN-and%20SKU-2ea44f)
![Marketplace](https://img.shields.io/badge/Marketplace-all%20sellers-1C7ED6)
![Search](https://img.shields.io/badge/Search-URL%20or%20keyword-8B5CF6)
![Export](https://img.shields.io/badge/Export-JSON%20%7C%20CSV%20%7C%20Excel-F59E0B)

> ### ▶️ [Run the Fnac.com Scraper on Apify](https://apify.com/fayoussef/fnac-data-scraping?fpr=youssef)
> Scrape **fnac.com** product data: price, list price, discount, **EAN**, SKU, brand, stock, **marketplace sellers and their prices**, ratings, reviews, full specs and images. Paste a Fnac URL or search by keyword with filters.

**Fnac.com Scraper** turns fnac.com, France's largest electronics and culture retailer, into clean product data: one record per product with numeric prices, identifiers, stock, every marketplace offer and customer reviews. It is built for price monitoring, retail and competitor intelligence, EAN catalog matching and marketplace research. This repository documents the Apify Actor and gives working Python, JavaScript and cURL examples for calling it through the API.

- **Run it in the browser:** [fayoussef/fnac-data-scraping on Apify](https://apify.com/fayoussef/fnac-data-scraping?fpr=youssef)
- **Guide and docs:** [automationbyexperts.com/apify/fnac-data-scraping](https://automationbyexperts.com/apify/fnac-data-scraping)
- **Actor ID for the API:** `fayoussef/fnac-data-scraping`

## What the Fnac scraper does

- **Any fnac.com page**: search results, categories, category hubs, brand pages and single products (including marketplace `/mp` listings).
- **Search by keyword, no URL needed**: type search terms and filter by category, brand, price range, sold by Fnac, condition and stock.
- **Every marketplace offer**: seller name, price, condition, seller rating, shipping cost and delivery time.
- **EAN, SKU and manufacturer reference** for catalog matching.
- **Customer reviews** with rating, title, text, date and verified purchase flag.
- **Full spec table**, often 50+ rows for electronics.
- **No API key, no Fnac account**: pagination, Fnac's anti-bot protection and French residential proxies are handled for you.

## Output fields: what data you get

One record per product. The main fields:

| Field | Description |
|---|---|
| `name` / `url` / `brand` / `categories` | Product identity |
| `ean` / `sku` / `mpn` | EAN barcode, Fnac reference, manufacturer part number |
| `price` / `original_price` / `discount_pct` / `promotion_label` | Price, list price and discount |
| `availability` / `in_stock` / `store_availability` | Online and in-store stock |
| `seller` / `seller_type` | Who sells it (Fnac or a marketplace seller) |
| `other_sellers` / `offers_new_count` / `offers_used_count` | Every marketplace offer |
| `rating` / `review_count` / `reviews` | Ratings and customer reviews |
| `characteristics` | Full technical specification table |
| `description` / `images` | Product text and images |
| `energy_class` / `repairability_index` / `warranty_options` | Extras |

## Input

Paste fnac.com URLs, or leave them empty and search by keyword:

| Field | What it does |
|---|---|
| `start_urls` | Search, category, brand or product URLs |
| `search_terms` | Keywords, e.g. `ordinateur portable` |
| `category` / `brands` | Category and brand filters |
| `min_price` / `max_price` | Price range in EUR |
| `sold_by_fnac` / `condition` / `in_stock_only` | Seller, new or used, in stock |
| `sort_by` | Sort order |
| `max_depth` / `max_items` | Pages per search and total products |

## Use cases

- **Price monitoring**: track Fnac prices and discounts on your products every day.
- **Competitor intelligence**: see which marketplace sellers undercut you and by how much.
- **EAN catalog matching**: match Fnac products to your catalog by barcode.
- **Brand protection**: find unauthorised sellers of your brand on the Fnac marketplace.
- **Review analysis**: collect customer reviews for product research.

Ready-made examples you can run in one click:

- [Scrape Fnac laptop prices, EAN and stock in France](https://apify.com/fayoussef/fnac-data-scraping/examples/fnac-laptop-prices-france?fpr=youssef): Exports every laptop in the fnac.com Tous les ordinateurs portables category with current price, crossed-out list price, discount, EAN, SKU, brand, stock status, marketplace sellers, ratings and the full spec table. Ready for price monitoring and EAN matching against Amazon.fr or Cdiscount.

## Quick start

### 1. In the browser (no code)

1. Open the Actor on Apify and click **Try for free**.
2. Paste a fnac.com search, category or product URL, or type search terms and pick filters.
3. Click **Start**, then download Excel, CSV or JSON from the **Output** tab.

### 2. Through the API

1. Create a free [Apify account](https://console.apify.com/sign-up?fpr=youssef) and copy your API token from [Settings > Integrations](https://console.apify.com/settings/integrations).
2. Set it as an environment variable: `export APIFY_TOKEN=...` (PowerShell: `$env:APIFY_TOKEN="..."`).
3. Edit [`input.json`](input.json) and run one of the examples below.

#### Python

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

#### JavaScript / Node.js

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

#### cURL (plain HTTP)

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

## Integrations and automation

- **Schedule it** daily for price and stock monitoring.
- **Send results** to Google Sheets, Airtable, Slack, a webhook, Make, Zapier or n8n with Apify integrations.
- **Use it from AI agents** through the Apify MCP server.

## FAQ

### Is there a Fnac API?
Fnac does not offer a public product API. This Actor is a Fnac API alternative that reads the same pages a shopper sees and returns structured JSON.

### Can I get the EAN of Fnac products?
Yes. `ean` holds the GTIN barcode, plus `sku` and `mpn`.

### Does it scrape Fnac marketplace sellers?
Yes. `other_sellers` lists every offer with seller, price, condition, rating, shipping and delivery time.

### Can I search Fnac by keyword?
Yes. Use `search_terms` with category, brand, price and stock filters.

### Does it work on fnacpro.com or other Fnac countries?
It is built for fnac.com (France).

### Are prices numbers or text?
Numbers: `649,99 €` arrives as `649.99`, ready for spreadsheets.

### What output formats are available?
JSON, CSV, Excel, XML and HTML from the Apify dataset, or through the API.

## Scraper Fnac en français

Le **Fnac.com Scraper** extrait les produits de fnac.com : prix, prix barré, remise, **EAN**, SKU, marque, stock, **vendeurs marketplace et leurs prix**, notes, avis clients, caractéristiques et images. Collez une URL Fnac ou recherchez par mot-clé avec filtres, puis exportez en Excel, CSV ou JSON. Idéal pour la veille tarifaire et la surveillance de la concurrence. [Essayer sur Apify](https://apify.com/fayoussef/fnac-data-scraping?fpr=youssef).

## Pricing

Pay per use on Apify: you are charged per event (results produced), with no subscription to this Actor. The current rate is shown on the [Actor's Store page](https://apify.com/fayoussef/fnac-data-scraping?fpr=youssef). Free-plan runs are capped; an [Apify plan](https://apify.com/pricing?fpr=youssef) unlocks full runs.

## Related scrapers by AutomationByExperts

- [Wallapop Scraper: Spain, France, Italy, Portugal & UK](https://github.com/automationbyexperts/wallapop-scraper)
- [Bulk AI Image Generator: Nano Banana & GPT Image](https://github.com/automationbyexperts/bulk-ai-image-generator)
- [Bulk LLM Runner: ChatGPT, Claude & Gemini in Bulk](https://github.com/automationbyexperts/bulk-llm-runner)
- [AutoTrader.ca Scraper: Canada Car Listings, VIN & Dealers](https://github.com/automationbyexperts/autotrader-canada-scraper)
- [Spitogatos.gr Scraper: Greek Real Estate Listings](https://github.com/automationbyexperts/spitogatos-scraper)
- [Canada411 Scraper: Phone Numbers & Addresses](https://github.com/automationbyexperts/canada411-scraper)
- [Full catalog of our web scraping APIs](https://github.com/automationbyexperts/web-scraping-apis)

## Support

Questions, bugs or a custom scraper: open an issue here, use the Issues tab on the [Apify page](https://apify.com/fayoussef/fnac-data-scraping?fpr=youssef), or email youssefarhan24@gmail.com.

## License

The example code in this repo is MIT licensed. The Actor itself runs on Apify under its own terms.
