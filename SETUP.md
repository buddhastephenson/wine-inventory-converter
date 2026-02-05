# Setup Instructions

## For GitHub

### 1. Initialize Git Repository

```bash
cd wine-inventory-converter
git init
git add .
git commit -m "Initial commit: Wine Inventory Converter v1.0"
```

### 2. Create GitHub Repository

1. Go to https://github.com/new
2. Name: `wine-inventory-converter`
3. Description: "Convert wine supplier price lists to standardized Excel format"
4. Public or Private (your choice)
5. Don't initialize with README (we have one)

### 3. Push to GitHub

```bash
git remote add origin https://github.com/YOUR_USERNAME/wine-inventory-converter.git
git branch -M main
git push -u origin main
```

## For Google Cloud (Antigravity)

### Option 1: Host as Static Website

```bash
# Upload to Google Cloud Storage bucket
gsutil mb gs://wine-inventory-converter
gsutil cp -r * gs://wine-inventory-converter/
gsutil web set -m index.html gs://wine-inventory-converter
gsutil iam ch allUsers:objectViewer gs://wine-inventory-converter
```

### Option 2: Deploy on Cloud Run

Create `Dockerfile`:

```dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 8080
CMD python -m http.server 8080
```

Deploy:

```bash
gcloud run deploy wine-converter \
  --source . \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated
```

### Option 3: Firebase Hosting

```bash
# Install Firebase CLI
npm install -g firebase-tools

# Initialize Firebase
firebase init hosting

# Deploy
firebase deploy
```

## Quick Start for Users

### Web App (No Installation)

1. Open `index.html` in any browser
2. Works offline!
3. All processing happens in browser

### Python Scripts

```bash
# Install dependencies
pip install -r requirements.txt

# Run individual parsers
python parsers/dallaterra_parser.py input.xlsx
```

## Development

### Adding a New Parser

1. Create `parsers/newparser.py`:

```python
import pandas as pd
from openpyxl import Workbook

def parse_supplier(file_path):
    # Your parsing logic here
    pass

if __name__ == "__main__":
    import sys
    parse_supplier(sys.argv[1])
```

2. Add to `index.html` dropdown
3. Add JavaScript parser function
4. Test with sample files
5. Update README.md

### Testing

```bash
# Test a parser
python parsers/dallaterra_parser.py examples/input/sample.xlsx

# Compare output
diff examples/output/expected.xlsx output.xlsx
```

## Troubleshooting

### "Module not found" errors
```bash
pip install -r requirements.txt --break-system-packages
```

### Large files timing out
- Use Python scripts instead of web app for files >10MB
- Split large files into smaller chunks

### Excel formatting issues
- Ensure openpyxl version is >=3.1.0
- Check that file is .xlsx format (not .xls)

## Support

- GitHub Issues: Report bugs or request features
- Pull Requests: Contributions welcome!
- Documentation: See README.md for full details
