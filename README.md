# JSR Orbital Launch History (1957–2024)
*A Clean, Deduped, Machine-Ready Dataset of Every Verified Orbital Launch*

**Maintained by:** Dev Verma (`dataninja88`)  
**Source Authority:** Jonathan’s Space Report (JSR)

---

## 📌 Overview

This repository transforms Jonathan McDowell’s Satellite Launch Log (JSR) into a clean, standardized, deduped dataset of every verified orbital launch from 1957 to 2024.

It also powers my **Liftoff Atlas** and **Cosmic Swarm** visualizations created for the **Maven Space Challenge 2025**.

Unlike many public datasets that contain:

- repeated entries  
- mission-level duplication  
- inconsistent agency naming  
- mixed orbital / suborbital records  
- gaps in early-year coverage  

this dataset provides a precise **one-row-per-launch** structure, validated for:

- unique `launch_id`  
- consistent date parsing  
- correct year extraction  
- outcome classification using strict JSR criteria  
- removal of all mission-level duplicates  

Designed for:

- scientific studies  
- aerospace analytics  
- orbital cadence research  
- longitudinal modelling  
- data visualization  
- machine learning pipelines  

---

## 📊 Dataset Summary

- **Total verified orbital launches (1957–2024):** 6,617  

**Outcome breakdown:**

- **Success:** 6,126 (92.6%)  
- **Failure:** 410 (6.2%)  
- **Partial / other:** 81 (1.2%)  

**Structure:**

- **Time span:** 1957–2024  
- **Rows:** 6,617  
- **Columns:** 12  

---

## 📁 Files Included

- `jsr_orbital_launches_1957_2024.csv`  
- `codebook_jsr.md`  
- `jsr_analysis.Rmd`     ← newly added reproducible analysis
- `CITATION.cff`  
- `LICENSE`  

---

## 🧬 Data Dictionary (Codebook)

> Full details are in `codebook_jsr.md`. Core fields:

| Column         | Type      | Description                                         |
|----------------|-----------|-----------------------------------------------------|
| `launch_id`    | character | Unique identifier for each launch event             |
| `launch_date`  | datetime  | Parsed launch timestamp                             |
| `year`         | integer   | Launch year                                         |
| `rocket`       | character | Booster or launch vehicle                           |
| `agency`       | character | Launch operator                                     |
| `location`     | character | Launch site or pad                                  |
| `success`      | logical   | Mission success flag                                |
| `success_hard` | logical   | Strict JSR-based success flag                       |
| `notes`        | character | Additional context from JSR logs                    |
| `…`            |           | Fields preserved exactly from JSR where relevant    |

---

## 🔬 Methodology (Reproducible)

End-to-end workflow:

1. Imported raw JSR logs using `tidyverse`.  
2. Normalized and cleaned date formats.  
3. Standardized naming for rockets, agencies, and locations.  
4. Removed all mission-level duplicate entries.  
5. Collapsed payload-level rows into unique launch events.  
6. Validated totals against:  
   - official JSR annual counts  
   - manually verified launch totals  
7. Confirmed **duplicate `launch_id` count = 0**.

Result: a canonical **6,617-launch** dataset suitable for research, analytics, and production pipelines.

---

## 📥 Loading the Dataset

### R

```r
library(readr)

df <- read_csv(
  "jsr_orbital_launches_1957_2024.csv",
  show_col_types = FALSE
)
```

🧾 Academic Citation

If you use this dataset, please cite:

Verma, D. (2024). JSR Orbital Launch History (1957–2024):
A Clean, Deduped Dataset of Verified Orbital Launches.
https://github.com/dataninja88/jsr-orbital-launch-history-1957-2024

Source data: Jonathan McDowell’s Satellite Launch Log (JSR)
License: CC BY 4.0

## 📜 License

This dataset is released under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** license.

You are free to share and adapt the data with proper credit.

Full license text:  
See the `LICENSE` file in this repository.  
https://creativecommons.org/licenses/by/4.0/


🙏 Acknowledgements

Jonathan McDowell, for maintaining JSR, widely regarded as a gold standard for launch verification

NASA, ESA, ISRO, Roscosmos, CNSA, SpaceX

The wider space analytics community for cross-checking annual totals

🛰 Maintained By

Dev Verma
Data Analyst · R Programmer · Aviation & Space Data Enthusiast

📧 dev.dataanalyst8@gmail.com
🌐 GitHub: @dataninja88
