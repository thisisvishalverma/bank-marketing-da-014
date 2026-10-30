# Bank Marketing Campaign Analysis

**Project ID:** DA-014  
**Domain:** Marketing Analytics

This working prototype explores historical bank telemarketing records and their term-deposit subscription outcomes. It includes a Streamlit dashboard, shared cleaning/calculation functions, a Jupyter notebook with the same analysis logic, and a downloader for the public UCI dataset. The local project bundle includes the CSV; the GitHub deployment can fetch it from UCI the first time the app starts.

## Dataset and response-rate definition

The dataset is UCI's `bank-additional-full.csv`, with 41,188 campaign contact records. The target column is `y`: `yes` means a client subscribed to a term deposit, and `no` means they did not. The local ZIP includes the CSV. If it is absent (as in the GitHub deployment repository), the dashboard downloads the official UCI archive on first launch.

**Response rate = records where `y == yes` ÷ all records with a valid `y` in the selected cohort.** Each row is a contact record. This dataset does not provide a unique customer ID, so the dashboard does not claim a unique-person denominator. The cleaning step trims text, maps `?` to missing, retains literal `unknown` values as `Unknown`, parses numeric columns, and excludes only records without a valid yes/no target. Source details and attribution are in [`data/SOURCE.md`](data/SOURCE.md).

The UCI source reports 4,640 `yes` records out of 41,188 (11.27%). The dashboard and notebook recompute this figure from the CSV, not a hard-coded KPI.

## Run the dashboard locally

Python 3.10 or newer is recommended.

1. Open a terminal in the project folder.
2. Create and activate a virtual environment:

   **Windows PowerShell**
   ```powershell
   py -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

   **macOS/Linux**
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

3. Install dependencies and launch:

   ```bash
   python -m pip install -r requirements.txt
   streamlit run app.py
   ```

4. Open the local URL printed by Streamlit (usually `http://localhost:8501`).

The CSV is bundled. If it is missing, restore it from the official UCI archive with:

```bash
python scripts/download_dataset.py
```

## Run the analysis notebook

Install the same requirements, start Jupyter from the project folder, and open `bank_marketing_analysis.ipynb`:

```bash
jupyter lab
```

Run **Kernel → Restart Kernel and Run All Cells**. The notebook imports the shared `analysis.py` module, which is also used by the Streamlit dashboard. To use Google Colab, upload the ZIP, extract the whole project, set the notebook working directory to the extracted project folder, then run all cells.

## Dashboard features

- Overall or filtered record count, successful response count, response rate, and average campaign contacts.
- Sidebar filters across available categorical fields and numeric ranges.
- Segment response rates, campaign contact-frequency bands, contact channel, month, and weekday charts.
- Filtered data preview and cleaning summary.
- Dynamic findings with a 30-record group-size threshold and recommendations framed as hypotheses for controlled testing.

`duration` (call duration in seconds) is shown for exploration but is only known after a contact; it should not inform a pre-call targeting decision. The analysis is descriptive and does not establish causation.

## Project files

- `app.py` — Streamlit interactive dashboard.
- `analysis.py` — shared cleaning, KPI, filter, grouping, and finding calculations.
- `bank_marketing_analysis.ipynb` — end-to-end exploratory analysis using those shared calculations.
- `data/bank-additional-full.csv` — bundled in the local ZIP; fetched from UCI for the hosted app if absent.
- `scripts/download_dataset.py` — downloader for the official UCI archive.
- `PROTOTYPE_DEMO.md` — short faculty demonstration guide.
- `requirements.txt` — runtime and notebook dependencies.

## Live dashboard and validation

**Public dashboard:** [Open the Bank Marketing Campaign Analysis app](https://bank-marketing-da-014-u3pnizm4t9g6wk8tpelvfg.streamlit.app/)

The deployed app was opened and verified after its first run. It loaded all 41,188 records, displayed 4,640 successful responses and an 11.27% overall response rate, and rendered the segment, contact-frequency, channel, month, and weekday charts. The methodology and findings pages loaded, and a category filter changed the findings before being restored to its default selection.

The app fetches the official UCI CSV when it is absent from the repository. The local ZIP includes the CSV so it can also run without downloading it again.

