# Contributing to Wine Inventory Converter

Thank you for your interest in contributing! This document provides guidelines for contributing to the project.

## How to Contribute

### Reporting Bugs

1. Check existing issues to avoid duplicates
2. Create a new issue with:
   - Clear title describing the bug
   - Steps to reproduce
   - Expected vs actual behavior
   - Sample file (if applicable)
   - Browser/Python version

### Requesting Features

1. Check if feature already requested
2. Create issue with:
   - Use case description
   - Expected behavior
   - Why it would benefit users

### Adding New Supplier Parsers

We welcome new supplier parsers! Here's how to add one:

#### 1. Create the Parser

Create `parsers/newsupplier_parser.py`:

```python
import pandas as pd
from openpyxl import Workbook
from openpyxl.styles import Font, PatternFill, Alignment
import re

def parse_newsupplier(file_path):
    """
    Parse News Supplier price list into standardized format.
    
    Args:
        file_path: Path to the Excel file
        
    Returns:
        DataFrame with standardized columns
    """
    df = pd.read_excel(file_path, sheet_name=0, header=None)
    clean_data = []
    
    for idx in range(1, len(df)):  # Start after header
        # Your parsing logic here
        # Extract: producer, wine name, vintage, size, price, etc.
        
        clean_data.append({
            'Product Type': product_type,
            'Country': country,
            'Region': region,
            'Producer': producer,
            'Product Name': product_name,
            'Vintage': vintage,
            'Case Size': case_size,
            'Bottle Size (ml)': bottle_size_ml,
            'Case Price': case_price,
            'Stock Status': stock_status
        })
    
    return pd.DataFrame(clean_data)

def save_to_excel(df, output_path):
    """Save DataFrame to formatted Excel file."""
    wb = Workbook()
    sheet = wb.active
    sheet.title = 'Supplier Name'
    
    # Add headers with formatting
    headers = list(df.columns)
    for col_idx, header in enumerate(headers, start=1):
        cell = sheet.cell(row=1, column=col_idx, value=header)
        cell.font = Font(bold=True, color='FFFFFF')
        cell.fill = PatternFill(start_color='366092', end_color='366092', fill_type='solid')
        cell.alignment = Alignment(horizontal='center', vertical='center')
    
    # Add data
    for row_idx, row_data in enumerate(df.values, start=2):
        for col_idx, value in enumerate(row_data, start=1):
            cell = sheet.cell(row=row_idx, column=col_idx, value=value)
            cell.alignment = Alignment(vertical='top')
    
    # Set column widths
    column_widths = {'A': 15, 'B': 18, 'C': 30, 'D': 60, 'E': 12}
    for col, width in column_widths.items():
        sheet.column_dimensions[col].width = width
    
    sheet.auto_filter.ref = sheet.dimensions
    wb.save(output_path)

if __name__ == "__main__":
    import sys
    if len(sys.argv) < 2:
        print("Usage: python newsupplier_parser.py <input_file.xlsx>")
        sys.exit(1)
    
    df = parse_newsupplier(sys.argv[1])
    output_file = 'News_Supplier_Clean.xlsx'
    save_to_excel(df, output_file)
    print(f"Converted {len(df)} products to {output_file}")
```

#### 2. Add to Web App

In `index.html`, add to dropdown:

```html
<option value="newsupplier">News Supplier</option>
```

Add JavaScript parser function:

```javascript
function parseNewsSupplier(workbook) {
    const sheet = workbook.Sheets[workbook.SheetNames[0]];
    const rawData = XLSX.utils.sheet_to_json(sheet, { header: 1, defval: null });
    const cleanData = [];
    
    // Your parsing logic (similar to Python version)
    
    return cleanData;
}
```

Add to conversion logic:

```javascript
} else if (supplier === 'newsupplier') {
    cleanData = parseNewsSupplier(workbook);
}
```

#### 3. Test Your Parser

```bash
# Test Python version
python parsers/newsupplier_parser.py examples/input/sample.xlsx

# Test web app
# Open index.html, select supplier, upload file
```

#### 4. Update Documentation

- Add supplier to README.md supported list
- Add any special notes about the supplier's format
- Include example output format

#### 5. Submit Pull Request

1. Fork the repository
2. Create feature branch: `git checkout -b add-newsupplier-parser`
3. Commit changes: `git commit -am 'Add News Supplier parser'`
4. Push: `git push origin add-newsupplier-parser`
5. Open Pull Request with description of changes

### Code Style

#### Python
- Follow PEP 8
- Use descriptive variable names
- Add docstrings to functions
- Handle errors gracefully

#### JavaScript
- Use camelCase for variables
- Use const/let (not var)
- Add comments for complex logic
- Handle edge cases

### Testing Checklist

Before submitting:

- [ ] Parser handles empty rows
- [ ] Bottle sizes converted to ml correctly
- [ ] Large formats (1.5L, 3L, etc.) work
- [ ] Pricing extracted correctly
- [ ] Stock status determined accurately
- [ ] Output columns match standard format
- [ ] Works with multi-sheet files (if applicable)
- [ ] Web app and Python versions produce same output
- [ ] No console errors in browser
- [ ] README.md updated

## Questions?

Feel free to open an issue for any questions about contributing!
