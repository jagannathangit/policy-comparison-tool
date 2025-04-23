# policy-comparison-tool

A web policy comparison tool that automatically scrapes and compares medical policy content from multiple websites. This tool uses Selenium and BeautifulSoup to extract text content from source and destination URLs, performs similarity analysis, and generates detailed Excel reports highlighting differences.

## 🌟 Features

- **Automated Web Scraping**: Uses Selenium and BeautifulSoup to extract policy content from different website structures
- **Intelligent Content Extraction**: Targeted scraping of specific content areas on both source and destination websites
- **Detailed Comparison**: Line-by-line comparison with visual highlighting of differences
- **Similarity Analysis**: Calculates similarity scores based on shared content
- **Excel Reporting**: Generates comprehensive Excel reports with color-coding for easy identification of changes
- **Scheduled Automation**: GitHub Actions workflow for regular automated comparisons
- **Configurable**: Supports various input formats (XLSX, CSV, JSON) and customizable parameters

## 📋 Requirements

- Python 3.8+
- Chrome browser (for Selenium WebDriver)
- Python packages:
  - beautifulsoup4
  - openpyxl
  - selenium
  - webdriver-manager

## 🚀 Getting Started

### Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/yourusername/policy-comparison-tool.git
   cd policy-comparison-tool
   ```

2. Install required packages:

   ```bash
   pip install -r scripts/requirements.txt
   ```

3. Ensure Chrome browser is installed on your system

### Usage

#### Generate Test Data

Generate test data with policy URLs for comparison:

```bash
python scripts/generate_xlsx.py --output data/policy_comparison_data.xlsx --count 100
```

Parameters:

- `--output`: Output file path (default: policy_comparison_data.xlsx)
- `--count`: Number of policy entries to generate (default: 100)

#### Run Comparison

Compare policies from the generated data:

```bash
python scripts/compare_websites_multi.py --config data/policy_comparison_data.xlsx --output results/policy_comparisons.xlsx --headless --max 10
```

Parameters:

- `--config`: Input configuration file with URL pairs (XLSX, CSV, or JSON)
- `--output`: Output Excel file with comparison results
- `--headless`: Run Chrome in headless mode (no UI)
- `--max`: Maximum number of URL pairs to process (0 = all)

## 📊 Output

The script generates an Excel file with the following:

1. **Policy Information**: Policy numbers and URLs for both source and destination
2. **Content Comparison**:
   - White background: Content matches in both sources
   - Light red background: Content only in source
   - Light green background: Content only in destination
3. **Similarity Score**: Numerical representation of content similarity

## 📂 Repository Structure

```
policy-comparison-tool/
├── .github/
│   └── workflows/
│       └── compare_policies.yml    # GitHub Actions workflow
├── scripts/
│   ├── compare_urls.py   # Main comparison script
│   ├── test_data_generator.py            # Data generation script
│   └── requirements.txt            # Python dependencies
├── data/
│   └── policy_comparison_data.xlsx             # Sample policy data
├── results/
│   └── policy_comparisons.xlsx     # Generated comparison results
└── README.md                       # This file
```

## 🔍 How It Works

1. **Data Generation**: Generate XLSX files with paired URLs for source and destination policies
2. **Web Scraping**:
   - Source URL: Extracts content from `journal-content-article` div
   - Destination URL: Extracts content from `main` tag and `contentWrapper` divs
3. **Content Processing**: Cleans and normalizes text content
4. **Comparison**: Uses Python's `difflib` to identify matching and unique content
5. **Reporting**: Generates color-coded Excel report with detailed differences

## 🛠️ Customization

### Adding New URL Patterns

The tool extracts policy numbers from URLs using regex patterns. To add support for new URL formats, modify the `extract_policy_number` function in `compare_urls.py`.

### Custom CSS Selectors

To target different HTML elements:

1. Modify `get_text_from_source_url` for source website structure
2. Modify `get_text_from_destination_url` for destination website structure

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 📧 Contact

Project Link: [https://github.com/jagannathangit/policy-comparison-tool/](https://github.com/jagannathangit/policy-comparison-tool/)
