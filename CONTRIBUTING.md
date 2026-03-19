# Contributing to SurveyResponderData

This repository is a static data host — not a software project. There is no code to build, no tests to run, and no dependencies to install. Contributing means uploading or updating data files.

## The One Rule

**Do not clone this repository.** All file management happens through the GitHub web interface. This is by design — it prevents contributors from downloading the full git history of (potentially large) data files.

## How to Upload or Update a File

1. Go to the [`data/`](data/) folder on GitHub.
2. Click **Add file** → **Upload files**.
3. Drag and drop your `.csv`, `.json`, or `.txt` file(s) into the upload area.
4. Write a short commit message (e.g., "Update respondent_demographics Q1 2025").
5. Select **Commit directly to the `main` branch**.
6. Click **Commit changes**.

## Accepted File Formats

| Extension  | When to Use                                                      |
|------------|------------------------------------------------------------------|
| `.csv`     | Default for datasets; human-readable in GitHub                   |
| `.json`    | Parameter snapshot that accompanies a CSV (`{base}_params.json`) |
| `.txt`     | Optional human notes for a dataset (`{base}_notes.txt`)          |


## File Naming Conventions

- Use lowercase with underscores — no spaces, no capital letters.
- Choose descriptive names: `respondent_demographics_2025.csv`, not `data2.csv`.
- If you need distinct versions to coexist, use date-stamped filenames:
  `survey_results_2025_03.csv`, `survey_results_2025_06.csv`.

### Dataset Bundles (A–E Companion Files)

Each dataset is identified by a unique base name (`{base}`). The `{base}` portion must be unique within `data/`, because it is what associates all companion files in the bundle.

For every raw dataset export there will be an accompanying parameter snapshot JSON. Optionally, you may also include a notes file. The full bundle looks like this:

| File pattern | Role | How it is created |
|---|---|---|
| `{base}.csv` | A) Raw responses export | `responder.run_write("{base}.csv")` |
| `{base}_ready.csv` | B) Analysis-ready data (numeric + reverse-coded) | Post-processing (`code tbd`) |
| `{base}_nan_audit.csv` | C) Missing-data audit | Audit step (`code tbd`) |
| `{base}_notes.txt` | D) Human notes (optional) | Manual |
| `{base}_params.json` | E) Reproducibility snapshot | `responder.run_write("{base}.csv")` |

When browsing the `data/` directory, companion files sort next to each other alphabetically because they share the same base name.

```
data/
├── res_qs_25.csv                ← Exported by `run_write` method
├── res_qs_25_params.json        ← Preserved by `run_write` method
├── res_qs_25_ready.csv          ← Analysis-ready data
├── res_qs_25_nan_audit.csv      ← Missing-data audit
├── res_qs_25_notes.txt          ← Human notes (optional)
└── ...
```

## Revising Committed Files

Avoid revising a CSV file once it has been committed. If a correction is truly necessary, discuss it in an issue first. Git tracks previous versions in its history automatically, so there is no need to rename or archive old files.

## File Size Guidelines

- GitHub warns at files over 50 MB and blocks files over 100 MB.
- For any CSV larger than ~10 MB, prefer Parquet.
- Keep all individual files under 50 MB whenever possible.

## Where to Put Files

All data files go in the `data/` directory. Do not create subdirectories unless there is a clear organizational need (discuss in an issue first).

## Updating the Data Index

After uploading a new dataset, please update [`DataIndex.md`](DataIndex.md) to include:

- **Base name**
- **One-line description**
- **Date last updated**
- **Files in the bundle**

This index update helps other users discover what data is available without browsing the directory.

## What Not to Do

- **Do not clone, fork, or pull this repo** for the purpose of adding files.
- **Do not upload confidential or personally identifiable data.**
- **Do not revise a committed CSV** — if a correction is necessary, open an issue first.
- **Do not delete files** — if a file should be removed, open an issue.
