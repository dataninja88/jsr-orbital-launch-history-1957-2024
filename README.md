# JSR Orbital Launch History (1957–2024)

A Clean, Deduped, Machine-Ready Dataset of Every Verified Orbital Launch

Maintained by: Dev Verma (@dataninja88)
Primary Source: Jonathan McDowell’s Satellite Launch Log (JSR)

# Overview

This repository provides a fully engineered, launch-level dataset of every verified orbital launch from 1957 to 2024, derived directly from Jonathan McDowell’s JSR logs.

The raw JSR export contains:

multiple payload rows per launch

inconsistent naming conventions

mixed orbital/suborbital outcomes

historical formatting variations

numerous mission-level duplicates

This project resolves all of that, delivering a canonical one-row-per-launch structure, validated against both JSR and cross-referenced annual totals.

# The dataset powers:

Liftoff Atlas (global bubble map)

Cosmic Swarm (1 dot = 1 launch)

Humanity Launch Timeline

SpaceX vs Humanity cadence analysis

Launch-site dominance models

Built for:

aerospace analytics

academic research

visualization

longitudinal modeling

machine-learning pipelines

# Dataset Summary
Metric	Value
Total Orbital Launches (1957–2024)	6,617
Time Span	1957 to 2024
Rows	6,617
Columns	12
Source Rows (Raw JSR)	~27,239 payload-level rows
Outcome Breakdown

Success: 6,126 (92.6%)

Failure: 410 (6.2%)

Partial / Other: 81 (1.2%)

#📁 Repository Structure

```
jsr-orbital-launch-history-1957-2024/
├── README.md
├── LICENSE
├── data/
│   ├── jsr_orbital_launches_1957_2024.csv      # canonical 6,617-launch dataset
│   ├── LaunchSites_Final_Geocoded.csv          # 51 validated launch-site coordinates
│   └── launchlog.tsv                           # original JSR raw export (~27k rows)
├── docs/
│   ├── liftoff_jsr_data_engineering.Rmd        # full reproducible ETL pipeline
│   └── liftoff_jsr_visuals.Rmd                 # Atlas + timeline + swarm + SpaceX visuals
└── outputs/                                    # optional exports added by users
```

# File Descriptions
jsr_orbital_launches_1957_2024.csv

Clean, deduped, launch-level dataset. One row = one launch.

LaunchSites_Final_Geocoded.csv

Canonical table of 51 global launch sites, manually validated and geocoded for map-ready use.

launchlog.tsv

# Original Jonathan’s Space Report raw payload-level export (27k rows).

docs/liftoff_jsr_data_engineering.Rmd

Complete R Markdown documenting the entire ETL pipeline:

raw ingestion

date parsing

normalization

orbital filtering

dedupe logic

launch-ID construction

validation

final export

Results in exactly 6,617 unique launches.

docs/liftoff_jsr_visuals.Rmd

# Reproducible visualizations:

Humanity Launch Timeline

Liftoff Atlas (global bubble map)

Cosmic Swarm (one dot per launch)

SpaceX vs Humanity cadence

Launch site dominance charts

# Data Dictionary
```
| Column         | Type      | Description                                      |
|----------------|-----------|--------------------------------------------------|
| `launch_id`    | character | Unique identifier for each launch event         |
| `launch_date`  | datetime  | Parsed launch timestamp                          |
| `year`         | integer   | Launch year                                      |
| `rocket`       | character | Booster or launch vehicle                        |
| `agency`       | character | Launch operator                                  |
| `location`     | character | Launch site or pad                               |
| `success`      | logical   | Mission success flag                             |
| `success_hard` | logical   | Strict JSR-based success flag                    |
| `notes`        | character | Additional context from JSR logs                 |
| `…`            |           | Fields preserved exactly from JSR where relevant |

```

# Methodology (Reproducible)
The full pipeline is documented here:
/docs/liftoff_jsr_data_engineering.Rmd

Summary of the R-based workflow:

Import raw JSR .tsv (payload-level).

Clean column names & standardize structure.

Parse historical date formats (multiple patterns).

Filter to orbital / failure codes (OS, OF, OP, OU).

Normalize text fields (vehicle, agency, site, pad).

Build a stable launch_id
using timestamp + site + pad + vehicle + flight ID.

Collapse payload rows → 1 launch per row.

Validate counts against canonical totals.

Export final 6,617-row dataset.

Every step is transparent, fully reproducible, and tailored to preserve scientific accuracy.

# Loading the Dataset
R
library(readr)

df <- read_csv(
  "data/jsr_orbital_launches_1957_2024.csv",
  show_col_types = FALSE
)

# Citation

If you use this dataset, please cite:

Verma, D. (2024).
JSR Orbital Launch History (1957–2024): A Clean, Deduped Dataset of Verified Orbital Launches.
GitHub: https://github.com/dataninja88/jsr-orbital-launch-history-1957-2024

Source data: Jonathan McDowell’s Satellite Launch Log (JSR)


# License
Full license in LICENSE.

# Acknowledgements

Jonathan McDowell for maintaining JSR, the gold standard for orbital launch records.

Global launch providers (NASA, ESA, CNSA, Roscosmos, ISRO, SpaceX, and more).

The broader aerospace data community for cross-referencing annual totals.

# Maintained By

Dev Verma
Data Analyst · R Programmer · Aviation & Space Data Enthusiast
📧 dev.dataanalyst8@gmail.com

🌐 GitHub: @dataninja88
