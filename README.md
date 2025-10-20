Elder Safe Alert Logic – AI & IoT Simulation Project
Google Colab README

This repository/Colab notebook implements a **Phase‑2 → Phase‑3** pipeline to evaluate indoor environmental safety for older adults using the **SML2010** dataset plus **synthetic extremes**. It reproduces the core tables and figures used in the report and exports clean CSVs for downstream analysis and visualization.

---

## 📦 What this notebook does
1. **Phase‑2: Data integration & labelling**
   - Load `NEW-DATA-1.T15.txt` (space‑delimited; Comedor streams used).
   - Generate `n_extreme = 200` synthetic cases (heat/cold, humidity spikes, high CO₂).
   - Apply public‑health‑informed thresholds to assign `risk_level ∈ {safe, warning, danger}`.
   - Save: `Hybrid_SML2010_with_labels.csv`.

2. **Phase‑2 summaries**
   - Compare **Real vs synthetic** distributions (mean ± SD): Temperature, Humidity, CO₂.
   - Check change in **% Warning + Danger** when synthetic data are added.

3. **Phase‑3: Elder Safe Alert Logic**
   - Auto‑detect all temp/humidity/CO₂ columns and **average** to per‑record streams.
   - Apply elder‑sensitive thresholds to classify `predicted_alert`.
   - Report agreement vs `risk_level` (overall + per‑class accuracy).
   - Save: `Hybrid_SML2010_with_alerts.csv`.

4. **Factor‑level alert bands**
   - Independent bands (Safe / Warning‑only / Danger) per factor.
   - Export: `factor_alert_table_independent.csv`.

5. **Practical case example**
   - One realistic scenario (closed room in summer afternoon) through the alert logic.

---

## 🔧 Colab setup (quick start)

Open in Google Colab and run the cells top‑to‑bottom. If your data are on local disk, use the **Upload** cell; if they are on Drive, use the **Drive mount** cell.

### Option A — Upload the data file directly
1. Download the SML2010 file and ensure it is named: **`NEW-DATA-1.T15.txt`**.
2. In Colab, run the **Upload** cell and select the file when prompted.
   ```python
   from google.colab import files
   uploaded = files.upload()  # choose NEW-DATA-1.T15.txt
   ```

### Option B — Mount Google Drive (if file lives in Drive)
1. Put `NEW-DATA-1.T15.txt` in a known Drive folder.
2. In Colab, run:
   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   # then set path, e.g.:
   data_path = '/content/drive/MyDrive/sml2010/NEW-DATA-1.T15.txt'
   ```
3. Replace the default read path in the notebook:
   ```python
   import pandas as pd
   df = pd.read_csv(data_path, sep=' ')
   ```

### Dependencies
Colab already includes recent versions of Python, NumPy, Pandas, and Matplotlib. If needed, re‑install explicitly:
```python
%pip install -q pandas numpy matplotlib
```

---

## ▶️ How to run (end‑to‑end)
1. **Set data path** (see Upload or Drive options above).
2. Run **Phase‑2** cells:
   - Create synthetic extremes and hybrid dataset.
   - Compute `risk_level` labels.
   - Save `Hybrid_SML2010_with_labels.csv`.
3. Run **Phase‑2 summary** cells:
   - Real vs synthetic mean ± SD table.
   - Risk mix comparison (`% Warning + Danger`).
4. Run **Phase‑3** cells:
   - Auto‑detect/average factor columns.
   - Compute `predicted_alert` and agreement vs `risk_level`.
   - Save `Hybrid_SML2010_with_alerts.csv`.
5. Run **Factor‑level bands** cells:
   - Export `factor_alert_table_independent.csv`.
6. (Optional) Run the **practical case** example cell.

**Outputs are saved to the current working directory** (e.g., `/content` in Colab). Use the **Files** pane or `files.download(...)` to retrieve them.

---

## 📁 Key inputs & outputs

**Input**
- `NEW-DATA-1.T15.txt` — SML2010 raw file (space‑delimited)

**Primary Outputs**
- `Hybrid_SML2010_with_labels.csv` — Phase‑2 hybrid dataset with `risk_level`.
- `Hybrid_SML2010_with_alerts.csv` — Phase‑3 outputs with `predicted_alert`.
- `factor_alert_table_independent.csv` — Factor‑level safe/warn/danger bands.

**Secondary / Display Tables (in‑notebook)**
- Real vs synthetic **mean ± SD** table (Temperature / Humidity / CO₂).
- Risk mix change (**% Warning + Danger**).  
- Per‑class performance table (**Accuracy (%)** and totals).

---

## 🧪 Reproducibility notes
- Synthetic set size is controlled by `n_extreme = 200` with `random_state=42` in sampling to ensure reproducibility.
- Thresholds are defined once and used consistently in Phase‑2 and Phase‑3.
- Phase‑3 averages across all detected factor columns to avoid room‑specific bias.

---

## 🗂️ Suggested repo / notebook structure
```
/ (root or Colab /content)
├── NEW-DATA-1.T15.txt                # input
├── Hybrid_SML2010_with_labels.csv    # Phase‑2 output
├── Hybrid_SML2010_with_alerts.csv    # Phase‑3 output
├── factor_alert_table_independent.csv# factor bands
└── README.md                         # this file
```

---

## 🔗 Mapping to Report & Appendix
- **Report Section (Methods/Results)**: Figures & tables generated from the saved CSVs.
- **Appendix A (Representative Code)**: A.1–A.6 blocks mirror the cells in the notebook:
  - A.1 Hybrid generation & labels
  - A.2 Real vs synthetic (mean ± SD)
  - A.3 Risk mix change
  - A.4 Elder Safe Alert Logic & agreement
  - A.5 Factor‑level bands
  - A.6 Practical case


---

## ❓Troubleshooting
- **`FileNotFoundError`**: Confirm the exact path to `NEW-DATA-1.T15.txt` and the `sep=' '` (space) delimiter.
- **Auto‑detection failed**: If `temp_cols/hum_cols/co2_cols` lists are empty, inspect `df.columns` and adjust filters.
- **CSV encoding/commas**: All outputs are standard UTF‑8 CSVs; open with Excel/Sheets or Pandas.


