# 🛠️ MCP Tools Documentation

Complete reference for all Model Context Protocol (MCP) tools available in the Theta Gateway system.

## 📋 Table of Contents

- [Overview](#overview)
- [Quick Reference](#quick-reference)
- [Excel Tools](#excel-tools)
- [Public Financial Market Tools](#public-financial-market-tools)
- [Private Market Tools](#private-market-tools)
- [Real Estate Tools](#real-estate-tools)
- [Accounting Tools](#accounting-tools)
- [Document Processing Tools](#document-processing-tools)
- [Tool Usage Guidelines](#tool-usage-guidelines)
- [Integration Examples](#integration-examples)

## Overview

The Theta Gateway provides access to 65+ professional tools across six main categories:

| Category | Tools | Description |
|----------|-------|-------------|
| **Excel** | 20+ tools | Create, manipulate, and analyze Excel workbooks |
| **Public Financial Market** | 17 tools | Real-time financial data from public markets and companies |
| **Private Market** | 2 tools | Private company data and funding information via Crunchbase |
| **Real Estate** | 19 tools | Property data, valuations, market analysis, and construction costs |
| **Accounting** | 9 tools | Double-entry accounting system via Ledger CLI for financial reporting and analysis |
| **Document Processing** | 3 tools | Read and analyze various document formats (PDF, TXT, DOCX, CSV, JSON) |

### 🎯 **Key Features:**
- **Clean Tool Names**: All tools use intuitive names without client prefixes (e.g., `getPropertyRecords`, not `rentcast_getPropertyRecords`)
- **Real-Time Data**: Live market data, property valuations, and construction costs
- **Professional Excel Integration**: Complete workbook creation and analysis capabilities
- **Comprehensive Real Estate Intelligence**: Property search, market analysis, and investment insights
- **Construction Cost Analysis**: Material, labor, and equipment pricing for development projects
- **Double-Entry Accounting**: Powerful Ledger CLI integration for financial reporting and budget analysis

---

## 🚀 Quick Reference

### Most Popular Tools

#### 🏠 **Real Estate Analysis**
```python
# Property search and analysis
properties = call_tool("getPropertyRecords", {"city": "Austin", "state": "TX"})
value = call_tool("getValueEstimate", {"address": "123 Main St, Austin, TX"})
rent = call_tool("getRentEstimate", {"address": "123 Main St, Austin, TX"})
market = call_tool("getMarketStatistics", {"zipCode": "78701"})

# Investment analysis
investments = call_tool("findInvestmentProperties", {"city": "Austin", "state": "TX", "maxPrice": 400000})
comparison = call_tool("compareMarkets", {"zipCodes": ["78701", "78702", "78703"]})

# Construction costs for development projects
materials = call_tool("searchSources", {"search_term": "concrete", "state": "Texas", "county": "Travis"})
labor = call_tool("getLaborRates", {"trade": "electrician", "state": "Texas", "county": "Travis"})
equipment = call_tool("getEquipmentRentalRates", {"equipment_type": "excavator", "state": "Texas", "county": "Travis"})
```

#### 📈 **Public Financial Market Data**
```python
# Stock market data
price = call_tool("getPriceSnapshot", {"ticker": "AAPL"})
historical = call_tool("getHistoricalPrices", {"ticker": "TSLA", "period": "1y"})
financials = call_tool("getFinancials", {"ticker": "MSFT", "period": "quarterly"})

# Market analysis
indices = call_tool("getMarketIndices", {})
sector = call_tool("getSectorPerformance", {"sector": "Technology"})
companies = call_tool("searchCompanies", {"query": "artificial intelligence"})
```

#### 🏢 **Private Market Intelligence**
```python
# Company research
company_info = call_tool("getCrunchbaseCompanyInfo", {"company": "openai"})
company_by_domain = call_tool("getCrunchbaseCompanyInfo", {"domain": "darwingov.com"})

# Funding analysis
funding_rounds = call_tool("getCrunchbaseFundingRounds", {"investment_type": "series_a", "days_since_announcement": 30})
```

#### 📊 **Excel Automation & Document Processing**
```python
# Excel automation
call_tool("excel_create_workbook", {"file_name": "Analysis.xlsx"})
call_tool("excel_write_data_to_excel", {"file_name": "Analysis.xlsx", "sheet_name": "Data", "data": [[...]]})
call_tool("excel_create_chart", {"file_name": "Analysis.xlsx", "sheet_name": "Data", "chart_type": "scatter", "data_range": "A1:C10"})

# Document processing
content = call_tool("readDocument", {"file_path": "/path/to/document.pdf"})
structure = call_tool("analyzeDocumentStructure", {"file_path": "/path/to/report.docx"})
documents = call_tool("listWorkspaceDocuments", {"workspace_path": "/workspace"})
```

#### 📈 **Accounting & Financial Analysis**
```python
# Account balances and reporting
balances = call_tool("ledger_balance", {"query": "Assets", "date_range": "2024"})
register = call_tool("ledger_register", {"query": "Expenses:Food", "date_range": "last month"})

# Account and transaction analysis
accounts = call_tool("ledger_accounts", {"query": "Income"})
payees = call_tool("ledger_payees", {"query": "Amazon"})
stats = call_tool("ledger_stats", {"query": "2024"})

# Budget analysis and reporting
budget = call_tool("ledger_budget", {"query": "Expenses", "period": "monthly"})
transactions = call_tool("ledger_print", {"query": "tag:business", "date_range": "Q1 2024"})
```

### 🎯 **Clean Tool Names**
All tools use intuitive names without client prefixes:
- ✅ `getPropertyRecords` (not `rentcast_getPropertyRecords`)  
- ✅ `searchSources` (not `onebuild_searchSources`)
- ✅ `getValueEstimate` (not `rentcast_getValueEstimate`)
- ✅ `ledger_balance` (Accounting tools use descriptive ledger_ prefix)
- ✅ `excel_create_workbook` (Excel tools keep excel_ prefix for clarity)

---

## 📊 Excel Tools

Professional Excel manipulation and automation tools for creating reports, charts, and data analysis.

### Workbook Operations (5 tools)

#### `excel_create_workbook`
Create new Excel workbooks with optional multiple sheets.

**Parameters:**
```json
{
  "file_name": "string (required) - Name of the Excel file to create",
  "sheets": "array[string] (optional) - List of sheet names, defaults to ['Sheet1']"
}
```

**Output:**
```json
{
  "status": "success",
  "file_path": "/path/to/created/file.xlsx",
  "sheets_created": ["Sheet1", "Sheet2"],
  "message": "Workbook created successfully"
}
```

#### `excel_get_workbook_info`
Get metadata about an existing workbook including sheet names and properties.

**Parameters:**
```json
{
  "file_name": "string (required) - Path to Excel file"
}
```

**Output:**
```json
{
  "file_name": "report.xlsx",
  "sheet_names": ["Summary", "Data", "Charts"],
  "named_ranges": ["SalesData", "Totals"],
  "file_size": 1024000,
  "last_modified": "2024-01-15T10:30:00Z"
}
```

#### `excel_create_worksheet`
Add new worksheets to existing workbooks.

**Parameters:**
```json
{
  "file_name": "string (required) - Path to Excel file",
  "sheet_name": "string (required) - Name of new worksheet"
}
```

#### `excel_copy_worksheet`
Duplicate existing worksheets within the same workbook.

**Parameters:**
```json
{
  "file_name": "string (required) - Path to Excel file",
  "source_sheet": "string (required) - Name of sheet to copy",
  "target_sheet": "string (required) - Name of new copied sheet"
}
```

#### `excel_delete_worksheet`
Remove worksheets from workbooks.

**Parameters:**
```json
{
  "file_name": "string (required) - Path to Excel file",
  "sheet_name": "string (required) - Name of sheet to delete"
}
```

### Data Operations (4 tools)

#### `excel_read_data_from_excel`
Read cell values and ranges from Excel sheets with validation metadata.

**Parameters:**
```json
{
  "file_name": "string (required) - Path to Excel file",
  "sheet_name": "string (required) - Name of worksheet",
  "start_cell": "string (default: 'A1') - Starting cell reference",
  "end_cell": "string (optional) - Ending cell reference for range"
}
```

**Output:**
```json
{
  "data": [
    ["Name", "Age", "Salary"],
    ["John Doe", 30, 50000],
    ["Jane Smith", 25, 45000]
  ],
  "range": "A1:C3",
  "cell_count": 9,
  "has_headers": true
}
```

#### `excel_write_data_to_excel`
Write data arrays to Excel sheets starting from specified cell.

**Parameters:**
```json
{
  "file_name": "string (required) - Path to Excel file",
  "sheet_name": "string (required) - Name of worksheet",
  "data": "array[array] (required) - 2D array of data to write",
  "start_cell": "string (default: 'A1') - Starting cell reference"
}
```

**Output:**
```json
{
  "status": "success",
  "rows_written": 100,
  "columns_written": 5,
  "range_affected": "A1:E100"
}
```

#### `excel_apply_formula`
Add Excel formulas to specific cells with validation.

**Parameters:**
```json
{
  "file_name": "string (required) - Path to Excel file",
  "sheet_name": "string (required) - Name of worksheet",
  "cell": "string (required) - Cell reference (e.g., 'A1')",
  "formula": "string (required) - Excel formula (e.g., '=SUM(A1:A10)')"
}
```

#### `excel_validate_formula_syntax`
Check formula validity before applying to cells.

**Parameters:**
```json
{
  "formula": "string (required) - Excel formula to validate"
}
```

**Output:**
```json
{
  "is_valid": true,
  "formula": "=SUM(A1:A10)",
  "parsed_references": ["A1:A10"],
  "function_used": ["SUM"]
}
```

### Formatting & Styling (6 tools)

#### `excel_format_range`
Apply comprehensive formatting to cell ranges including fonts, colors, borders, and number formats.

**Parameters:**
```json
{
  "file_name": "string (required) - Path to Excel file",
  "sheet_name": "string (required) - Name of worksheet",
  "range": "string (required) - Cell range (e.g., 'A1:C10')",
  "formatting": {
    "font": {
      "name": "string (optional) - Font name",
      "size": "number (optional) - Font size",
      "bold": "boolean (optional) - Bold text",
      "italic": "boolean (optional) - Italic text",
      "color": "string (optional) - Font color (hex)"
    },
    "fill": {
      "color": "string (optional) - Background color (hex)"
    },
    "border": {
      "style": "string (optional) - Border style",
      "color": "string (optional) - Border color (hex)"
    },
    "alignment": {
      "horizontal": "string (optional) - left/center/right",
      "vertical": "string (optional) - top/center/bottom"
    },
    "number_format": "string (optional) - Number format code"
  }
}
```

#### `excel_merge_cells` / `excel_unmerge_cells`
Merge or unmerge cell ranges for headers and layout.

**Parameters:**
```json
{
  "file_name": "string (required) - Path to Excel file",
  "sheet_name": "string (required) - Name of worksheet",
  "range": "string (required) - Cell range to merge/unmerge"
}
```

#### `excel_get_merged_cells`
List all merged cell ranges in a worksheet.

**Output:**
```json
{
  "merged_ranges": ["A1:C1", "A5:B7"],
  "count": 2
}
```

#### `excel_copy_range`
Copy cell ranges with formatting and formulas preserved.

**Parameters:**
```json
{
  "file_name": "string (required) - Path to Excel file",
  "sheet_name": "string (required) - Name of worksheet",
  "source_range": "string (required) - Source range to copy",
  "destination_cell": "string (required) - Destination cell reference"
}
```

#### `excel_delete_range`
Delete cell ranges and shift remaining cells.

**Parameters:**
```json
{
  "file_name": "string (required) - Path to Excel file",
  "sheet_name": "string (required) - Name of worksheet",
  "range": "string (required) - Range to delete",
  "shift": "string (optional) - 'up' or 'left' for shift direction"
}
```

### Advanced Features (5 tools)

#### `excel_create_chart`
Generate professional charts with extensive customization options.

**Parameters:**
```json
{
  "file_name": "string (required) - Path to Excel file",
  "sheet_name": "string (required) - Name of worksheet",
  "chart_type": "string (required) - Chart type: line/bar/pie/scatter/area",
  "data_range": "string (required) - Data range for chart",
  "title": "string (optional) - Chart title",
  "chart_position": "string (optional) - Position cell reference"
}
```

**Output:**
```json
{
  "status": "success",
  "chart_id": "chart_001",
  "chart_type": "line",
  "position": "E2:M20",
  "data_series": 3
}
```

#### `excel_create_pivot_table`
Create pivot tables for data analysis and aggregation.

**Parameters:**
```json
{
  "file_name": "string (required) - Path to Excel file",
  "sheet_name": "string (required) - Name of worksheet",
  "data_range": "string (required) - Source data range",
  "pivot_config": {
    "rows": "array[string] - Row fields",
    "columns": "array[string] - Column fields", 
    "values": "array[object] - Value fields with aggregation",
    "filters": "array[string] - Filter fields"
  }
}
```

#### `excel_create_table`
Create native Excel tables with filtering and sorting capabilities.

**Parameters:**
```json
{
  "file_name": "string (required) - Path to Excel file",
  "sheet_name": "string (required) - Name of worksheet",
  "data_range": "string (required) - Data range for table",
  "table_name": "string (optional) - Name for the table",
  "has_headers": "boolean (default: true) - Whether first row contains headers"
}
```

#### `excel_validate_excel_range`
Verify that cell range references are valid.

**Parameters:**
```json
{
  "range": "string (required) - Range to validate (e.g., 'A1:C10')"
}
```

#### `excel_get_data_validation_info`
Extract data validation rules from cells.

**Parameters:**
```json
{
  "file_name": "string (required) - Path to Excel file",
  "sheet_name": "string (required) - Name of worksheet",
  "cell": "string (required) - Cell reference"
}
```

---

## 📈 Public Financial Market Tools

Real-time financial data and analysis tools for public markets powered by Financial Datasets API.

### Market Data Tools

#### `getPriceSnapshot`
Get current stock prices with comprehensive market data.

**Parameters:**
```json
{
  "ticker": "string (required) - Stock ticker symbol (e.g., 'AAPL', 'TSLA')"
}
```

**Output:**
```json
{
  "ticker": "AAPL",
  "price": 150.25,
  "change": 2.50,
  "change_percent": 1.69,
  "volume": 45000000,
  "market_cap": 2400000000000,
  "52_week_high": 180.00,
  "52_week_low": 120.00,
  "pe_ratio": 25.5,
  "dividend_yield": 0.52,
  "timestamp": "2024-01-15T16:00:00Z"
}
```

#### `getHistoricalPrices`
Retrieve historical price data with flexible time periods.

**Parameters:**
```json
{
  "ticker": "string (required) - Stock ticker symbol",
  "period": "string (default: '1y') - Time period: 1d/5d/1mo/3mo/6mo/1y/2y/5y/10y/ytd/max",
  "interval": "string (default: '1d') - Data interval: 1m/2m/5m/15m/30m/60m/90m/1h/1d/5d/1wk/1mo/3mo"
}
```

**Output:**
```json
{
  "ticker": "AAPL",
  "period": "1y",
  "interval": "1d",
  "data": [
    {
      "date": "2024-01-15",
      "open": 148.50,
      "high": 152.00,
      "low": 147.80,
      "close": 150.25,
      "volume": 45000000,
      "adj_close": 150.25
    }
  ],
  "data_points": 252
}
```

#### `getIntradayPrices`
Get intraday trading data for day trading analysis.

**Parameters:**
```json
{
  "ticker": "string (required) - Stock ticker symbol",
  "interval": "string (default: '5m') - Interval: 1m/2m/5m/15m/30m/60m/90m"
}
```

### Company Financial Data

#### `getFinancials`
Access comprehensive financial statements including income statements, balance sheets, and cash flow.

**Parameters:**
```json
{
  "ticker": "string (required) - Stock ticker symbol",
  "period": "string (default: 'quarterly') - 'quarterly' or 'annual'",
  "limit": "integer (default: 4) - Number of periods to return",
  "years": "integer (optional) - Alias for limit parameter"
}
```

**Output:**
```json
{
  "ticker": "AAPL",
  "period": "quarterly",
  "income_statements": [
    {
      "period_ending": "2023-12-31",
      "revenue": 119575000000,
      "gross_profit": 54738000000,
      "operating_income": 40323000000,
      "net_income": 33916000000,
      "earnings_per_share": 2.18
    }
  ],
  "balance_sheets": [
    {
      "period_ending": "2023-12-31",
      "total_assets": 352755000000,
      "total_liabilities": 274764000000,
      "shareholders_equity": 77991000000
    }
  ],
  "cash_flow_statements": [
    {
      "period_ending": "2023-12-31",
      "operating_cash_flow": 46327000000,
      "investing_cash_flow": -1445000000,
      "financing_cash_flow": -35563000000
    }
  ]
}
```

#### `getFinancialRatios`
Calculate and retrieve key financial ratios and metrics.

**Parameters:**
```json
{
  "ticker": "string (required) - Stock ticker symbol",
  "period": "string (default: 'quarterly') - 'quarterly' or 'annual'"
}
```

**Output:**
```json
{
  "ticker": "AAPL",
  "ratios": {
    "profitability": {
      "gross_margin": 0.458,
      "operating_margin": 0.337,
      "net_margin": 0.284,
      "return_on_assets": 0.096,
      "return_on_equity": 0.435
    },
    "liquidity": {
      "current_ratio": 1.02,
      "quick_ratio": 0.85,
      "cash_ratio": 0.52
    },
    "efficiency": {
      "asset_turnover": 1.12,
      "inventory_turnover": 35.8,
      "receivables_turnover": 15.2
    },
    "leverage": {
      "debt_to_equity": 2.53,
      "debt_ratio": 0.32,
      "interest_coverage": 23.4
    }
  }
}
```

#### `getSegmentedFinancials`
Get business segment financial data for diversified companies.

**Parameters:**
```json
{
  "ticker": "string (required) - Stock ticker symbol",
  "period": "string (default: 'quarterly') - 'quarterly' or 'annual'"
}
```

### Company Information

#### `getCompanyInfo`
Retrieve comprehensive company profiles and business descriptions.

**Parameters:**
```json
{
  "ticker": "string (required) - Stock ticker symbol"
}
```

**Output:**
```json
{
  "ticker": "AAPL",
  "company_name": "Apple Inc.",
  "sector": "Technology",
  "industry": "Consumer Electronics",
  "description": "Apple Inc. designs, manufactures, and markets smartphones, personal computers, tablets, wearables, and accessories worldwide.",
  "headquarters": "Cupertino, CA",
  "employees": 161000,
  "founded": "1976-04-01",
  "market_cap": 2400000000000,
  "enterprise_value": 2380000000000,
  "website": "https://www.apple.com"
}
```

#### `getCompanyNews`
Get latest company-specific news and announcements.

**Parameters:**
```json
{
  "ticker": "string (required) - Stock ticker symbol",
  "limit": "integer (default: 10) - Number of news articles"
}
```

**Output:**
```json
{
  "ticker": "AAPL",
  "news": [
    {
      "title": "Apple Reports Q4 Earnings Beat",
      "summary": "Apple Inc. reported quarterly earnings that exceeded analyst expectations...",
      "url": "https://finance.example.com/news/apple-earnings",
      "published_date": "2024-01-15T09:00:00Z",
      "source": "Financial News Network"
    }
  ],
  "total_articles": 25
}
```

#### `getEarnings`
Access earnings data, estimates, and historical performance.

**Parameters:**
```json
{
  "ticker": "string (required) - Stock ticker symbol",
  "period": "string (default: 'quarterly') - 'quarterly' or 'annual'"
}
```

### Market Analysis Tools

#### `getInsiderTrades`
Track insider trading activity for compliance and analysis.

**Parameters:**
```json
{
  "ticker": "string (required) - Stock ticker symbol",
  "limit": "integer (default: 50) - Number of transactions"
}
```

**Output:**
```json
{
  "ticker": "AAPL",
  "insider_trades": [
    {
      "insider_name": "John Doe",
      "title": "Chief Executive Officer",
      "transaction_date": "2024-01-10",
      "transaction_type": "Sale",
      "shares": 10000,
      "price_per_share": 150.00,
      "total_value": 1500000,
      "shares_owned_after": 500000
    }
  ]
}
```

#### `getInstitutionalOwnership`
Analyze institutional holdings and ownership patterns.

**Parameters:**
```json
{
  "ticker": "string (required) - Stock ticker symbol"
}
```

#### `getSECFilings`
Access regulatory filings including 10-K, 10-Q, and 8-K documents.

**Parameters:**
```json
{
  "ticker": "string (required) - Stock ticker symbol",
  "filing_type": "string (optional) - Specific filing type to filter",
  "limit": "integer (default: 10) - Number of filings"
}
```

### Search and Discovery

#### `searchCompanies`
Search for companies by name or business description.

**Parameters:**
```json
{
  "query": "string (required) - Search term",
  "limit": "integer (default: 10) - Number of results"
}
```

#### `getMarketIndices`
Get major market indices data and performance.

**Parameters:** None

**Output:**
```json
{
  "indices": [
    {
      "name": "S&P 500",
      "symbol": "^GSPC",
      "value": 4800.50,
      "change": 25.30,
      "change_percent": 0.53
    },
    {
      "name": "Dow Jones",
      "symbol": "^DJI", 
      "value": 37000.25,
      "change": 150.75,
      "change_percent": 0.41
    }
  ]
}
```

#### `getSectorPerformance`
Analyze sector performance and rotation trends.

**Parameters:**
```json
{
  "sector": "string (optional) - Specific sector to analyze"
}
```

### Economic Data

#### `getInterestRates`
Access various interest rate data including federal funds rate.

**Parameters:**
```json
{
  "rate_type": "string (default: 'federal_funds') - Type of interest rate"
}
```

#### `getEconomicIndicators`
Get economic indicators like GDP, inflation, unemployment.

**Parameters:**
```json
{
  "indicator": "string (required) - Economic indicator name"
}
```

---

## 🏢 Private Market Tools

Private company data and funding information via Crunchbase API.

### Company Research Tools

#### `getCrunchbaseCompanyInfo`
Get detailed company information from Crunchbase including name, description, funding, location, social networks, and more.

**Parameters:**
```json
{
  "company": "string (optional) - Company name or identifier (e.g., 'openai', 'google', 'microsoft'). Either company or domain must be provided.",
  "domain": "string (optional) - Company domain/website (e.g., 'openai.com', 'google.com', 'darwingov.com'). Either company or domain must be provided."
}
```

**Output:**
```json
{
  "success": true,
  "data": {
    "basic_info": {
      "name": "Darwin AI",
      "uuid": "2f703326-93b0-4dad-9a13-c4bc6799e3e5",
      "permalink": "darwin-ai-e3e5",
      "website": "https://darwingov.com",
      "founded": "2024-05-20",
      "headline": "GenAI Adoption and GRC platform for state and local government agencies.",
      "description": "...",
      "operating_status": "active",
      "company_type": "for profit",
      "employee_count": "1-10"
    },
    "location": [
      {
        "name": "Las Vegas",
        "type": "city"
      }
    ],
    "categories": [
      {
        "name": "Generative AI",
        "permalink": "generative-ai"
      }
    ],
    "funding_summary": {
      "funding_total": {
        "value": 5000000,
        "currency": "USD"
      },
      "num_funding_rounds": 1
    },
    "social_networks": [
      {
        "name": "linkedin",
        "url": "https://www.linkedin.com/company/darwin-gov-ai/"
      }
    ]
  }
}
```

#### `getCrunchbaseFundingRounds`
Get funding round information from Crunchbase with filtering options.

**Parameters:**
```json
{
  "days_since_announcement": "integer (optional) - Number of days since funding announcement (1-360 days), default: 30",
  "investment_type": "string (optional) - Type of investment. Options: pre_seed, seed, series_a, series_b, series_c, etc.",
  "investor_identifiers": "string (optional) - UUID of specific investor to filter by"
}
```

**Output:**
```json
{
  "success": true,
  "data": {
    "total_results": 1,
    "funding_rounds": [
      {
        "uuid": "565ec15e-4779-4dfd-878d-5ac112c62c85",
        "round_name": "Seed Round - Darwin AI",
        "company": {
          "name": "Darwin AI",
          "uuid": "2f703326-93b0-4dad-9a13-c4bc6799e3e5"
        },
        "announced_date": "2025-03-12",
        "investment_type": "seed",
        "money_raised": {
          "value": 5000000,
          "currency": "USD"
        },
        "investors": [
          {
            "name": "Resolute Ventures",
            "uuid": "d0a6043b-7164-af60-1063-e3314c6d9d95",
            "role": "investor"
          },
          {
            "name": "UpWest",
            "uuid": "a7d96886-7467-ce1a-db6c-06b293e26ed1",
            "role": "investor"
          }
        ]
      }
    ]
  }
}
```

---

## 🏠 Real Estate Tools

Real estate data, property valuations, market analysis tools with access to 140+ million property records, plus construction cost data.

### Property Data Tools

> **Note**: All tools use clean names without client prefixes (e.g., `getPropertyRecords`, not `rentcast_getPropertyRecords`)

#### `getPropertyRecords`
Search for property records by location and attributes.

**Parameters:**
```json
{
  "address": "string (optional) - Property address",
  "city": "string (optional) - City name",
  "state": "string (optional) - State name",
  "zipCode": "string (optional) - ZIP code",
  "propertyType": "string (optional) - Property type",
  "bedrooms": "integer (optional) - Number of bedrooms",
  "bathrooms": "number (optional) - Number of bathrooms",
  "squareFootage": "integer (optional) - Square footage",
  "lotSize": "integer (optional) - Lot size in square feet",
  "yearBuilt": "integer (optional) - Year the property was built",
  "limit": "integer (default: 20) - Result limit",
  "offset": "integer (default: 0) - Result offset for pagination"
}
```

**Output:**
```json
{
  "sources": [
    {
      "id": "src_12345",
      "name": "Concrete Ready Mix 3000 PSI",
      "source_type": "MATERIAL",
      "description": "Standard concrete mix for foundation work",
      "total_cost_usd": 125.50,
      "labor_cost_usd": 35.00,
      "material_cost_usd": 90.50,
      "unit": "cubic yard"
    }
  ],
  "total_count": 25,
  "search_term": "concrete",
  "location": "Los Angeles County, California"
}
```

#### `getCategoryTree`
Get the construction category hierarchy for organized browsing.

**Parameters:**
```json
{
  "category_path": "array[string] (optional) - Category path filter"
}
```

**Output:**
```json
{
  "categories": [
    "Concrete",
    "Steel", 
    "Lumber",
    "Electrical",
    "Plumbing"
  ],
  "category_count": 5
}
```

#### `getSourcesBatch`
Get pricing for multiple construction sources at once.

**Parameters:**
```json
{
  "source_ids": "array[string] (required) - List of source IDs",
  "state": "string (required) - State name",
  "county": "string (required) - County name",
  "zipcode": "string (optional) - ZIP code"
}
```

**Output:**
```json
{
  "sources": [
    {
      "id": "src_12345",
      "name": "Concrete Ready Mix",
      "source_type": "MATERIAL",
      "total_cost_usd": 125.50,
      "labor_cost_usd": 35.00,
      "material_cost_usd": 90.50
    }
  ],
  "location": "Los Angeles County, California",
  "source_count": 1
}
```

### Specialized Lookup Tools

#### `quickCostLookup`
Quick lookup for common construction materials with simplified parameters.

**Parameters:**
```json
{
  "material_name": "string (required) - Name of construction material (e.g., 'concrete', 'lumber', 'steel')",
  "state": "string (required) - State name (e.g., 'California')",
  "county": "string (required) - County name (e.g., 'Los Angeles County')",
  "limit": "integer (default: 3) - Number of results to return"
}
```

**Output:**
```json
{
  "sources": [
    {
      "id": "src_12345",
      "name": "Ready Mix Concrete 3000 PSI",
      "source_type": "MATERIAL",
      "total_cost_usd": 125.50,
      "material_cost_usd": 90.50,
      "labor_cost_usd": 35.00
    }
  ],
  "total_count": 3,
  "search_term": "concrete",
  "location": "Los Angeles County, California"
}
```

#### `getLaborRates`
Get labor rates for specific construction trades.

**Parameters:**
```json
{
  "trade": "string (required) - Construction trade (e.g., 'carpenter', 'electrician', 'plumber', 'contractor')",
  "state": "string (required) - State name (e.g., 'California')",
  "county": "string (required) - County name (e.g., 'Los Angeles County')"
}
```

**Output:**
```json
{
  "sources": [
    {
      "id": "src_67890",
      "name": "Licensed Electrician - Commercial",
      "source_type": "LABOR",
      "total_cost_usd": 85.00,
      "labor_cost_usd": 85.00,
      "description": "Per hour rate for commercial electrical work"
    }
  ],
  "total_count": 5,
  "search_term": "electrician",
  "location": "Los Angeles County, California"
}
```

#### `getEquipmentRentalRates`
Get equipment rental rates for construction equipment.

**Parameters:**
```json
{
  "equipment_type": "string (required) - Type of equipment (e.g., 'excavator', 'crane', 'bulldozer', 'forklift')",
  "state": "string (required) - State name (e.g., 'California')",
  "county": "string (required) - County name (e.g., 'Los Angeles County')"
}
```

**Output:**
```json
{
  "sources": [
    {
      "id": "src_11111",
      "name": "Excavator 320 Size - Daily Rental",
      "source_type": "EQUIPMENT",
      "total_cost_usd": 450.00,
      "material_cost_usd": 450.00,
      "description": "Mid-size excavator daily rental rate"
    }
  ],
  "total_count": 5,
  "search_term": "excavator",
  "location": "Los Angeles County, California"
}
```

### Construction Cost Tools

Professional construction cost data and material pricing tools.

> **Note**: All OneBuild tools use clean names without prefixes (e.g., `searchSources`, not `onebuild_searchSources`)

#### `searchSources`
Search for construction cost data by location and material type.

### Property Data Tools

#### `getPropertyRecords`
Search for property records by location and attributes.

**Parameters:**
```json
{
  "address": "string (optional) - Property address",
  "city": "string (optional) - City name",
  "state": "string (optional) - State name",
  "zipCode": "string (optional) - ZIP code",
  "propertyType": "string (optional) - Property type",
  "bedrooms": "integer (optional) - Number of bedrooms",
  "bathrooms": "number (optional) - Number of bathrooms",
  "squareFootage": "integer (optional) - Square footage",
  "lotSize": "integer (optional) - Lot size in square feet",
  "yearBuilt": "integer (optional) - Year the property was built",
  "limit": "integer (default: 20) - Result limit",
  "offset": "integer (default: 0) - Result offset for pagination"
}
```

**Output:**
```json
{
  "properties": [
    {
      "id": "prop_12345",
      "address": "123 Main St, Austin, TX 78701",
      "propertyType": "Single Family",
      "bedrooms": 3,
      "bathrooms": 2,
      "squareFootage": 1500,
      "lotSize": 7200,
      "yearBuilt": 1995,
      "lastSaleDate": "2022-03-15",
      "lastSalePrice": 450000,
      "estimatedValue": 485000,
      "taxAssessment": 425000
    }
  ],
  "total_count": 150,
  "page_info": {
    "limit": 20,
    "offset": 0,
    "has_more": true
  }
}
```

#### `getPropertyById`
Get detailed property information by property ID.

**Parameters:**
```json
{
  "propertyId": "string (required) - Unique property identifier"
}
```

**Output:**
```json
{
  "id": "prop_12345",
  "address": "123 Main St, Austin, TX 78701",
  "propertyType": "Single Family",
  "bedrooms": 3,
  "bathrooms": 2,
  "squareFootage": 1500,
  "lotSize": 7200,
  "yearBuilt": 1995,
  "detailed_info": {
    "construction_type": "Frame",
    "roof_material": "Asphalt Shingle",
    "heating_type": "Central",
    "cooling_type": "Central Air"
  }
}
```

#### `getRandomProperties`
Get random property records for sampling and discovery.

**Parameters:**
```json
{
  "limit": "integer (default: 20) - Number of random properties to return"
}
```

### Property Valuation Tools

#### `getValueEstimate`
Get property value estimates with comparable sales analysis.

**Parameters:**
```json
{
  "address": "string (optional) - Property address",
  "latitude": "number (optional) - Property latitude",
  "longitude": "number (optional) - Property longitude",
  "propertyType": "string (optional) - Property type",
  "bedrooms": "integer (optional) - Number of bedrooms",
  "bathrooms": "number (optional) - Number of bathrooms",
  "squareFootage": "integer (optional) - Square footage",
  "maxRadius": "number (optional) - Maximum search radius for comparables in miles",
  "daysOld": "integer (optional) - Maximum age of comparable sales in days",
  "compCount": "integer (optional) - Number of comparable sales to include"
}
```

**Output:**
```json
{
  "address": "123 Main St, Austin, TX",
  "estimate": {
    "value": 485000,
    "low": 460000,
    "high": 510000,
    "confidence": 0.85,
    "date": "2024-01-15"
  },
  "comparables": [
    {
      "address": "125 Main St",
      "sold_date": "2023-12-01",
      "sold_price": 475000,
      "bedrooms": 3,
      "bathrooms": 2,
      "square_footage": 1480,
      "distance_miles": 0.1
    }
  ],
  "price_per_sqft": 323,
  "methodology": "Automated Valuation Model"
}
```

#### `getRentEstimate`
Get property rent estimates with rental comparables.

**Parameters:**
```json
{
  "address": "string (optional) - Property address",
  "latitude": "number (optional) - Property latitude",
  "longitude": "number (optional) - Property longitude",
  "propertyType": "string (optional) - Property type",
  "bedrooms": "integer (optional) - Number of bedrooms",
  "bathrooms": "number (optional) - Number of bathrooms",
  "squareFootage": "integer (optional) - Square footage",
  "maxRadius": "number (optional) - Maximum search radius for comparables in miles",
  "daysOld": "integer (optional) - Maximum age of comparable rentals in days",
  "compCount": "integer (optional) - Number of comparable rentals to include"
}
```

**Output:**
```json
{
  "address": "123 Main St, Austin, TX",
  "rent_estimate": {
    "rent": 2400,
    "low": 2200,
    "high": 2600,
    "confidence": 0.82,
    "date": "2024-01-15"
  },
  "comparable_rentals": [
    {
      "address": "127 Main St",
      "monthly_rent": 2350,
      "bedrooms": 3,
      "bathrooms": 2,
      "square_footage": 1520,
      "distance_miles": 0.2
    }
  ],
  "rent_per_sqft": 1.60,
  "market_trends": {
    "monthly_change": 0.02,
    "yearly_change": 0.08
  }
}
```

### Property Listings Tools

#### `getSaleListings`
Search for active property listings for sale.

**Parameters:**
```json
{
  "address": "string (optional) - Property address",
  "city": "string (optional) - City name",
  "state": "string (optional) - State name",
  "zipCode": "string (optional) - ZIP code",
  "latitude": "number (optional) - Search center latitude",
  "longitude": "number (optional) - Search center longitude",
  "radius": "number (optional) - Search radius in miles",
  "propertyType": "string (optional) - Property type filter",
  "bedrooms": "integer (optional) - Number of bedrooms",
  "bathrooms": "number (optional) - Number of bathrooms",
  "squareFootage": "integer (optional) - Square footage",
  "priceMin": "integer (optional) - Minimum listing price",
  "priceMax": "integer (optional) - Maximum listing price",
  "status": "string (optional) - Listing status filter",
  "limit": "integer (default: 20) - Result limit",
  "offset": "integer (default: 0) - Result offset for pagination"
}
```

**Output:**
```json
{
  "listings": [
    {
      "id": "listing_12345",
      "address": "456 Oak St, Austin, TX",
      "price": 525000,
      "bedrooms": 4,
      "bathrooms": 3,
      "squareFootage": 2100,
      "propertyType": "Single Family",
      "status": "Active",
      "listingDate": "2024-01-10",
      "daysOnMarket": 5
    }
  ],
  "total_count": 45,
  "search_criteria": {
    "city": "Austin",
    "state": "TX",
    "priceMax": 600000
  }
}
```

#### `getRentalListings`
Search for active rental property listings.

**Parameters:**
```json
{
  "address": "string (optional) - Property address",
  "city": "string (optional) - City name",
  "state": "string (optional) - State name",
  "zipCode": "string (optional) - ZIP code",
  "latitude": "number (optional) - Search center latitude",
  "longitude": "number (optional) - Search center longitude",
  "radius": "number (optional) - Search radius in miles",
  "propertyType": "string (optional) - Property type filter",
  "bedrooms": "integer (optional) - Number of bedrooms",
  "bathrooms": "number (optional) - Number of bathrooms",
  "squareFootage": "integer (optional) - Square footage",
  "rentMin": "integer (optional) - Minimum monthly rent",
  "rentMax": "integer (optional) - Maximum monthly rent",
  "status": "string (optional) - Listing status filter",
  "limit": "integer (default: 20) - Result limit",
  "offset": "integer (default: 0) - Result offset for pagination"
}
```

#### `getSaleListingById`
Get detailed sale listing information by listing ID.

**Parameters:**
```json
{
  "listingId": "string (required) - Unique sale listing identifier"
}
```

#### `getRentalListingById`
Get detailed rental listing information by listing ID.

**Parameters:**
```json
{
  "listingId": "string (required) - Unique rental listing identifier"
}
```

### Market Analysis Tools

#### `getMarketStatistics`
Get market statistics and trends for a ZIP code area.

**Parameters:**
```json
{
  "zipCode": "string (required) - ZIP code for market analysis"
}
```

**Output:**
```json
{
  "zipCode": "78701",
  "market_statistics": {
    "median_sale_price": 485000,
    "median_rent": 2400,
    "price_per_sqft": 320,
    "rent_per_sqft": 1.60,
    "inventory_count": 45,
    "days_on_market_avg": 28,
    "price_change_30d": 0.02,
    "price_change_1y": 0.12
  },
  "property_types": [
    {
      "type": "Single Family",
      "count": 30,
      "median_price": 525000
    },
    {
      "type": "Condo",
      "count": 15,
      "median_price": 385000
    }
  ]
}
```

#### `analyzeProperty`
Get comprehensive property analysis including value estimate, rent estimate, and comparables.

**Parameters:**
```json
{
  "address": "string (required) - Property address",
  "propertyType": "string (optional) - Property type",
  "bedrooms": "integer (optional) - Number of bedrooms",
  "bathrooms": "number (optional) - Number of bathrooms",
  "squareFootage": "integer (optional) - Square footage"
}
```

**Output:**
```json
{
  "property": {
    "address": "123 Main St, Austin, TX",
    "propertyType": "Single Family",
    "bedrooms": 3,
    "bathrooms": 2,
    "squareFootage": 1500
  },
  "value_estimate": {
    "value": 485000,
    "confidence": 0.85
  },
  "rent_estimate": {
    "rent": 2400,
    "confidence": 0.82
  },
  "investment_metrics": {
    "gross_yield": 5.9,
    "price_to_rent_ratio": 16.9,
    "cash_flow_potential": "positive"
  }
}
```

#### `compareMarkets`
Compare market statistics across multiple ZIP code areas.

**Parameters:**
```json
{
  "zipCodes": "array[string] (required) - List of ZIP codes to compare"
}
```

**Output:**
```json
{
  "markets": {
    "78701": {
      "median_sale_price": 485000,
      "median_rent": 2400,
      "price_change_1y": 0.12
    },
    "78702": {
      "median_sale_price": 425000,
      "median_rent": 2200,
      "price_change_1y": 0.08
    }
  },
  "comparison": {
    "highest_appreciation": "78701",
    "best_rental_yield": "78702",
    "lowest_price_entry": "78702"
  }
}
```

#### `findInvestmentProperties`
Find potential investment properties with value and rent estimates for ROI analysis.

**Parameters:**
```json
{
  "city": "string (required) - City to search",
  "state": "string (required) - State to search",
  "maxPrice": "integer (optional) - Maximum purchase price",
  "minBedrooms": "integer (optional) - Minimum number of bedrooms",
  "propertyType": "string (optional) - Property type filter",
  "limit": "integer (default: 10) - Number of properties to analyze"
}
```

**Output:**
```json
{
  "search_criteria": {
    "city": "Austin",
    "state": "TX",
    "maxPrice": 500000,
    "minBedrooms": 2
  },
  "properties": [
    {
      "listing": {
        "address": "789 Investment Ave",
        "price": 425000,
        "bedrooms": 3,
        "bathrooms": 2
      },
      "rent_estimate": {
        "rent": 2200
      },
      "investment_metrics": {
        "monthly_gross_yield_percent": 0.52,
        "annual_gross_yield_percent": 6.21,
        "price_to_rent_ratio": 16.1
      }
    }
  ]
}
```

---

## 📈 Accounting Tools

Double-entry accounting system via Ledger CLI for comprehensive financial reporting and analysis.

> **Note**: Based on the powerful [Ledger CLI](https://github.com/minhyeoky/mcp-server-ledger) system for professional accounting workflows.

### Account Balance Tools

#### `ledger_balance`
Shows account balances with powerful filtering options for comprehensive financial reporting.

**Parameters:**
```json
{
  "query": "string (optional) - Query pattern to filter accounts (e.g., 'Assets', 'Expenses:Food')",
  "date_range": "string (optional) - Date range for the report (e.g., '2024', 'last month', 'Q1 2024')",
  "display_options": "object (optional) - Additional display formatting options"
}
```

**Output:**
```json
{
  "success": true,
  "balance_report": "Formatted balance report showing account totals",
  "total_balance": "Summary of filtered accounts",
  "query_applied": "Assets",
  "date_range": "2024"
}
```

#### `ledger_register`
Shows transaction register with detailed history for account analysis.

**Parameters:**
```json
{
  "query": "string (optional) - Query pattern to filter transactions",
  "date_range": "string (optional) - Date range for transactions",
  "sorting_options": "object (optional) - Options for sorting the register output"
}
```

**Output:**
```json
{
  "success": true,
  "register_report": "Detailed transaction register with dates, descriptions, and amounts",
  "transaction_count": 45,
  "date_range": "last month",
  "total_amount": "$2,450.00"
}
```

### Account Management Tools

#### `ledger_accounts`
Lists all accounts in the ledger file with optional filtering.

**Parameters:**
```json
{
  "query": "string (optional) - Query pattern to filter account names"
}
```

**Output:**
```json
{
  "success": true,
  "accounts": [
    "Assets:Checking",
    "Assets:Savings",
    "Income:Salary",
    "Expenses:Food",
    "Expenses:Utilities"
  ],
  "account_count": 25,
  "query_applied": "Income"
}
```

#### `ledger_payees`
Lists all payees from transactions with optional filtering.

**Parameters:**
```json
{
  "query": "string (optional) - Query pattern to filter payee names"
}
```

**Output:**
```json
{
  "success": true,
  "payees": [
    "Amazon",
    "Whole Foods",
    "Utility Company",
    "Employer Corp"
  ],
  "payee_count": 42,
  "query_applied": "Amazon"
}
```

#### `ledger_commodities`
Lists all commodities (currencies) used in the ledger.

**Parameters:**
```json
{
  "query": "string (optional) - Query pattern to filter commodities"
}
```

**Output:**
```json
{
  "success": true,
  "commodities": [
    "USD",
    "EUR",
    "AAPL",
    "BTC"
  ],
  "commodity_count": 8
}
```

### Transaction Analysis Tools

#### `ledger_print`
Prints transactions in ledger format for detailed analysis.

**Parameters:**
```json
{
  "query": "string (optional) - Query pattern to filter transactions",
  "date_range": "string (optional) - Date range for transactions"
}
```

**Output:**
```json
{
  "success": true,
  "ledger_entries": "Formatted ledger entries in standard double-entry format",
  "transaction_count": 15,
  "date_range": "Q1 2024"
}
```

#### `ledger_stats`
Shows comprehensive statistics about the ledger file.

**Parameters:**
```json
{
  "query": "string (optional) - Query pattern to filter statistics"
}
```

**Output:**
```json
{
  "success": true,
  "statistics": {
    "total_transactions": 523,
    "date_range": "2020-01-01 to 2024-12-31",
    "account_count": 45,
    "payee_count": 78,
    "commodity_count": 6
  },
  "file_info": {
    "file_size": "125 KB",
    "last_modified": "2024-01-15"
  }
}
```

### Budget and Analysis Tools

#### `ledger_budget`
Shows budget analysis with variance reporting.

**Parameters:**
```json
{
  "query": "string (optional) - Query pattern for budget analysis",
  "date_range": "string (optional) - Date range for budget period",
  "reporting_period": "string (optional) - Period grouping (monthly, quarterly, yearly)"
}
```

**Output:**
```json
{
  "success": true,
  "budget_report": "Formatted budget vs actual analysis",
  "period": "monthly",
  "variance_summary": {
    "over_budget": "$245.00",
    "under_budget": "$156.00",
    "categories_analyzed": 12
  }
}
```

#### `ledger_raw_command`
Runs a raw Ledger CLI command for advanced functionality.

**Parameters:**
```json
{
  "command_args": "array[string] (required) - Command arguments as list of strings (e.g., ['bal', '--depth', '2', 'Assets'])"
}
```

**Output:**
```json
{
  "success": true,
  "command_output": "Raw output from Ledger CLI command",
  "command_executed": "ledger bal --depth 2 Assets",
  "exit_code": 0
}
```

---

## 📄 Document Processing Tools

Document reading and analysis tools for various file formats.

### Document Reading Tools

#### `readDocument`
Read and extract content from various document formats (PDF, TXT, DOCX, CSV, JSON).

**Parameters:**
```json
{
  "file_path": "string (required) - Path to the document file to read",
  "extract_metadata": "boolean (default: true) - Whether to extract document metadata",
  "max_chars": "integer (default: 50000) - Maximum characters to extract (for large documents)"
}
```

**Output:**
```json
{
  "success": true,
  "content": "Document content extracted...",
  "metadata": {
    "file_type": "pdf",
    "page_count": 10,
    "file_size": 1024000,
    "title": "Document Title"
  },
  "char_count": 25000
}
```

#### `listWorkspaceDocuments`
List all documents in the current workspace directory.

**Parameters:**
```json
{
  "workspace_path": "string (required) - Path to workspace directory",
  "file_types": "array[string] (default: ['.pdf', '.txt', '.docx', '.csv', '.json']) - File extensions to include"
}
```

**Output:**
```json
{
  "documents": [
    {
      "path": "/workspace/report.pdf",
      "name": "report.pdf",
      "size": 1024000,
      "type": "pdf",
      "modified": "2024-01-15T10:30:00Z"
    }
  ],
  "total_count": 15
}
```

#### `analyzeDocumentStructure`
Analyze document structure and extract key information.

**Parameters:**
```json
{
  "file_path": "string (required) - Path to document file",
  "analysis_type": "string (default: 'summary') - Type of analysis: summary/detailed/metadata_only"
}
```

**Output:**
```json
{
  "analysis_type": "summary",
  "structure": {
    "sections": 5,
    "tables": 3,
    "images": 2,
    "headings": ["Introduction", "Analysis", "Conclusion"]
  },
  "key_metrics": {
    "word_count": 2500,
    "page_count": 10,
    "reading_time_minutes": 10
  }
}
```

---

## 🔧 Tool Usage Guidelines

### Authentication
All tools require authentication using Theta API keys:

```bash
Authorization: Bearer theta_your_api_key_here
```

### Error Handling
Tools return standardized error responses:

```json
{
  "error": {
    "code": "INVALID_PARAMETER",
    "message": "The ticker symbol 'INVALID' was not found",
    "details": {
      "parameter": "ticker",
      "value": "INVALID"
    }
  }
}
```

### Rate Limits
- **Excel Tools**: No rate limits (local processing)
- **Document Processing Tools**: No rate limits (local processing)
- **Accounting Tools**: No rate limits (local Ledger CLI processing)
- **Public Financial Market Tools**: 1000 calls/hour per API key
- **Private Market Tools**: 500 calls/hour per API key (Crunchbase)
- **Real Estate Tools**: 1000 calls/hour per API key (RentCast + OneBuild)

### Session Management
Excel tools support session-aware file paths for isolated workspaces:

```json
{
  "session_id": "sess_12345",
  "file_name": "report.xlsx"
}
```

---

## 🚀 Integration Examples

### OpenAI Function Calling
```json
{
  "type": "function",
  "function": {
    "name": "call_theta_tools",
    "description": "Call Excel or Finance tools from Theta MCP Gateway",
    "parameters": {
      "type": "object",
      "properties": {
        "tool_name": {
          "type": "string",
          "enum": ["excel_create_workbook", "getPriceSnapshot", "getCrunchbaseCompanyInfo", "getValueEstimate", "searchSources", "readDocument", "ledger_balance", "ledger_register"]
        },
        "arguments": {
          "type": "object"
        }
      },
      "required": ["tool_name", "arguments"]
    }
  }
}
```

### Direct HTTP API
```bash
curl -X POST https://playground.thetasoftware.ai/mcp \
  -H "Authorization: Bearer theta_your_api_key" \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "method": "tools/call",
    "params": {
      "name": "getPriceSnapshot",
      "arguments": {"ticker": "AAPL"}
    },
    "id": 1
  }'
```

### Python SDK Example
```python
import requests

headers = {
    "Authorization": "Bearer theta_your_api_key",
    "Content-Type": "application/json"
}

# Get stock price
response = requests.post(
    "https://playground.thetasoftware.ai/mcp",
    headers=headers,
    json={
        "jsonrpc": "2.0",
        "method": "tools/call", 
        "params": {
            "name": "getPriceSnapshot",
            "arguments": {"ticker": "AAPL"}
        },
        "id": 1
    }
)

data = response.json()
print(f"AAPL Price: ${data['result']['price']}")
```

### Comprehensive Investment Analysis Workflow
```python
# 1. Research private market companies
company_data = call_tool("getCrunchbaseCompanyInfo", {
    "company": "proptech_startup"
})

# 2. Find real estate properties
properties = call_tool("getPropertyRecords", {
    "city": "Austin", 
    "state": "TX",
    "maxPrice": 500000
})

# 3. Get public market comparisons
public_reits = call_tool("searchCompanies", {
    "query": "real estate investment trust"
})

# 4. Analyze personal finances for investment capacity
account_balances = call_tool("ledger_balance", {
    "query": "Assets",
    "date_range": "2024"
})

investment_history = call_tool("ledger_register", {
    "query": "Assets:Investments",
    "date_range": "last 12 months"
})

# 5. Get construction costs for development
materials = call_tool("searchSources", {
    "search_term": "kitchen renovation",
    "state": "Texas",
    "county": "Travis"
})

# 6. Process market research documents
market_report = call_tool("readDocument", {
    "file_path": "/workspace/market_analysis.pdf"
})

# 7. Create comprehensive Excel analysis
call_tool("excel_create_workbook", {
    "file_name": "investment_analysis.xlsx"
})

# Include financial position data
call_tool("excel_write_data_to_excel", {
    "file_name": "investment_analysis.xlsx",
    "sheet_name": "Financial_Position",
    "data": account_balances_data
})

call_tool("excel_write_data_to_excel", {
    "file_name": "investment_analysis.xlsx",
    "sheet_name": "Properties",
    "data": properties_data
})

call_tool("excel_create_chart", {
    "file_name": "investment_analysis.xlsx",
    "sheet_name": "Analysis",
    "chart_type": "scatter",
    "data_range": "A1:C20",
    "title": "ROI vs. Risk Analysis"
})
```

---

## 📝 Notes

- All monetary values in USD unless specified
- Dates in ISO 8601 format (YYYY-MM-DDTHH:MM:SSZ)
- Geographic data uses US standard (state/county/ZIP)
- Excel files stored in session-isolated directories
- Financial data updated in real-time during market hours
- Construction costs vary by location and market conditions
- Property estimates provided for informational purposes only

---

**Last Updated:** January 2024  
**API Version:** 2.0  
**Total Tools:** 65+

For support or additional features, contact: support@thetasoftware.ai
