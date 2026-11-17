## CHANGELOG

## [0.1.0] 

### Added
- Added the initial cyclone data exploration notebook.
- Loaded and inspected the IBTrACS historical cyclone dataset.
- Examined dataset columns, data types, and missing values.
- Filtered historical records for the North Indian Ocean basin.
- Added a historical cyclone track visualisation.


# Changelog

## [v0.1.1] — Phase 1: Satellite Image Exploration

### Added
- Explored INSAT-3DS infrared satellite imagery from MOSDAC.
- Collected and compared satellite image samples from different dates.
- Examined image dimensions, modes, pixel values, grayscale conversion, and contrast enhancement.
- Saved a processed grayscale satellite image for further exploration.

### Analysis
- Identified a candidate satellite observation from 25 October 2024 for cyclone exploration.
- Explored Cyclone Dana's historical track using IBTrACS data.
- Plotted the cyclone track using latitude and longitude.
- Compared the satellite observation timestamp with the nearest recorded cyclone observation.

### Notes
- Gallery images are used for preliminary visual exploration, not as calibrated scientific training data.
- The satellite image's geographic match with Cyclone Dana remains to be verified.
- No classification or prediction models have been trained in this phase.



## [v0.1.2] — Phase 1: Data Exploration

### Added
- Tested grayscale conversion and contrast enhancement.
- Saved a processed grayscale image and documented image metadata limitations.

### Notes
- Satellite gallery images are for preliminary visual exploration only.
- Geographic verification against the historical cyclone track remains incomplete.
- Scientific satellite data acquisition and model training are deferred to later work.




## [v0.2.0] — Phase 2: HURSAT Dataset Inspection

### Added
- Inspected and extracted metadata from the HURSAT-B1 MEGH dataset (98 observations).
- Inspected and extracted metadata from the HURSAT-B1 CHAPALA dataset (122 observations).
- Saved both cyclone metadata tables as CSV files in `data/processed/`.
- Extracted storm-centre coordinates, wind speed, central pressure, and ARCHER measurements.

### Notes
- A total of 220 cyclone observations have been extracted.
- Raw NetCDF files and processed CSV datasets remain local and are excluded from Git.
- Wind-speed and pressure units still require verification.
- Comparative cyclone analysis and further validation are pending.



## [v0.2.1] — Phase 2: Comparative Cyclone Analysis

### Added
- Compared wind-speed variation between MEGH and CHAPALA.
- Analysed central-pressure variations across both cyclones.
- Visualised and compared cyclone tracks using HURSAT centre coordinates.
- Added starting and ending position markers to cyclone track visualisations.
- Calculated minimum, maximum, and average wind speed and central pressure.
- Validated matching MET-7 and MSG-3 satellite observations.

### Findings
- CHAPALA recorded a maximum wind speed of 112.5 knots.
- MEGH recorded a maximum wind speed of 95.9 knots.
- CHAPALA reached a minimum central pressure of 934.5 mb, compared with MEGH's 952.5 mb.

### Notes
- Comparative analysis uses 110 unique timestamps from 220 original satellite records.
- Original satellite records have been preserved.
- ARCHER score analysis and further validation remain pending.



## [v0.2.2] — Phase 2: ARCHER Score Analysis

### Added
- Extracted and inspected ARCHER Combo Score and Ring Score metadata.
- Calculated derived Spiral Scores using the documented difference between Combo and Ring Scores.
- Generated time-series visualisations for all three ARCHER scores.
- Calculated descriptive statistics for ARCHER measurements.
- Analysed Pearson and Spearman correlations between ARCHER scores, wind speed, and central pressure.
- Compared ARCHER score behaviour between MEGH and CHAPALA.

### Findings
- CHAPALA exhibited a stronger association between Ring Score and intensity measurements than MEGH.
- MEGH recorded a higher average Combo Score and Spiral Score.
- CHAPALA recorded a higher average Ring Score and greater Spiral Score variation.

### Notes
- ARCHER scores are dimensionless storm-centre determination measurements.
- Spiral Score is derived as Combo Score minus Ring Score.
- Correlation findings describe associations within the selected observations and do not establish predictive capability.
- Raw NetCDF files and processed CSV datasets remain excluded from Git.
- Further validation and model development remain pending.




### v0.3.0 —  Phase 2: Dataset Preparation 

**Added**
- Extracted IRWIN, IRWVP, and VSCHN satellite channels from MEGH and CHAPALA HURSAT observations.
- Created training (39), validation (10), and testing (61) dataset splits.
- Verified all 110 extracted images for channel availability and dimensions (301 × 301).
- Generated an image metadata manifest containing storm information, wind speed, central pressure, and ARCHER scores.
- Added provisional cyclone intensity labels based on wind-speed ranges.
- Analysed wind-speed distributions across dataset splits.




### v0.3.1 — Dataset Preparation and Image-Level Labelling (Phase 3)

**Added**
- Extracted IRWIN, IRWVP, and VSCHN satellite channels from HURSAT NetCDF observations.
- Created storm-level training, validation, and testing splits:
  - Training: 39 MEGH observations.
  - Validation: 10 MEGH observations.
  - Testing: 61 CHAPALA observations.
- Converted raw satellite values into physical measurements using channel-specific scale factors and offsets.
- Calculated training-set channel statistics and established 1st–99th percentile normalization limits.
- Applied consistent normalization across all three dataset splits, scaling valid pixel values to [0, 1].
- Preserved missing pixels as NaN during normalization.
- Generated and verified 110 normalized satellite images.
- Combined the three satellite channels into multi-channel images of shape 301 × 301 × 3.
- Generated and verified the stacked image dataset.
- Created an image-to-label mapping containing storm metadata, observation timestamps, geographic coordinates, wind speed, central pressure, and provisional intensity labels.
- Verified image-to-label correspondence across all 110 observations.

**Notes**
- Retained continuous wind-speed measurements alongside provisional intensity categories.
- Used MEGH for training and validation and CHAPALA as an unseen storm-level test set.
- Preserved original extracted satellite data separately from normalized and stacked images.
- Dataset contains observations from only two cyclones; broader generalization requires additional storm datasets.

Current dataset

data/
├── processed/
│   └── cyclone_dataset/
│       ├── train/
│       │   └── MEGH/             # 39 extracted images
│       ├── validation/
│       │   └── MEGH/             # 10 extracted images
│       ├── test/
│       │   └── CHAPALA/          # 61 extracted images
│       ├── normalized/
│       │   ├── train/
│       │   ├── validation/
│       │   └── test/
│       └── stacked/
│           ├── train/
│           ├── validation/
│           ├── test/
│           └── image_labels.csv