# U.S. Congressional Stock & Options Trading Open Dataset
### Real-Time Disclosures Under the Stop Trading on Congressional Knowledge (STOCK) Act of 2012

[![Live Platform](https://img.shields.io/badge/Live%20Platform-CapitolStockWatch.com-0066FF?style=for-the-badge&logo=google-chrome&logoColor=white)](https://www.capitolstockwatch.com)
[![GitHub Repo](https://img.shields.io/badge/GitHub-Open_Data_Repo-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/CapitolStockWatch/capitol-stock-watch-open-data)
[![Sync Cadence](https://img.shields.io/badge/Sync%20Cadence-Every%202%20Hours-00C853?style=for-the-badge&logo=githubactions&logoColor=white)](https://www.capitolstockwatch.com/recent)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg?style=for-the-badge)](https://creativecommons.org/licenses/by/4.0/)
[![No Paywall](https://img.shields.io/badge/Paywall-100%25_Free-orange?style=for-the-badge)](https://www.capitolstockwatch.com/)

Maintained by the **[CapitolStockWatch Research Desk](https://www.capitolstockwatch.com)**.

---

## 1. Overview & Provenance

This open dataset provides normalized, machine-readable securities transactions disclosed by members of the **United States House of Representatives** and **United States Senate** under the **Stop Trading on Congressional Knowledge (STOCK) Act of 2012 (Public Law 112-105)**.

Unlike commercial terminals that charge subscription fees or delay filings behind paywalls, **CapitolStockWatch publishes 100% of its parsed disclosures for public research, investigative journalism, and algorithmic finance**.

### Official Government Primary Sources
* **U.S. House of Representatives:** Office of the Clerk — [Financial Disclosure Reports & Periodic Transaction Reports (PTR)](https://disclosures-clerk.house.gov/FinancialDisclosure).
* **U.S. Senate:** Senate Select Committee on Ethics — [Electronic Financial Disclosure (eFD) System](https://efdsearch.senate.gov/search/).
* **Executive Branch:** [Office of Government Ethics (OGE) Form 278e](https://www.oge.gov/).

---

## 2. Direct Download Links (Updated Bi-Hourly)

| Dataset | Format | Direct URL | Description |
| :--- | :---: | :--- | :--- |
| **All Congressional Trades** | CSV | `https://www.capitolstockwatch.com/data/open-data/congress_trades_latest.csv` | Full chronological feed of recent transactions across House & Senate. |
| **STOCK Act Violations** | CSV | `https://www.capitolstockwatch.com/data/open-data/stock_act_violations.csv` | All transactions disclosed beyond the statutory 45-day deadline. |
| **Options Contracts** | CSV | `https://www.capitolstockwatch.com/data/open-data/congress_options_trades.csv` | Congressional Call and Put options contracts with strike prices and expirations. |
| **Politicians Directory** | CSV | `https://www.capitolstockwatch.com/data/open-data/politicians_directory.csv` | Lawmakers roster with win rates, trade counts, volume, and profile links. |
| **Raw JSON Feed** | JSON | `https://www.capitolstockwatch.com/data/trades.json` | Complete raw JSON payload with performance return benchmarks and insider tags. |

---

## 3. Data Dictionary / Schema

### `congress_trades_latest.csv`
| Column | Type | Example | Description |
| :--- | :--- | :--- | :--- |
| `filer_name` | String | `Nancy Pelosi` | Name of the Member of Congress. |
| `chamber` | String | `house` / `senate` | Chamber of Congress. |
| `party` | String | `D` / `R` / `I` | Political party affiliation. |
| `state` | String | `CA`, `TX`, `FL` | State represented. |
| `transaction_date` | Date | `2026-09-23` | Date the trade was executed by the lawmaker or spouse. |
| `filing_date` | Date | `2026-10-21` | Official date disclosed to House Clerk or Senate Secretary. |
| `disclosure_delay_days` | Integer | `28` | Number of calendar days between execution and disclosure. |
| `is_late_filing` | String | `Yes` / `No` | Flagged `Yes` if disclosure exceeded statutory 45 days. |
| `ticker` | String | `NVDA` | Public equity or derivative ticker symbol. |
| `asset_name` | String | `Nvidia Corporation` | Clean legal asset description. |
| `security_type` | String | `stock` / `option` | Asset category. |
| `transaction_type` | String | `Purchase`, `Sale (Full)` | Direction of transaction. |
| `amount_range` | String | `$1,001 - $15,000` | Mandatory STOCK Act reporting bracket. |
| `amount_min_usd` | Float | `1001` | Statutory lower bound in USD. |
| `amount_max_usd` | Float | `15000` | Statutory upper bound in USD. |
| `filing_url` | URL | `https://...` | Official link to certified government PTR PDF filing. |

---

## 4. Quickstart Code Examples

### Python (Pandas)
```python
import pandas as pd

# Load directly from CapitolStockWatch Open Data endpoint
url = "https://www.capitolstockwatch.com/data/open-data/congress_trades_latest.csv"
df = pd.read_csv(url)

# Filter for top purchased stocks by House members
buys = df[(df['transaction_type'] == 'Purchase') & (df['chamber'] == 'house')]
top_stocks = buys['ticker'].value_counts().head(10)

print("Top 10 Stocks Bought by U.S. House Members:")
print(top_stocks)
```

### R (tidyverse)
```r
library(readr)
library(dplyr)

trades <- read_csv("https://www.capitolstockwatch.com/data/open-data/congress_trades_latest.csv")

# Identify members with the highest late filing count (>45 days)
late_filers <- trades %>%
  filter(is_late_filing == "Yes") %>%
  count(filer_name, party, sort = TRUE)

print(head(late_filers, 10))
```

---

## 5. Academic & Press Citation

If you use this dataset or data from [CapitolStockWatch.com](https://www.capitolstockwatch.com) in academic papers, student research, journalistic articles, or quantitative backtests, please cite as follows:

### BibTeX
```bibtex
@misc{capitolstockwatch2026,
  title = {CapitolStockWatch: Open Congressional Securities Transactions and STOCK Act Compliance Dataset},
  author = {{CapitolStockWatch Research Desk}},
  year = {2026},
  howpublished = {\url{https://www.capitolstockwatch.com}},
  note = {Public domain financial disclosures synced from the U.S. House of Representatives and U.S. Senate}
}
```

### APA Style
> CapitolStockWatch Research Desk. (2026). *CapitolStockWatch: Open Congressional Securities Transactions and STOCK Act Compliance Dataset*. Retrieved from https://www.capitolstockwatch.com.

---

## 6. Terms of Use & License
This dataset is published under the **[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)** license. You are free to share, copy, analyze, and build upon this data for commercial and non-commercial purposes, provided appropriate attribution and a link to **[CapitolStockWatch.com](https://www.capitolstockwatch.com)** are preserved.
