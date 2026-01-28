# ManaBox Collection Data Enrichment

A Python notebook that enhances ManaBox Magic: The Gathering collection exports with comprehensive card data from the Scryfall API.

## Overview

This tool takes a CSV export from the ManaBox collection management app and enriches it with detailed card information from Scryfall, including prices, legality, oracle text, images, and more. The result is a comprehensive Excel file with your complete collection data ready for analysis, tracking, or organization.

## What It Does

The notebook:
- Reads your ManaBox collection export (CSV format)
- Fetches detailed card data from the Scryfall API for each card
- Handles dual-faced cards, adventures, and modal cards correctly
- Converts mana symbols and card text to human-readable format
- Exports an enriched Excel file with 40+ data fields per card

## Features

### Data Enrichment
- **Base Identity**: Card name, Oracle ID, layout, rarity, language
- **Color & Mana**: Colors, color identity, mana cost, mana value, produced mana
- **Stats**: Power, toughness (for creatures)
- **Legality**: Commander format legality, EDHREC rank
- **Text**: Type line, keywords, oracle text, flavor text (human-readable format)
- **Set Information**: Set code, set name, collector number, release date
- **Pricing**: USD price for normal and foil versions
- **Media**: Image URLs and Scryfall page links
- **Dual-Face Support**: Separate data for both faces of transforming/modal cards

### ManaBox Original Data Preserved
- Quantity
- Foil status
- Condition
- Purchase price
- Misprint/Altered status
- Language
- ManaBox and Scryfall IDs

## Requirements

- Python 3.x
- Google Colab (recommended) or Jupyter Notebook
- Required libraries:
  - pandas
  - requests
  - openpyxl
  - json
  - re

## Usage

### Step 1: Export Your ManaBox Collection
1. Open ManaBox app
2. Export your collection as CSV
3. Save the file

### Step 2: Run the Notebook
1. Open the notebook in Google Colab
2. Upload your ManaBox export when prompted
3. Rename the uploaded file to `ManaBox_Collection.csv` or update the `file_path` variable in the notebook
4. Run all cells sequentially

### Step 3: Download Results
- The enriched collection will be saved as `Complete_ManaBox_Collection.xlsx`
- Download the file from Colab's file browser

## Technical Details

### API Rate Limiting
The notebook includes a 100ms delay between API calls to respect Scryfall's rate limits (10 requests per second). For large collections, expect approximately:
- 100 cards: ~10 seconds
- 500 cards: ~50 seconds
- 1000 cards: ~2 minutes

### Mana Symbol Conversion
The notebook automatically converts mana symbols to readable text:
- `{W}` → White
- `{U}` → Blue
- `{B}` → Black
- `{R}` → Red
- `{G}` → Green
- `{C}` → Colorless
- `{T}` → Tap

### Error Handling
If a card fails to fetch from Scryfall (rare cases of API downtime or invalid IDs), the notebook will:
- Print a warning message with the Scryfall ID
- Continue processing remaining cards
- Include the original ManaBox data for that card

## Output Format

The resulting Excel file contains one row per card with the following columns:

**From ManaBox:**
- Quantity
- Card Name
- Set Code
- Card Number
- Foil
- Rarity
- Condition
- ManaBox ID
- Scryfall ID
- Purchase Price
- Misprint
- Altered
- Language
- Purchase Price Currency

**From Scryfall:**
- Name, Oracle ID, Layout, Rarity, Lang
- Colors, Color Identity, Mana Cost, Mana Value, Produced Mana
- Power, Toughness
- Commander Legal, EDHREC Rank, Digital Availability
- Type, Keywords, Printed Text, Flavor Text
- Set Code, Set Name, Collector Number, Release Date
- Price USD, Price USD Foil
- Image URL, Scryfall URI
- Face A/B data (for dual-faced cards)

## Use Cases

- **Collection Valuation**: Track current market prices for your entire collection
- **Deck Building**: Filter by legality, color identity, and card type
- **Inventory Management**: Identify high-value cards or gaps in your collection
- **Data Analysis**: Analyze collection trends, set distribution, or spending patterns
- **Trading**: Generate comprehensive lists for trades with accurate pricing

## Limitations

- Requires valid Scryfall IDs in the ManaBox export (included by default)
- Prices are USD only (Scryfall limitation)
- Processing time scales linearly with collection size due to API rate limits
- Requires internet connection for API calls

## Future Improvements

Potential enhancements:
- Batch API calls for faster processing
- Additional price sources (TCGPlayer, CardKingdom)
- Collection analytics/visualizations
- Filtering by format legality or price ranges
- Duplicate detection and consolidation

## Resources

- [ManaBox App](https://manabox.app/)
- [Scryfall API Documentation](https://scryfall.com/docs/api)
- [Magic: The Gathering Official Site](https://magic.wizards.com/)

## License

This project is provided as-is for personal use. Scryfall data is provided under [Scryfall's Terms of Service](https://scryfall.com/docs/terms).

---

**Built by Nate Dunning** | [npdfw.com](https://npdfw.com) | [LinkedIn](https://linkedin.com/in/npdunning)
