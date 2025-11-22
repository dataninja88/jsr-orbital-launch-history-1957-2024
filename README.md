# Liftoff Atlas | Humanity’s Orbital Launch History (1957–2024)

By Dev Verma
# Repository: jsr-orbital-launch-history-1957-2024

This repository contains the canonical, reproducible, launch-level dataset of 6,617 verified orbital launches (1957–2024), engineered from Jonathan McDowell’s Satellite Launch Log (JSR). It also hosts the full data-engineering pipeline, validation steps, and all final visualizations used for the 2025 Maven Space Data Challenge.

# Project Summary

Every orbital launch begins as a line of code, a burst of fire, and a database entry.
Together, these events trace humanity’s ascent into orbit.

For the Maven Space Data Challenge 2025, I rebuilt the orbital record from the ground up, cross-validating:

JSR launchlog.tsv (≈27k payload rows)

cleaned + deduped to 6,617 unique orbital launches

timestamp normalization

outcome classification

site canonicalization (51 launch sites)

R-based reproducibility from ingestion → final charts

This repository contains the exact pipeline and all supporting datasets required to regenerate the full project.

# Key Outputs in This Repository

1. Canonical Verified Launch Dataset

✔ data/jsr_unique_launches_1957_2024.csv
→ 6,617 deduped launches
→ 1957–2024
→ Launch-true: one row = one real launch, no estimates

2. Data-Engineering Pipeline

✔ docs/Liftoff Atlas JSR Data Engineering Pipeline by DV.Rmd
→ full cleaning, collapsing, datetime parsing, and validation
→ defines canonical launch_id
→ produces all downstream-ready tables

3. Cosmic Swarm (Two Variants)

Historical (1-dot-per-launch)

Launch-true

6,617 points

Used for analysis, timeline interpretation, decade rings

Dense Poster Variant (with grain)

Adds a procedural grain halo around the launch-true base

Used only for the published poster

Fully documented in the Rmd

4. Liftoff Atlas Poster

✔ docs/Liftoff_Atlas_Maven_Challenge_Poster.png
The full 2025 Maven Space Challenge submission containing:

Cosmic Swarm

Global launch footprint (51 sites)

Humanity’s launch timeline

SpaceX trajectory chart

Rendered in R (ggplot2) and refined in Figma.

# Launch KPIs (1957–2024)

Derived from the canonical JSR dataset.

Total launches: 6,617

Success: 6,126 (92.6%)

Failure: 410 (6.2%)

Partial / Other: 81 (1.2%)

# Cosmic Swarm Variants (A & B)
A) Historical Swarm (Launch-True)

Exactly 6,617 points

One point per verified orbital launch

Decade rings, year-radiating structure

Highlight: Plesetsk nucleus (1,670 launches, 25.2% of dataset)

B) Dense Poster Swarm (Artistic Enhancement)

Built on top of Variant A

Adds an outer grain halo for readability and print contrast

Used in the official challenge poster

Fully documented in the Rmd for transparency

Both variants are included in the upcoming R Markdown:
✔ docs/Liftoff_Atlas_Cosmic_Swarm_Variants.Rmd (to be added)

🌐 Reproducibility

This repository follows a transparent, researcher-friendly structure:
```
jsr-orbital-launch-history-1957-2024/
│
├── data/                ← All required input datasets
├── outputs/             ← Generated plots (swarm, atlas, timelines)
├── docs/                ← Full data-engineering and visualization pipelines
│     ├── Liftoff Atlas JSR Data Engineering Pipeline by DV.Rmd
│     ├── Liftoff_Atlas_Maven_Challenge_Poster.png
│     └── Liftoff_Atlas_Cosmic_Swarm_Variants.Rmd   (upcoming)
├── README.md
└── LICENSE (optional)
```


All code is written in R (tidyverse + ggplot2 + sf + ggforce) and runs on any standard R setup.

Technical Glimpse (R)
```
Load dataset
library(readr)
library(dplyr)

missions <- read_csv(
  "data/jsr_unique_launches_1957_2024.csv",
  show_col_types = FALSE
) |>
  clean_names() |>
  mutate(year = as.integer(year)) |>
  filter(year >= 1957, year <= 2024)
  ```

Launches per year
```
missions |>
  count(year, name = "launches") |>
  ggplot(aes(year, launches)) +
  geom_line(colour = "#FF4DA6", linewidth = 0.9) +
  theme_minimal()
  ```

KPI Snapshot
```
jsr_kpi <- jsr |>
  mutate(
    outcome_group = case_when(
      success_hard == TRUE ~ "Success",
      success_hard == FALSE & success == FALSE ~ "Failure",
      success_hard == FALSE & is.na(success) ~ "Partial / other",
      TRUE ~ "Partial / other"
    )
  ) |>
  count(outcome_group, name = "launches") |>
  mutate(
    total = sum(launches),
    share = paste0(round(100 * launches / total, 1), "%")
  )
  ```

Design & Storytelling

The visual system is inspired by:

David McCandless – clarity, beauty, compression of complexity

Federica Fragapane – soft cosmic geometry and living data patterns

All charts were rendered in R, exported as transparent PNGs, and finalized in Figma.


Maven Space Challenge Poster

This is the exact submission poster combining the Cosmic Swarm, Liftoff Atlas world map, humanity’s launch timeline, and SpaceX cadence chart.

🔗 Links

JSR Dataset (canonical): data/jsr_unique_launches_1957_2024.csv

Full Data Engineering Pipeline: docs/Liftoff Atlas JSR Data Engineering Pipeline by DV.Rmd

Maven Submission Poster: docs/Liftoff_Atlas_Maven_Challenge_Poster.png

Open-source, reproducible, extendable.

“Every launch is a leap; and every leap leaves its trace in data.” — Dev
