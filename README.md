# Python-Based-Predictive-Traffic-Intelligence-Early-Warning-System
A Python-based project that analyzes traffic patterns, explores environmental factors, and uses machine learning to predict potential traffic congestion and support early warning systems.

## Project overview

The repository contains four Jupyter notebooks organized into a practical workflow:

1. **Traffic data quality and preprocessing** — inspect schema and data types, check missing values and duplicates, derive time-based fields, and calculate baseline KPIs.
2. **Traffic pattern analysis (MySQL + Python)** — SQL aggregations for location, hour, weekday/weekend, road type, and a location-by-hour heat map.
3. **Environmental and cause analysis** — explore relationships between rainfall, visibility, weather, accidents, events, construction, public-transport delays, and traffic measures.
4. **Next-hour congestion prediction** — explore the target distribution and train a Random Forest classifier to predict `target_congestion_next_hour` from selected traffic features.

The included dataset is a 100,000-row CSV supplied with the project. Treat results as exploratory unless the data source and real-world validity are independently established; correlations do not prove causation.

## Repository structure

```text
.
├── data/
│   └── traffic_intelligence_dataset_1lakh.csv
├── notebooks/
│   ├── 01_traffic_data_quality_and_preprocessing.ipynb
│   ├── 02_traffic_pattern_analysis_mysql.ipynb
│   ├── 03_environmental_and_cause_analysis.ipynb
│   └── 04_next_hour_congestion_prediction.ipynb
├── presentation/
│   └── project_presentation.pdf
├── README.md
├── requirements.txt
└── .gitignore
```

## Dataset

The CSV includes timestamp and location fields, road type, weather and environmental measurements, vehicle counts, occupancy, average speed, travel-time index, incident/context indicators, current congestion, and the next-hour congestion target.

File: `data/traffic_intelligence_dataset_1lakh.csv`

## Setup

Python 3.10+ is recommended.

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd Python-Based-Predictive-Traffic-Intelligence-Early-Warning-System
python -m venv .venv
```

Activate the environment:

- **Windows:** `.venv\Scripts\activate`
- **macOS/Linux:** `source .venv/bin/activate`

Install dependencies:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Launch Jupyter:

```bash
jupyter lab
```

Open notebooks in the numbered order. The notebooks expect the CSV to be located in `data/`, so run them from the repository's normal folder structure.

## MySQL notebook setup

Notebook 02 reads from a MySQL table named `traffic` in a database (default: `traffic_intelligence`). Create/import the dataset into that database and table before running the SQL analysis cells. Configure connection settings using environment variables rather than committing credentials:

- `TRAFFIC_DB_USER`
- `TRAFFIC_DB_PASSWORD`
- `TRAFFIC_DB_HOST` (defaults to `localhost`)
- `TRAFFIC_DB_NAME` (defaults to `traffic_intelligence`)

The SQL notebook cannot run until the MySQL server, database, and `traffic` table are configured.

## Model workflow

The prediction notebook uses a stratified train/test split (80/20) and a `RandomForestClassifier` with 100 trees. It reports accuracy, a normalized confusion matrix, and feature importances. Evaluate performance beyond accuracy when classes are imbalanced, and avoid using target-derived or future-leaking features in a production forecasting system. This repository is a learning/prototype project, not a deployed traffic warning service.

## Limitations

- Validate the dataset's provenance, collection method, and representativeness before making real-world claims.
- Notebook outputs can depend on library versions, SQL setup, and execution order.
- Predictions should not be used for operational traffic management without robust validation, monitoring, and safety review.

## Tools and technologies

Python, pandas, NumPy, Matplotlib, Seaborn, Jupyter Notebook, scikit-learn, SQL, SQLAlchemy, MySQL Connector/PyMySQL.

