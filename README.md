# Wine Inventory Converter

A comprehensive web-based tool for converting wine supplier price lists into standardized Excel spreadsheets. Supports 14 major wine importers and distributors with intelligent parsing for various formats.

## Features

- **14 Supplier Parsers** - Converts price lists from major wine importers
- **Standardized Output** - Consistent column structure across all suppliers
- **Large Format Support** - Properly converts bottle sizes (375ml, 750ml, 1.5L, 3L, 6L, etc.)
- **Multi-sheet Processing** - Handles complex spreadsheets with multiple tabs
- **Smart Data Extraction** - Intelligently extracts producers, regions, vintages, and pricing
- **Web-based Interface** - No installation required, runs in browser
- **Excel Output** - Generates clean, filterable Excel files with proper formatting

## Supported Suppliers

1. **ZRS (Zimmerman Robbins Selections)** - National pricebooks and spirits
2. **David Bowler Wine** - Complete inventory with country/region extraction
3. **Selections de la Viña** - Spanish wine specialists
4. **Vinum USA** - Italian wine importer
5. **Louis/Dressner Selections** - Natural wine importer
6. **Bon Vivant Imports** - With hyperlinks and country corrections
7. **Indigenous Selections** - Italian wine specialist
8. **Skurnik Wines** - Wine and spirits, multi-sheet support
9. **DNS Wines** - FOB and DI pricing
10. **Valkyrie Selections** - Imported and domestic wines, multi-sheet
11. **Diamond Wine Importers** - Greek wines with smart producer extraction
12. **Diamond Library Pre-Sale** - Back vintages and large formats
13. **Dalla Terra** - Italian wines with proper large format conversion
14. **Vinum USA** - Comprehensive Italian portfolio

## Quick Start

### Option 1: Use the Web App (Easiest)

1. Open `index.html` in a web browser
2. Select your supplier from the dropdown
3. Upload the price list Excel file
4. Click "Convert"
5. Download your clean Excel file

### Option 2: Python Scripts

```bash
# Install dependencies
pip install pandas openpyxl --break-system-packages

# Run a specific parser
python parsers/zrs_parser.py input_file.xlsx
```

## Output Format

All parsers generate standardized Excel files with these core columns:

- **Product Type** - Wine, Spirits, Sparkling, etc.
- **Country** - Country of origin
- **Region** - Wine region/appellation
- **Producer** - Winery/distillery name
- **Product Name** - Full product description
- **Vintage** - Year or NV (non-vintage)
- **Case Size** - Bottles per case
- **Bottle Size (ml)** - Standardized in milliliters
- **Pricing** - FOB, DI, or case pricing (varies by supplier)
- **Stock Status** - In Stock, Out of Stock, Pre-Sale, etc.

Additional columns vary by supplier (SKU, ABV, press scores, notes, etc.)

## Special Features

### Large Format Conversion
Automatically converts all bottle sizes to milliliters:
- 375ML → 375ml
- 750ML → 750ml
- 1.5L → 1500ml
- 3L → 3000ml
- 6L → 6000ml
- And more!

### Multi-Sheet Support
Handles complex spreadsheets:
- **Skurnik Wines** - Separate wine and spirits sheets
- **Valkyrie Selections** - Imported and domestic tabs
- **Diamond Library** - Annual pre-sale format

### Smart Producer Extraction
Intelligently extracts producer names from product descriptions:
- Pattern recognition for multi-word producers
- Handles various naming conventions
- Producer-to-country mapping for corrections

### Hyperlink Preservation
**Bon Vivant Imports** parser preserves product links for easy online ordering.

## File Structure

```
wine-inventory-converter/
├── index.html              # Main web application
├── README.md              # This file
├── LICENSE                # MIT License
├── parsers/               # Individual parser scripts
│   ├── zrs_parser.py
│   ├── bowler_parser.py
│   ├── vina_parser.py
│   ├── vinum_parser.py
│   ├── dressner_parser.py
│   ├── bonvivant_parser.py
│   ├── indigenous_parser.py
│   ├── skurnik_parser.py
│   ├── dns_parser.py
│   ├── valkyrie_parser.py
│   ├── diamond_parser.py
│   ├── diamond_library_parser.py
│   └── dallaterra_parser.py
└── examples/              # Sample input/output files
    ├── input/
    └── output/
```

## Technical Details

### Dependencies
- Python 3.8+
- pandas
- openpyxl
- Modern web browser (for web app)

### Browser Compatibility
The web app uses:
- SheetJS (xlsx.js) for Excel parsing
- Vanilla JavaScript (no frameworks)
- Works in all modern browsers (Chrome, Firefox, Safari, Edge)

## Contributing

Contributions welcome! To add a new supplier parser:

1. Create a new parser function following the existing patterns
2. Add supplier to the dropdown in `index.html`
3. Update the supplier list in README.md
4. Test with sample files
5. Submit a pull request

## Known Limitations

- Hyperlinks cannot be extracted in the web app (use Python scripts for this)
- Browser storage not supported in Claude.ai artifacts
- Large files (>10MB) may be slow in browser

## License

MIT License - see LICENSE file for details

## Author

Created for wine industry professionals to streamline inventory management and ordering workflows.

## Version History

- **v1.0** (Feb 2026) - Initial release with 14 supplier parsers
- Complete large format conversion support
- Multi-sheet processing
- Smart producer extraction
- Country correction mapping

## Support

For issues, feature requests, or questions, please open an issue on GitHub.

---

**Happy converting! 🍷**
