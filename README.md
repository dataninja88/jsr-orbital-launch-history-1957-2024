# Liftoff Atlas
Orbital Launch History (1957–2024) | Cleaned, Verified, and Visualised

By Dev Verma

# Overview

Liftoff Atlas is a reproducible space-launch analysis and visual storytelling project built for the Maven Space Challenge 2025.

At its core is a rigorously engineered dataset:

6,617 verified orbital launches

1957–2024, derived from Jonathan’s Space Report (JSR)

Fully deduped, parsed, and site-normalized

Mapped to 51 canonical launch sites through a structured mapping pipeline

# The project includes:

Complete data-engineering workflow in R

Full visual suite: timelines, global atlas, SpaceX trajectory

Cosmic Swarm A and Cosmic Swarm B

High-resolution Maven competition poster

Fully reproducible files stored in clean repository structure

# Repository Structure
```
jsr-orbital-launch-history-1957-2024/
│
├── data/                          
│     ├── jsr_orbital_launches_1957_2024.csv
│     ├── LaunchSites_Final_Geocoded.csv
│     ├── site_alias.csv
│     ├── canon_48.csv
│     └── (reference inputs)
│
├── docs/
│     ├── Liftoff_Atlas_JSR_Data_Engineering_Pipeline_by_DV.Rmd
│     ├── Liftoff_Atlas_JSR_Visuals_by_DV.Rmd
│     ├── Liftoff_Atlas_Maven_Challenge_Poster.png
│     ├── Liftoff_Atlas_Maven_Challenge_Poster.pdf
│     ├── swarm_historical.png                 # Cosmic Swarm A
│     └── swarm_dense_poster_github.png        # Cosmic Swarm B
│
├── R/
│     └── (supporting scripts if added later)
│
├── LICENSE
└── README.md
```

Note:
All visual exports are intentionally stored in /docs for easier viewing directly on GitHub.
No outputs/ directory is required.

# 1. Data Engineering Pipeline

Full step-by-step logic is documented in:

📄 docs/Liftoff_Atlas_JSR_Data_Engineering_Pipeline_by_DV.Rmd

Included steps:

Load raw JSR launch log

Clean & normalize fields (dates, sites, pads, success outcomes)

Remove non-orbital entries

Collapse multi-payload lines into launch-level rows

Apply structured alias → canonical site mapping

Validate 100% mapping resolution

Export final canonical dataset:
data/jsr_unique_launches_1957_2024.csv

This file is the authoritative dataset powering all visuals.

# 2. Visualisation Pipeline

All visuals, timelines, maps, and swarm variants are generated through:

📄 docs/Liftoff_Atlas_JSR_Visuals_by_DV.Rmd
🌐 docs/Liftoff_Atlas_JSR_Visuals_by_DV.html (for direct GitHub viewing)

Includes:

Humanity’s orbital cadence (1957–2024)

Liftoff Atlas (global launch-site bubble map)

SpaceX’s orbital growth (2006–2024)

Cosmic Swarm A | launch-true

Cosmic Swarm B | dense poster variant

PNG files are stored inside /docs.

# 3. Cosmic Swarm Variants
A) Cosmic Swarm A | Launch-True (Analytical)

📸 docs/swarm_historical.png

6,617 points = 6,617 launches

Radius encodes year (1957 → 2024)

Pink nucleus = Plesetsk Cosmodrome

Outer rings = remaining global sites

Used for accurate analysis and storytelling

B) Cosmic Swarm B | Dense Poster Variant (Artistic)

📸 docs/swarm_dense_poster_github.png

Synthesized high-density grain field

Concentric inky halos

Bloom-enhanced pink core

Used only for poster aesthetics

Code included in visuals Rmd for transparency

This preserves a clear boundary between data-honest visualisation and creative rendering.

# 4. Maven Challenge Poster

📸 Stored in /docs:

Liftoff_Atlas_Maven_Challenge_Poster.png

Liftoff_Atlas_Maven_Challenge_Poster.pdf

A final composition combining:

World Atlas

Humanity timeline

SpaceX trajectory

Fully polished Cosmic Swarm

Figma-styled layout

# 5. Reproducibility

Every figure in this repository can be rebuilt by:

Opening the .Rmd files in RStudio

Keeping the data/ folder unchanged

Clicking Knit

Outputs will match the poster exactly.

# 6. Acknowledgements

Jonathan’s Space Report (JSR)

rnaturalearth, ggplot2, ggforce, sf

Maven Analytics for the challenge framework

# 7. Closing Note

Liftoff Atlas became more than a competition entry.
It turned into a complete archival map of humanity’s journey into orbit, built line by line, launch by launch, inside R.

Every ring, dot, and orbit in this project carries a real moment of human ambition.
Rebuilding this dataset taught me precision, patience, and the importance of reproducibility in storytelling.

If you explore or extend this dataset, I’d love to see what you create.

Clear skies,

DV
