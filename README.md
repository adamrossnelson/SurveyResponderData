# SurveyResponderData

A static file host for non-confidential CSV and Parquet data files. This is **not** a software project — it is a companion data repository for [SurveyResponder](https://github.com/adamrossnelson/SurveyResponder) and [SurveyResponderMemos](https://github.com/adamrossnelson/SurveyResponderMemos).

## Why This Repo Exists

Large data files create bloat when stored alongside application code. By hosting data here in its own repository, we keep [SurveyResponder](https://github.com/adamrossnelson/SurveyResponder) and [SurveyResponderMemos](https://github.com/adamrossnelson/SurveyResponderMemos) lean while providing stable, publicly accessible URLs that anyone can use to load data directly from code.

**You never need to clone, pull, or fetch this repository.** All file management happens through the GitHub web interface. All data consumption happens via raw URLs.

## Repository Structure

```
├── README.md
├── CONTRIBUTING.md
├── LICENSE
├── data/
│   ├── README.md          ← manifest of available datasets
│   └── (CSV and Parquet files go here)
```

## How to Access the Data

Every file in the `data/` directory is available at:

```
https://raw.githubusercontent.com/adamrossnelson/SurveyResponderData/main/data/<filename>
```

### Python (pandas)

```python
import pandas as pd

# CSV
df = pd.read_csv(
    "https://raw.githubusercontent.com/adamrossnelson/SurveyResponderData/main/data/survey_results.csv"
)

# Parquet (preferred — smaller, faster, typed columns)
df = pd.read_parquet(
    "https://raw.githubusercontent.com/adamrossnelson/SurveyResponderData/main/data/survey_results.parquet"
)
```

### Python (Polars)

```python
import polars as pl

df = pl.read_csv(
    "https://raw.githubusercontent.com/adamrossnelson/SurveyResponderData/main/data/survey_results.csv"
)

df = pl.read_parquet(
    "https://raw.githubusercontent.com/adamrossnelson/SurveyResponderData/main/data/survey_results.parquet"
)
```

### R

```r
library(readr)

df <- read_csv(
    "https://raw.githubusercontent.com/adamrossnelson/SurveyResponderData/main/data/survey_results.csv"
)
```

```r
library(arrow)

df <- read_parquet(
    "https://raw.githubusercontent.com/adamrossnelson/SurveyResponderData/main/data/survey_results.parquet"
)
```

## Caching Warning

> **Note:** `raw.githubusercontent.com` is CDN-cached. After a file is updated, the old version may continue to be served for **several minutes**. If you just uploaded a new file and your code still loads the old data, wait a few minutes and try again.

## File Format Strategy

| Format  | Best For                                  | Notes                                       |
|---------|-------------------------------------------|---------------------------------------------|
| CSV     | Human inspection, small files             | GitHub renders CSVs in the web UI           |
| Parquet | Programmatic access, large files          | 5–10× smaller, faster to load, typed columns|
| JSON    | Preserving the parameters used to generate a CSV | Pairs with a CSV of the same base name |

When both formats exist for the same dataset, the **Parquet version is canonical**.

## File Naming Conventions

Use **lowercase** with **underscores** — no spaces, no capital letters.

Each CSV data file may have an accompanying **JSON file** that records the parameters used to generate it. To keep these paired, use the **same base name** for both files:

```
data/
├── respondent_demographics_2025.csv        ← the data
├── respondent_demographics_2025.json       ← parameters used to create the CSV
├── survey_results_2025_03.csv
├── survey_results_2025_03.json
└── ...
```

This naming convention makes it immediately clear which JSON belongs to which CSV. When browsing the `data/` directory, paired files will sort next to each other alphabetically.

If you need distinct versions to coexist, use date-stamped filenames (e.g., `survey_results_2025_03.csv` / `survey_results_2025_03.json`).

## File Size Limits

- GitHub **warns** at files over **50 MB** and **blocks** files over **100 MB**.
- For any CSV larger than ~10 MB, prefer Parquet.
- Keep all individual files under **50 MB** whenever possible.

## How to Contribute / Update Files

All uploads happen through the **GitHub web interface**. Do **not** clone this repository.

1. Navigate to the [`data/`](data/) folder on GitHub.
2. Click **Add file** → **Upload files**.
3. Drag and drop your `.csv` or `.parquet` file(s).
4. Write a brief commit message describing the change.
5. Commit directly to `main`.

If you are replacing an existing file, upload the new version **with the same filename** — git handles version history automatically. If you need distinct versions to coexist, use date-stamped filenames like `survey_results_2025_03.csv`.

For full contribution guidelines, see [CONTRIBUTING.md](CONTRIBUTING.md).

## Related Repositories

- **[SurveyResponder](https://github.com/adamrossnelson/SurveyResponder)** — the main application
- **[SurveyResponderMemos](https://github.com/adamrossnelson/SurveyResponderMemos)** — memos and documentation

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.
