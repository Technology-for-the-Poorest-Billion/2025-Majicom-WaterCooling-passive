Author: Oishi 

# Experimental Data & Analysis

This directory contains all files related to the experimental testing of evaporative cooling materials for Majicom's solar-powered water kiosk.

The goal of the experiments was to identify low-cost, energy-efficient materials and fan configurations that maximise water cooling via passive or assisted evaporative methods. Testing was conducted using wrapped 1L bottles under controlled indoor conditions, simulating Tanzanian tap water (~15°C) and different airflow scenarios.

---

## Folder Structure - 
In this folder we have all the experimental methods and findings. For the raw and processed data, this can be found in 'finalassets/experimentaldata' 

- `plots/` – PNG images of final temperature difference graphs for each configuration (fan placement + voltage)
- `experimentalprocessed.csv` – Cleaned data used to generate the plots (normalised ΔT values)
- `experimentalraw.csv/` – Includes full temperature logs from each trial and all readings taken

---

## Experiment Summary

Each test recorded:
- Initial & final water temperature
- Ambient chamber temperature
- ΔT (Temp diff from ambient)
- Fan configuration (Bottom / Top / Side ×2)
- Fan voltage (9V / 12V)
- Material used: Jute, Cotton, Linen, or Control
- Change in weight

---

## Plot Legend

The following graphs are included:
- `botfan9V.png` – Bottom fan @ 9V
- `botfan12V.png` – Bottom fan @ 12V
- `topfan9V.png` – Top fan @ 9V
- `sidefan9V.png` – Side fans ×2 @ 9V
- `sidefan12V.png` – Side fans ×2 @ 12V

---

## How to Reproduce / Use

- All plots are based on the `experimentalprocessed.csv` dataset.
- You can recreate the graphs using Python, Excel, or Jupyter with tools like `pandas` and `matplotlib`.
- Normalisation accounts for varying ambient conditions.

---

## Key Findings (Summary)

- **Best Performance**: Cotton with 12V bottom fan (~6.8°C cooling)
- **Most Efficient Low-Energy Setup**: Jute with 9V bottom fan
- **Top fan placement** was the least effective
- **Dual 12V side fans** offer high performance but diminishing returns on energy

[Find the full results](/final/Experiment/Findings.md)

---

## Authors

Experimentation and analysis by: Oishi, assisted by Timothy.
Part of: 2025 Majicom Cooling Project, University of Cambridge

