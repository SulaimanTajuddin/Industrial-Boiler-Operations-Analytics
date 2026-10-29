# Industrial Boiler Operations Analytics

Exploratory analysis and anomaly screening for timestamped industrial boiler sensor data.

## Repository contents

| File | Description |
| --- | --- |
| `columns.csv` | Sensor catalog with variant identifiers and process measurement labels. |
| `data.csv` | Timestamped boiler measurements. |
| `data_AutoReg.csv` | Second timestamped measurement dataset used for comparison. |
| `EDA.ipynb` | Exploratory data analysis of data quality, time coverage, distributions, trends, correlations, and differences between the datasets. |
| `anomaly detection.ipynb` | Candidate anomaly screening, visual inspection, and comparison of detection results across both datasets. |
| `41597_2025_5096_Fig3_HTML.png` | Supporting figure included with the project. |

## Analysis notebooks

Open the notebooks from the repository root in Jupyter or Visual Studio Code and select a Python kernel. Both notebooks load the CSV files using repository-relative paths.

### Exploratory data analysis

`EDA.ipynb`:

- Inspects dataset dimensions, schema, and sensor metadata.
- Checks missing values, duplicate records and timestamps, timestamp parsing, chronological order, and sampling intervals.
- Summarizes numeric measurements and compares common sensors on matched timestamps.
- Visualizes missingness, measurement distributions, time series, correlations, and daily averages.

### Anomaly detection

`anomaly detection.ipynb`:

- Uses the sensor catalog and the EDA notebook's data-quality context.
- Screens both datasets using global robust outlier scores, local rolling deviations, and multivariate Isolation Forest.
- Summarizes flagged measurements and periods, plots candidate readings, and compares flags and sensor values across matched timestamps.
- Uses the catalog's `Attribute name` as a label when the `Description` field is blank.

The anomaly thresholds and Isolation Forest contamination rate are configurable in the notebook. Statistical flags are candidates for review, not validated alarm limits, fault diagnoses, or proof of unsafe operation. Confirm any findings against operating context, sensor calibration, maintenance information, and approved engineering limits.

## Requirements

The notebooks use Python with:

- pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn (anomaly detection notebook)
- Jupyter or Visual Studio Code's Jupyter support

Select an environment where these packages are installed before running the notebook cells.
