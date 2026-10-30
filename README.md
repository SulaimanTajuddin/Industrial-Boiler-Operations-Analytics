# Industrial Boiler Operations Analytics

Exploratory analysis, trend and seasonality checks, anomaly screening, and short-term forecasting for timestamped industrial boiler sensor data.

## Repository contents

| File | Description |
| --- | --- |
| `columns.csv` | Sensor catalog with variant identifiers and process measurement labels. |
| `data.csv` | Timestamped boiler measurements. |
| `data_AutoReg.csv` | Second timestamped measurement dataset used for comparison. |
| `EDA.ipynb` | Exploratory data analysis of data quality, time coverage, distributions, trends, correlations, and differences between the datasets. |
| `seasonality & trend.ipynb` | Descriptive sensor trend, within-day profile, autocorrelation, and seasonal-decomposition eligibility checks across both datasets. |
| `anomaly detection.ipynb` | Candidate anomaly screening, visual inspection, and comparison of detection results across both datasets. |
| `forecasting.ipynb` | Short-term autoregressive forecast for main steam flow, with a chronological holdout comparison against persistence. |
| `41597_2025_5096_Fig3_HTML.png` | Supporting figure included with the project. |

## Analysis notebooks

Open the notebooks from the repository root in Jupyter or Visual Studio Code and select a Python kernel. The notebooks load the CSV files from the repository directory; some locate the root automatically, while others expect to be run with the repository root as the working directory.

### Exploratory data analysis

`EDA.ipynb`:

- Inspects dataset dimensions, schema, and sensor metadata.
- Checks missing values, duplicate records and timestamps, timestamp parsing, chronological order, and sampling intervals.
- Summarizes numeric measurements and compares common sensors on matched timestamps.
- Visualizes missingness, measurement distributions, time series, correlations, and daily averages.

### Seasonality and trend checks

`seasonality & trend.ipynb`:

- Checks timestamp coverage and sampling cadence, then resamples both datasets to minute-level summaries.
- Examines descriptive linear trends, within-day profiles, and short-lag autocorrelation.
- Runs seasonal decomposition only when the available observations support the selected period.

The records span only a few days, so they cannot establish reliable weekly or longer-term seasonality. Results are descriptive, not causal.

### Anomaly detection

`anomaly detection.ipynb`:

- Uses the sensor catalog and the EDA notebook's data-quality context.
- Screens both datasets using global robust outlier scores, local rolling deviations, and multivariate Isolation Forest.
- Summarizes flagged measurements and periods, plots candidate readings, and compares flags and sensor values across matched timestamps.
- Uses the catalog's `Attribute name` as a label when the `Description` field is blank.

The anomaly thresholds and Isolation Forest contamination rate are configurable in the notebook. Statistical flags are candidates for review, not validated alarm limits, fault diagnoses, or proof of unsafe operation. Confirm any findings against operating context, sensor calibration, maintenance information, and approved engineering limits.

### Short-term forecasting

`forecasting.ipynb`:

- Forecasts `ZZQBCHLL.AV_0#` (main steam flow rate after compensation) using one-minute means from `data.csv`.
- Evaluates a recursive autoregressive least-squares model against a persistence baseline on the final held-out hour.
- Produces a 60-minute forecast and an empirical residual band labeled as a heuristic, not a calibrated prediction interval.

The short record does not establish weekly or annual seasonality, causal relationships, safe operating limits, or reliable long-range forecast accuracy. Forecasts are exploratory and must not be used as operating controls or safety decisions.

## Requirements

The notebooks use Python with:

- pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn (anomaly detection notebook)
- statsmodels (optional; enables autocorrelation and STL checks in the seasonality and trend notebook)
- Jupyter or Visual Studio Code's Jupyter support

Select an environment where the required packages are installed before running the notebook cells. The seasonality and trend notebook skips its statsmodels analyses with a warning if statsmodels is unavailable.
