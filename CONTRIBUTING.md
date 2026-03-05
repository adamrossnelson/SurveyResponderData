# Contributing to SurveyResponderData

This repository is a static data host — not a software project. There is no code to build, no tests to run, and no dependencies to install. Contributing means uploading or updating data files.

## The One Rule

**Do not clone this repository.** All file management happens through the GitHub web interface. This is by design — it prevents contributors from downloading the full git history of (potentially large) data files.

## How to Upload or Update a File

1. Go to the [`data/`](data/) folder on GitHub.
2. Click **Add file** → **Upload files**.
3. Drag and drop your file(s) into the upload area.
4. Write a short commit message (e.g., "Update respondent_demographics Q1 2025").
5. Select **Commit directly to the `main` branch**.
6. Click **Commit changes**.

## Accepted File Formats

| Extension  | When to Use                                                    |
|------------|----------------------------------------------------------------|
| `.csv`     | Default for small-to-medium datasets; human-readable in GitHub |
| `.parquet` | Preferred for programmatic access and files over ~10 MB        |
| `.json`    | Preserving the parameters used to generate a CSV file          |

## File Naming Conventions

- Use **lowercase** with **underscores** — no spaces, no capital letters.
- Choose descriptive names: `respondent_demographics_2025.csv`, not `data2.csv`.
- If you need distinct versions to coexist, use date-stamped filenames:
  `survey_results_2025_03.csv`, `survey_results_2025_06.csv`.

### Pairing CSV and JSON Files

Each CSV should have an accompanying `.json` file that records the parameters used to generate it. **Use the same base name** for both so the pairing is obvious:

```
respondent_demographics_2025.csv      ← the data
respondent_demographics_2025.json     ← parameters used to create the CSV
```

Always upload both files together. When browsing the `data/` directory, paired files will sort next to each other alphabetically.

## Replacing an Existing File

Upload the new version **with the exact same filename**. Git tracks the previous version in its history automatically. There is no need to rename or archive old files.

## File Size Guidelines

| Threshold | What Happens                                    |
|-----------|-------------------------------------------------|
| > ~10 MB  | Provide a Parquet version alongside the CSV     |
| > 20 MB   | Parquet version is **required**; note it as the preferred format |
| > 50 MB   | GitHub displays a warning on the file           |
| > 100 MB  | **GitHub blocks the upload** — file must be split or compressed |

Keep individual files under **50 MB** whenever possible.

## Where to Put Files

All data files go in the `data/` directory. Do not create subdirectories unless there is a clear organizational need (discuss in an issue first).

## Updating the Data Manifest

After uploading a new dataset, please update [`data/README.md`](data/README.md) to include:

- **Filename**
- **One-line description**
- **Date last updated**
- **Format(s) available**

This helps other users discover what data is available without browsing the directory.

## What Not to Do

- **Do not clone, fork, or pull this repo** for the purpose of adding files.
- **Do not add scripts, notebooks, or code** — those belong in [SurveyResponder](https://github.com/adamrossnelson/SurveyResponder) or [SurveyResponderMemos](https://github.com/adamrossnelson/SurveyResponderMemos).
- **Do not upload confidential or personally identifiable data.**
- **Do not delete files** — if a file should be removed, open an issue.
