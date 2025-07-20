# 🏏 ODI Live Win Probability Predictor

## 📌 Overview

This project aims to **predict the live win probability** for One Day International (ODI) cricket matches **ball-by-ball** using machine learning models. It processes historical ball-by-ball match data and dynamically updates win probabilities as the match progresses.

---

## 🧠 Problem Statement

To develop a predictive system that calculates **live win probabilities** for both teams during an ongoing ODI match. The model considers match progression, team form, and various engineered features to generate meaningful and timely win predictions.

---

## 📂 Dataset

- **Source:** [CricSheet.org](https://cricsheet.org)
- **Data:** Ball-by-ball JSON files of men’s ODI matches.
- **Processed Format:** Cleaned and transformed into a consolidated CSV file.
- **Features Extracted:**
  - Match ID, inning details, teams, players, ball outcomes, runs, wickets, extras, over number, etc.

Additional engineered features:
- Head-to-head match outcomes
- Last 5 match results for both batting and bowling teams

---

## ⚙️ Data Preprocessing & Feature Engineering

Key steps:
- Removal of non-live features (like final innings score).
- Separation of models for **first** and **second innings** due to differing objectives.
- Feature Engineering:
  - **Wicket Resource Lost (WRL):** Captures the impact of wicket timing and position.
  - **Form Difference (FD):** Weighted metric of recent team performance.
  - **Predicted Remaining Score:** Estimated using k-Nearest Neighbors (kNN) on historical patterns.

---

## 🧪 Models Used

1. **DLS Par Score Method**
   - Calculates par score using Duckworth-Lewis method formulas.
   - Basic heuristic, lowest accuracy among all models.

2. **Basic Logistic Regression**
   - Trained separately for first and second innings using core match features.

3. **Dynamic Logistic Regression**
   - 3311 models trained for each combination of overs remaining and wickets fallen.
   - Highly responsive to current game state.

4. **XGBoost**
   - Gradient boosting decision trees.
   - Most accurate model, leveraging engineered features.
   - Separate models for both innings.

---

## 📊 Model Performance (Accuracy)

| Model                    | 1st Innings | 2nd Innings |
|--------------------------|-------------|--------------|
| DLS Par Score            | 38.34%      | 43.23%       |
| Basic Logistic Regression| 74.57%      | 92.07%       |
| Dynamic Logistic Regression | 77.78%   | 85.60%       |
| XGBoost                  | 77.78%      | 92.43%       |
| **XGBoost + Engineered Features** | **94.45%** | **97.7%** |

---

## 📈 Case Studies

### 1. India vs Australia – ICC World Cup 2023
- XGBoost demonstrated sensitivity to early wickets and adjusted probability accordingly.
- Dynamic regression models showed good adaptability with changing run rates.

### 2. Australia vs Afghanistan
- Showcased the importance of stable run rates and wickets in chasing scenarios.
- XGBoost adapted well to sudden shifts in match momentum.

---

## 🔍 Key Observations

- **XGBoost** with engineered features outperformed all other methods significantly.
- Features like **WRL**, **FD**, and **Predicted Score** contributed heavily to model success.
- The model reacts well to real-time match dynamics such as fall of wickets, run rates, and overs remaining.

---

## 🚀 Future Work

To improve the predictive power of the model, future versions may include:
- Pitch conditions and weather data
- Player ICC rankings
- Bowler-batsman interaction history
- Partnership analytics

---

## 🧩 Tech Stack

- **Language:** Python
- **Libraries:** pandas, numpy, scikit-learn, XGBoost

---
## 📁 Repository Structure

📦 Live-win-predictor-for-ODI-Match/
├── 📁 Model/                 # All scripts and notebooks  
│   └── final_code.ipynb  
│  
├── 📁 Data/                  # Raw or processed datasets (excluded if too large)  
│   └── Compress_files.zip  
│  
├── 📁 Report/                # Presentation and project report files  
│   ├── Report.pdf  
│   └── Presentation.pdf  
│  
├── README.md                # Project overview, setup, usage, etc.  
└── requirements.txt         # Python dependencies  

