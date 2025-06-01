# VC Investor Scraper

A powerful Python tool to scrape investor data from [VCSheet.com](https://vcsheet.com) and export to CSV format or upload directly to Odoo CRM via API.

## Features

- 🔍 **Smart Keyword Filtering**: Search for investors by keywords (e.g., "fintech", "AI", "marketing")
- 📊 **Complete Data Extraction**: Extracts names, companies, emails, social media links, investment focus, and stages
- 📁 **Multiple Export Options**: 
  - Standard CSV format
  - Odoo CRM-compatible CSV format
  - Direct Odoo API upload
- 🎯 **Odoo Integration**: Upload leads directly to your Odoo CRM with team and user assignments
- 🔄 **Full Pagination**: Scrapes all pages (35+ pages, 1000+ investors)
- 🛡️ **Robust Error Handling**: Handles network issues, parsing errors, and API failures gracefully
- ⚡ **Rate Limiting**: Built-in delays to respect website resources

## Installation

1. **Clone the repository**:
```bash
git clone https://github.com/yourusername/vc_investor_scraper.git
cd vc_investor_scraper
```

2. **Install dependencies**:
```bash
pip install -r requirements.txt
```

3. **Install the package** (optional):
```bash
pip install -e .
```

## Quick Start

### Basic CSV Export
```bash
# Export all investors
python -m vcsheet_scraper.scraper -o all_investors.csv

# Export investors with specific keywords
python -m vcsheet_scraper.scraper -k "fintech" "AI" -o fintech_ai_investors.csv

# Export in Odoo-compatible format
python -m vcsheet_scraper.scraper -k "marketing" -o marketing_investors.csv --odoo
```

### Direct Odoo Upload
```bash
# Upload to Odoo CRM
python -m vcsheet_scraper.scraper -k "AI research" --odoo-upload \
  --odoo-url "https://your-odoo.com" \
  --odoo-db "your_database" \
  --odoo-user "your_username" \
  --odoo-password "your_password" \
  --odoo-team "Your Sales Team" \
  --odoo-user-assign "Your Name"
```

## Usage Examples

### 1. Marketing Investors
```bash
python -m vcsheet_scraper.scraper -k "marketing" -o marketing_investors.csv --odoo
```

### 2. AI & Machine Learning Investors
```bash
python -m vcsheet_scraper.scraper -k "AI" "machine learning" -o ai_ml_investors.csv
```

### 3. Early Stage Investors
```bash
python -m vcsheet_scraper.scraper -k "seed" "pre-seed" -o early_stage_investors.csv
```

### 4. Upload to Odoo with Team Assignment
```bash
python -m vcsheet_scraper.scraper -k "fintech" --odoo-upload \
  --odoo-url "https://your-company.odoo.com" \
  --odoo-db "production" \
  --odoo-user "admin" \
  --odoo-password "your_api_key" \
  --odoo-model "crm.lead" \
  --odoo-stage "New" \
  --odoo-team "Investment Team" \
  --odoo-user-assign "john.doe@company.com"
```

## Command Line Options

### Basic Options
- `-k, --keywords`: Keywords to filter investors (e.g., 'fintech', 'AI', 'seed')
- `-o, --output`: Output CSV filename (optional when using --odoo-upload)
- `--odoo`: Generate Odoo CRM leads compatible CSV format
- `--log-level`: Set logging level (DEBUG, INFO, WARNING, ERROR)

### Odoo API Options
- `--odoo-upload`: Upload data directly to Odoo via API
- `--odoo-url`: Odoo server URL (e.g., 'https://your-odoo.com')
- `--odoo-db`: Odoo database name
- `--odoo-user`: Odoo username
- `--odoo-password`: Odoo password or API key
- `--odoo-model`: Odoo model ('crm.lead' or 'res.partner', default: crm.lead)
- `--odoo-stage`: Default pipeline stage for leads
- `--odoo-team`: Default sales team to assign leads to
- `--odoo-user-assign`: Default user to assign leads to

## Output Formats

### Standard CSV Format
```csv
name,company,website,description,focus,location,stage,email,linkedin,twitter,crunchbase,youtube,check_size
John Doe,Acme Ventures,https://acme.vc,Bio and description,AI,San Francisco,Seed,john@acme.vc,linkedin.com/in/johndoe,twitter.com/johndoe,crunchbase.com/person/john-doe,,
```

### Odoo-Compatible CSV Format
```csv
External ID,Name,Company Name,Contact Name,Email,Job Position,Phone,Mobile,Street,Street2,City,State,Zip,Country,Website,Notes
1,John Doe,Acme Ventures,John Doe,john@acme.vc,Investor,,,,,,,,,https://acme.vc,"Company: Acme Ventures; Focus Areas: AI; Bio: ...; LinkedIn: ...; Source: VCSheet.com"
```

## Odoo Integration

### Setting Up Odoo API Access

1. **Get API Key** (recommended):
   - Log into Odoo → Settings → Users & Companies → Users
   - Click your user → Preferences tab → API Keys section
   - Create new API key

2. **Or use regular password** (less secure)

### Odoo Configuration Requirements

- **CRM module** must be installed
- **User permissions**: Create/write access to CRM leads
- **Sales teams**: Must exist if using --odoo-team
- **Users**: Must exist if using --odoo-user-assign

### What Gets Created in Odoo

**For CRM Leads (crm.lead)**:
- Lead name: Investor's name (without "Investor:" prefix)
- Contact name, company, email, website
- Comprehensive description with bio, focus areas, investment stages
- All social media links in description
- UTM source tracking ("VCSheet.com")
- Optional stage, team, and user assignment

## Data Extracted

For each investor, the scraper extracts:

- **Basic Info**: Name, company/fund, email, website
- **Professional**: Investment focus areas, stages, bio/description
- **Social Media**: LinkedIn, Twitter, Crunchbase, YouTube profiles
- **Metadata**: Source tracking, external IDs

## Error Handling

The scraper includes robust error handling for:
- Network connectivity issues
- Website structure changes
- Odoo API authentication failures
- Invalid search parameters
- Rate limiting and timeouts

## Rate Limiting

- Built-in delays between page requests (1-2 seconds)
- Respectful scraping practices
- Configurable timeouts and retries

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Disclaimer

This tool is for educational and business purposes. Please respect VCSheet.com's terms of service and use responsibly. The authors are not responsible for any misuse of this tool.

## Support

For issues, questions, or contributions, please open an issue on GitHub.

---

**Made with ❤️ for the startup ecosystem**
