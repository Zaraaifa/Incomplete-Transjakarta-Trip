# Studi Analisis Incomplete Journey: Mengoptimalkan Pendapatan dan Validitas Data Operasional TransJakarta

## Overview
This repository contains a Jupyter Notebook analyzing **incomplete journeys** in the Transjakarta public transportation system for April 2023. An *incomplete journey* occurs when a passenger taps in but fails to tap out, leading to missing data and potential revenue loss. The analysis identifies patterns, assesses financial impacts, and proposes strategies to reduce incomplete journeys below the 1.5% Southeast Asia industry standard (2020), supporting Transjakarta’s operational efficiency and Jakarta’s smart city vision.

## Dataset
The dataset (`Transjakarta.csv`) includes **37,900 transaction records** from April 2023, detailing passenger journeys. Key columns:

| Column             | Description                                                  |
|--------------------|--------------------------------------------------------------|
| `transID`          | Unique transaction ID.                                       |
| `payCardBirthDate` | Passenger’s birth year (for age analysis).                   |
| `corridorName`     | Route name (e.g., "Matraman Baru - Ancol").                  |
| `tapInTime`        | Tap-in timestamp.                                           |
| `tapOutTime`       | Tap-out timestamp (missing for incomplete journeys).         |
| `payAmount`        | Fare paid (e.g., 0, 3500, 20000).                           |
| `incomplete_journey`| Boolean flag for incomplete journeys (True/False).          |

**Source**: [Google Drive](https://drive.google.com/drive/folders/1p7f4a2tUP1Ek159BUVA2bFkdQUklOe7h?usp=share_link)

## Objectives
1. Identify factors significantly correlated with incomplete journeys by corridor and time.
2. Detect demographic or behavioral patterns predicting incomplete journeys.
3. Analyze spatial (corridors, stops) and temporal (time, day) characteristics.
4. Recommend strategies to reduce incomplete journeys below 1.5%.

## Methodology
### Data Preprocessing
- **Cleaning**: Handled missing `tapOutTime` values and adjusted data types (e.g., `tapInTime` to datetime).
- **Feature Engineering**:
  - Created `age_group` (<18, 18-25, ..., >55).
  - Derived `trans_type` (TransJakarta, Mikrotrans, Royaltrans) from `payAmount`.
  - Added `hour_category` (e.g., Morning Peak) and `is_weekday`.
  - Mapped `region` (e.g., Jakarta Selatan) using stop coordinates.
- **Validation**: Confirmed no duplicates and addressed outliers per statistical best practices.

### Analysis
- **Statistical Tests**:
  - Chi-square for correlations (age, corridor, transport type, etc.).
  - T-test and Spearman correlation for age impact.
- **EDA**:
  - Crosstabs and visualizations to explore patterns.
  - Calculated incomplete rates (e.g., 3.55% overall).
- **Tools**: Python (`pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy.stats`).

## Dashboard
Hasil dashboard dapat dilihat [di sini](https://lookerstudio.google.com/reporting/eb960d8a-b71c-479e-80ed-d90e2be66b90)

## Key Findings
- **Scale**: 1,344 incomplete journeys (3.55%) caused ~Rp 3,573,250 revenue loss.
- **Significant Factors**:
  - **Age**: Older passengers (>55) have higher rates (4.52%, p=0.002).
  - **Transport Type**: Mikrotrans shows elevated rates (p<0.001).
  - **Corridor**: Hotspots include "Kebayoran Lama - Tanah Abang" (p<0.001).
- **Non-Significant**: Gender, payment method, time, and day type (p>0.05).
- **Spatial**: Concentrated in Jakarta Selatan and stops like Cervino Village.
- **Temporal**: No clear time-based patterns (p=0.446 for hours).
- **Financial**: Many incomplete journeys yield `payAmount=0`.

## Recommendations
1. **Age-Targeted Education**:
   - Install clear tap-in/tap-out guides at stops.
   - Deploy assistants for <18 and >55 passengers during peaks.
   - Add app tutorials for new users.
2. **Transport Type Audit**:
   - Inspect Mikrotrans tap-out devices.
   - Standardize procedures with reminders.
   - Test auto tap-out systems.
3. **Corridor/Stop Upgrades**:
   - Fix devices at top 5-10 stops.
   - Improve signage and access.
   - Add buses to reduce peak crowding.
4. **Monitoring**:
   - Build real-time incomplete journey dashboard.
   - Conduct quarterly statistical reviews.
   - Enable app-based passenger feedback.
5. **Awareness Campaigns**:
   - Run social media campaigns (“Tap-In, Tap-Out!”).
   - Add in-bus tap-out reminders.

## Installation
```bash
# Clone repository
git clone https://github.com/your-username/transjakarta-incomplete-journey.git
```

## Install dependencies
```bash
pip install pandas numpy matplotlib seaborn scipy
```

## Usage
1. Download Transjakarta.csv from the source link.
2. Place it in the project directory.
3. Open Transjakarta_Incomplete_Journey_Analysis.ipynb in Jupyter:
```bash
jupyter notebook Transjakarta_Incomplete_Journey_Analysis.ipynb
```
4. Run all cells to reproduce results.

## Project Structure
├── Transjakarta_Incomplete_Journey_Analysis.ipynb  # Analysis notebook
├── Transjakarta.csv                                # Dataset (external)
├── Dashboard_Transjakarta_Incomplete_Journey       # Visualizations 
└── README.md                                       # Project overview

## Limitations
- Limited temporal pattern analysis due to non-significant time factors.
- Behavioral variables (e.g., frequency) underutilized.
- Incomplete dashboard details (e.g., specific stop names).

## Future Work
- Analyze temporal patterns (e.g., hourly trends).
- Explore behavioral predictors (e.g., new vs. loyal users).
- Simulate recommendation impacts.
- Pilot interventions in high-risk corridors.

## Lisence
For educational use only. Dataset usage complies with Transjakarta’s terms.

## Contact
Open an issue or contact [abdillah.zaraa@gmail.com] for questions.
