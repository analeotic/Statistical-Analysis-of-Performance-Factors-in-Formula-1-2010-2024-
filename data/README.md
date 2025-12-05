# 📁 Data Directory

This directory contains all datasets used in the F1 statistical analysis project.

## Directory Structure

```
data/
├── raw/           # Original, immutable data from Ergast API
├── processed/     # Cleaned and transformed datasets
└── README.md     # This file (data dictionary)
```

## Data Sources

### Primary Source: Ergast Developer API
- **URL**: http://ergast.com/mrd/
- **License**: Attribution required (see website for details)
- **Last Updated**: December 2024
- **Coverage**: 1950-2024 Formula 1 seasons

## Raw Data Files

### 1. races.csv
Contains information about each Grand Prix race.

| Column | Type | Description |
|--------|------|-------------|
| raceId | int | Unique race identifier |
| year | int | Season year |
| round | int | Round number in season |
| circuitId | int | Circuit identifier |
| name | str | Grand Prix name |
| date | date | Race date (YYYY-MM-DD) |
| time | time | Race start time (UTC) |
| url | str | Wikipedia URL |

**Sample Size**: 305 races (2010-2024)

### 2. results.csv
Contains individual driver results for each race.

| Column | Type | Description |
|--------|------|-------------|
| resultId | int | Unique result identifier |
| raceId | int | Foreign key to races |
| driverId | int | Foreign key to drivers |
| constructorId | int | Foreign key to constructors |
| number | int | Car number |
| grid | int | Starting grid position |
| position | str | Final position (or DNF/DSQ) |
| positionText | str | Position as text |
| positionOrder | int | Position for ordering |
| points | float | Championship points earned |
| laps | int | Laps completed |
| time | str | Total race time |
| milliseconds | int | Race time in milliseconds |
| fastestLap | int | Fastest lap number |
| rank | int | Fastest lap rank |
| fastestLapTime | str | Fastest lap time |
| fastestLapSpeed | float | Fastest lap speed (km/h) |
| statusId | int | Status code (finished/DNF/etc) |

**Sample Size**: 6,436 results (2010-2024)

### 3. drivers.csv
Contains driver information and demographics.

| Column | Type | Description |
|--------|------|-------------|
| driverId | int | Unique driver identifier |
| driverRef | str | Driver reference code |
| number | int | Permanent number (if any) |
| code | str | Three-letter code |
| forename | str | First name |
| surname | str | Last name |
| dob | date | Date of birth |
| nationality | str | Nationality |
| url | str | Wikipedia URL |

**Sample Size**: 150+ drivers (active 2010-2024)

### 4. constructors.csv
Contains constructor (team) information.

| Column | Type | Description |
|--------|------|-------------|
| constructorId | int | Unique constructor identifier |
| constructorRef | str | Constructor reference code |
| name | str | Team name |
| nationality | str | Team nationality |
| url | str | Wikipedia URL |

**Sample Size**: 20+ constructors (active 2010-2024)

## Processed Data Files

### f1_modern_cleaned.csv
Main analysis dataset combining all sources, filtered for 2010-2024.

**Features**:
- Original columns from all 4 raw datasets
- Derived variables:
  - `won`: Binary indicator (1st place = 1)
  - `podium`: Binary indicator (top 3 = 1)
  - `points_scored`: Binary indicator (points > 0 = 1)
  - `pole_position`: Binary indicator (grid = 1)
  - `top3_grid`: Binary indicator (grid ≤ 3)
  - `position_change`: Grid - Final position
  - `age_at_race`: Driver age at race time
  - `driver_name`: Full driver name
  - `constructor_name`: Team name

**Sample Size**: 6,436 observations

**Missing Values**:
- `fastestLapSpeed`: ~15% missing (DNF races)
- `milliseconds`: ~5% missing (DNF races)
- Other fields: <1% missing

**Data Quality**:
- ✅ No duplicate records
- ✅ All dates validated
- ✅ Numeric fields cleaned and validated
- ✅ Categorical fields standardized

## Data Processing Pipeline

1. **Load** - Import 4 CSV files from Ergast
2. **Merge** - Join tables on foreign keys (raceId, driverId, constructorId)
3. **Filter** - Select 2010-2024 period (Modern Era)
4. **Clean** - Handle missing values, convert types
5. **Engineer** - Create derived features
6. **Validate** - Check for errors and inconsistencies
7. **Export** - Save as `f1_modern_cleaned.csv`

## Usage Examples

### Python (pandas)
```python
import pandas as pd

# Load raw data
races = pd.read_csv('data/raw/races.csv')
results = pd.read_csv('data/raw/results.csv')
drivers = pd.read_csv('data/raw/drivers.csv')
constructors = pd.read_csv('data/raw/constructors.csv')

# Load processed data
df = pd.read_csv('data/processed/f1_modern_cleaned.csv')
```

### R
```r
library(readr)

# Load processed data
df <- read_csv('data/processed/f1_modern_cleaned.csv')
```

## Data Ethics & Privacy

- ✅ **Public Data**: All data is publicly available from Ergast API
- ✅ **No PII**: No personally identifiable information beyond public figures
- ✅ **Attribution**: Proper credit given to Ergast Developer API
- ✅ **Academic Use**: Used solely for educational/research purposes

## Known Issues & Limitations

1. **Missing Lap Times**: ~15% of races have missing fastest lap data (DNFs)
2. **Historical Changes**: Points systems changed over time (standardized to current system)
3. **Sprint Races**: 2021+ sprint races treated as regular qualifying
4. **Weather Data**: Not included in current dataset
5. **Mechanical Failures**: Status codes exist but not analyzed in detail

## Updates & Versioning

- **v1.0** (Dec 2024): Initial dataset (2010-2024)
- **v1.1** (Future): Add weather data
- **v1.2** (Future): Add track characteristics

## Contact & Support

For questions about the data:
- Ergast API: http://ergast.com/mrd/
- Project Issues: [GitHub Issues](https://github.com/yourusername/f1-analysis/issues)

## References

1. Ergast Developer API. (2024). Formula 1 Race Data. http://ergast.com/mrd/
2. Formula 1 Official Website. https://www.formula1.com/

---
*Last Updated: December 2024*
