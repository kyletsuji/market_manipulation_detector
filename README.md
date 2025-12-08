# Market Manipulation Detector

A data analysis project that detects potential market manipulation in Bitcoin trading by analyzing the correlation between social media sentiment (Twitter) and price movements.

## Overview

This project combines Bitcoin price data with Twitter sentiment analysis to identify anomalous patterns that may indicate market manipulation. It uses statistical methods and machine learning techniques to flag suspicious trading periods where unusual social media activity coincides with price volatility.

## Features

- **Data Integration**: Merges Bitcoin price data with Twitter sentiment scores at minute-level granularity
- **Anomaly Detection**: 
  - Z-score based statistical analysis for volume and sentiment spikes
  - Isolation Forest machine learning algorithm for outlier detection
- **Feature Engineering**: 
  - Rolling window statistics (mean, standard deviation)
  - Z-score calculations for volume and sentiment
  - Price volatility metrics
  - Combined manipulation signals
- **Visualization**: Interactive dashboard showing price movements, sentiment, volume, and detected manipulation signals
- **Signal Strength Scoring**: 0-100 scale indicating the strength of potential manipulation signals

## Project Structure

```
market_manipulation_detector/
├── BTC-2018min.csv          
├── BTC-2018min.txt          
├── BTC_Tweets_Updated.csv   
├── BTC_Tweets_Updated.txt   
├── data_preprocessing.ipynb 
├── requirements.txt      
├── preprocessed_data.csv    
├── manipulation_detection_results.csv 
├── detected_manipulation_events.csv  
├── manipulation_detection_dashboard.png 
├── manipulation_summary_statistics.png 
└── README.md                
```

## Requirements

- Python
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn


## Installation

1. Clone or download this repository
2. Install required packages:

```bash
pip install -r requirements.txt
```

Or install manually:
```bash
pip install pandas numpy scikit-learn matplotlib seaborn jupyter
```

## Usage

1. Open the Jupyter notebook data_preprocessing.ipynb:
```bash
jupyter notebook data_preprocessing.ipynb
```

2. Run all cells sequentially to:
   - Load and preprocess the data

3. Open the Jupyter notebook detection.ipynb:
```bash
jupyter notebook detection.ipynb
```

4. Run all cells sequentially to:
   - Perform feature engineering
   - Detect manipulation signals
   - Generate visualizations
   - **Automatically export results** 

3. **Output files are automatically generated** when you run the notebook:
   - `preprocessed_data.csv`: Cleaned and merged dataset 
   - `manipulation_detection_results.csv`: All results with manipulation signals 
   - `detected_manipulation_events.csv`: **Only the detected manipulation events** 
   - `manipulation_detection_dashboard.png`: Main visualization dashboard 
   - `manipulation_summary_statistics.png`: Summary statistics visualization 
   
   These files will appear in the same directory as the notebook after running all cells.

## Methodology

### Data Preprocessing
- Twitter data is aggregated by minute with average sentiment scores
- Price data is aggregated by minute with closing prices
- Both datasets are merged on minute timestamps

### Feature Engineering
- **Volume Features**: Rolling mean, standard deviation, and Z-scores
- **Sentiment Features**: Rolling mean, standard deviation, and Z-scores
- **Price Features**: Price changes, absolute changes, and volatility
- **Signal Indicators**: Binary flags for volume spikes, sentiment spikes, and combined manipulation signals

### Detection Methods

1. **Z-Score Based Detection**:
   - Flags anomalies when volume or sentiment Z-scores exceed ±2 standard deviations
   - Combined signal requires both volume and sentiment spikes

2. **Isolation Forest**:
   - Unsupervised anomaly detection algorithm
   - Identifies outliers in multi-dimensional feature space
   - Contamination rate set to 10%

3. **Signal Strength Calculation**:
   - Combines volume and sentiment Z-scores
   - Adjusts for price volatility
   - Outputs 0-100 scale for manipulation likelihood

## Results

The analysis processes data at minute-level intervals and identifies periods with:
- Unusual message volume spikes
- Extreme sentiment scores
- Coinciding price volatility
- Combined anomalies detected by multiple methods

Results include:
- Total manipulation signals detected
- Signal strength scores
- Correlation analysis between features
- Top manipulation events ranked by signal strength

## Output Files

The following files are automatically generated when you run the notebook (no manual export needed):

- preprocessed_data.csv: Clean dataset ready for analysis (generated after data preprocessing)
- manipulation_detection_results.csv: Complete results with all features and signals for all time periods (generated at the end of analysis)
- detected_manipulation_events.csv: Filtered file containing only the detected manipulation events - sorted by signal strength (generated automatically)
- manipulation_detection_dashboard.png: Main multi-panel visualization showing:
  - Price and signal strength over time
  - Volume and sentiment trends
  - Z-score anomalies
  - Highlighted manipulation signals
- manipulation_summary_statistics.png: Summary statistics visualization including:
  - Feature correlation heatmap
  - Signal strength distribution
  - Normal vs detected events comparison
  - Top 15 detected events by signal strength
