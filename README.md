# 🏎️ Statistical Analysis of Performance Factors in Formula 1 (2010-2024)

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Data Science](https://img.shields.io/badge/Data%20Science-Compliant-orange.svg)]()

> A comprehensive statistical analysis examining the key factors that influence race performance in modern Formula 1 racing (2010-2024), using rigorous data science methodologies.

## 📊 Project Overview

This project investigates the statistical relationships between various factors (grid position, team performance, driver characteristics) and race outcomes in Formula 1. The analysis employs both classical statistics and machine learning techniques, following industry-standard data science practices.

### Research Questions

1. Does pole position significantly increase win probability beyond 50%?
2. Is there a statistical difference in performance between top drivers (Hamilton vs Verstappen)?
3. Do top constructors (Mercedes, Red Bull, Ferrari) perform significantly differently?
4. How strongly does grid position correlate with final race position?
5. Can we predict podium finishes based on starting position?

### Dataset

- **Period**: 2010-2024 (Modern Hybrid Era)
- **Sample Size**: 6,436 race results from 305 races
- **Sources**: Ergast F1 API (races, results, drivers, constructors)
- **Features**: Grid position, final position, points, constructor, driver demographics

## 🎯 Key Findings

| Finding | Statistic | Interpretation |
|---------|-----------|----------------|
| **Grid Position Effect** | r = 0.758, R² = 0.574, p < 0.001 | Grid position explains 57.4% of final position variance |
| **Starting Advantage** | χ² = 2108, V = 0.572, p < 0.001 | Top 3 grid: 60.9% podium rate vs 5.6% for others |
| **Constructor Performance** | F = 16.36, η² = 0.018, p < 0.001 | Mercedes & Red Bull significantly outperform Ferrari |
| **Driver Comparison** | t = 1.32, d = 0.09, p = 0.189 | No statistical difference between Hamilton & Verstappen |
| **Pole Position Win Rate** | z = 0.40, p = 0.344 | 51.1% win rate - not significantly > 50% |
| **Podium Prediction** | AUC = 0.914, Acc = 91.4% | Excellent predictive performance from grid position |

## 🛠️ Technology Stack

### Core Libraries
- **Data Manipulation**: pandas, numpy
- **Statistical Analysis**: scipy, statsmodels
- **Machine Learning**: scikit-learn
- **Visualization**: matplotlib, seaborn

### Data Science Practices
- ✅ Reproducibility (random seed, version control)
- ✅ Data validation and quality checks
- ✅ Statistical assumptions testing
- ✅ Effect size reporting
- ✅ Train-test split and cross-validation
- ✅ Regression diagnostics
- ✅ Comprehensive metrics
- ✅ Professional documentation

## 📁 Project Structure

```
Statistical-Analysis-of-Performance-Factors-in-Formula-1-2010-2024/
│
├── data/
│   ├── raw/                    # Raw CSV files from Ergast API
│   ├── processed/              # Cleaned and processed datasets
│   └── README.md              # Data dictionary and sources
│
├── notebooks/
│   └── F1_Complete_Analysis.ipynb  # Main analysis notebook
│
├── src/                       # Source code (if modularized)
│   ├── data_processing.py    # Data loading and cleaning functions
│   ├── statistical_tests.py  # Hypothesis testing functions
│   ├── modeling.py           # ML model functions
│   └── visualization.py      # Plotting functions
│
├── outputs/
│   ├── figures/              # All visualizations (PNG, 300 DPI)
│   ├── tables/               # Statistical results (CSV)
│   └── reports/              # Final reports (PDF, HTML)
│
├── requirements.txt          # Python dependencies
├── .gitignore               # Git ignore rules
├── LICENSE                  # MIT License
└── README.md               # This file
```

## 🚀 Getting Started

### Prerequisites

- Python 3.8 or higher
- pip or conda package manager

### Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/f1-statistical-analysis.git
cd f1-statistical-analysis
```

2. Create a virtual environment:
```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Launch Jupyter:
```bash
jupyter notebook notebooks/F1_Complete_Analysis.ipynb
```

## 📈 Methodology

### 1. Data Collection & Cleaning
- Loaded 4 datasets (races, results, drivers, constructors)
- Filtered for Modern Era (2010-2024)
- Handled missing values and outliers
- Feature engineering (derived variables)

### 2. Exploratory Data Analysis
- Descriptive statistics (mean, median, SD, IQR)
- Distribution analysis
- Top performers identification
- Temporal trends

### 3. Hypothesis Testing (5 Tests)

#### Test 1: One-Sample Proportion Test
- **Question**: Does pole position give > 50% win rate?
- **Method**: z-test for proportions
- **Result**: No evidence (p = 0.344)

#### Test 2: Independent t-test
- **Question**: Hamilton vs Verstappen performance difference?
- **Method**: Welch's t-test (unequal variances)
- **Result**: No significant difference (p = 0.189)

#### Test 3: One-Way ANOVA
- **Question**: Performance difference among top 3 constructors?
- **Method**: ANOVA + Tukey HSD post-hoc
- **Result**: Significant differences (p < 0.001)

#### Test 4: Chi-Square Test
- **Question**: Association between top 3 grid and podium?
- **Method**: Chi-square test of independence
- **Result**: Strong association (p < 0.001, V = 0.572)

#### Test 5: Correlation Analysis
- **Question**: Grid vs final position correlation?
- **Method**: Pearson correlation
- **Result**: Strong positive correlation (r = 0.758, p < 0.001)

### 4. Regression Modeling (3 Models)

#### Model 1: Simple Linear Regression
- **Target**: Final Position
- **Predictor**: Grid Position
- **Performance**: R² = 0.574, RMSE = 3.48
- **Diagnostics**: All assumptions met

#### Model 2: Multiple Linear Regression
- **Target**: Points
- **Predictors**: Grid + Constructor dummies
- **Performance**: R² = 0.193, VIF < 5
- **Findings**: Mercedes +1.73 pts, Red Bull +1.67 pts vs Ferrari

#### Model 3: Logistic Regression
- **Target**: Podium (binary)
- **Predictor**: Grid Position
- **Performance**: AUC = 0.914, Accuracy = 91.4%
- **Interpretation**: Each grid position back multiplies podium odds by 0.625

### 5. Model Validation
- Train-test split (80/20)
- Stratified sampling (classification)
- 5-fold cross-validation
- Overfitting detection
- Regression diagnostics
- Multicollinearity checks (VIF)

## 📊 Visualizations

The project includes 7 publication-quality figures (300 DPI):

1. **Distribution Plots** - Points, grid, position, position change
2. **Constructor Comparison** - Box plots by team
3. **Yearly Trends** - Total and average points over time
4. **Top Drivers** - Horizontal bar chart
5. **Correlation Heatmap** - Key variable relationships
6. **Simple Regression** - Scatter plot with regression line + residuals
7. **Logistic Regression** - Probability curve + confusion matrix

## 📚 Statistical Techniques

### From TU155 (Statistics)
- Descriptive Statistics
- One-Sample Proportion Test (z-test)
- Independent Samples t-test
- Hypothesis Testing Framework
- Confidence Intervals

### From DSI204 (Data Science)
- One-Way ANOVA with post-hoc tests
- Chi-Square Test of Independence
- Pearson Correlation
- Simple & Multiple Linear Regression
- Logistic Regression
- Cross-Validation
- Model Diagnostics

## 🎓 Academic Context

This project was developed for:
- **TU155**: Statistics for Engineers
- **DSI204**: Data Science and Analytics

The analysis demonstrates:
- ✅ Statistical rigor (assumptions testing, effect sizes)
- ✅ Data science best practices (validation, reproducibility)
- ✅ Professional reporting (documentation, visualizations)
- ✅ Critical thinking (interpretation, limitations)

## 📝 Results & Conclusions

### Main Conclusions

1. **Grid Position is King**: Starting position is the single most important predictor of race outcome, explaining 57% of variance in final position.

2. **Top 3 Grid Advantage**: Starting in the top 3 dramatically increases podium chances (61% vs 6%), representing a 10x improvement.

3. **Team Matters**: Mercedes and Red Bull show statistically significant advantages over Ferrari, though effect sizes are modest (~1.7 points/race).

4. **Driver Parity**: No statistical difference between Hamilton and Verstappen when controlling for other factors, suggesting similar skill levels.

5. **Pole Position Myth**: While pole position is advantageous, the win rate (51%) is not statistically different from 50%, debunking the "guaranteed win" myth.

6. **Predictability**: Race outcomes are highly predictable from grid position alone (91% accuracy for podium prediction).

### Limitations

- Analysis focuses on 2010-2024 era; results may not generalize to earlier F1 eras
- Weather conditions, mechanical failures, and race incidents not accounted for
- Driver and constructor effects confounded (top drivers often in top teams)
- Causal relationships not established (observational study)

### Future Work

- Include weather and track characteristics
- Time-series analysis for performance evolution
- Causal inference methods (propensity score matching)
- Deep learning for race outcome prediction
- Survival analysis for mechanical reliability

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👤 Author

**Your Name**
- GitHub: [@yourusername](https://github.com/yourusername)
- Email: your.email@example.com

## 🙏 Acknowledgments

- [Ergast Developer API](http://ergast.com/mrd/) for F1 data
- TU155 & DSI204 course instructors
- Formula 1 community for domain knowledge

## 📚 References

1. Ergast Developer API. (2024). Formula 1 Race Data. http://ergast.com/mrd/
2. Cohen, J. (1988). Statistical Power Analysis for the Behavioral Sciences (2nd ed.). Routledge.
3. James, G., Witten, D., Hastie, T., & Tibshirani, R. (2013). An Introduction to Statistical Learning. Springer.
4. VanderPlas, J. (2016). Python Data Science Handbook. O'Reilly Media.

---

**Note**: This is an academic project demonstrating statistical analysis and data science methodologies. It is not intended for betting or commercial purposes.

*Last Updated: December 2024*
