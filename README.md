# Student Mental Health Prediction

A machine learning project that estimates a student's **depression risk** from four simple factors: age, stress level, sleep duration, and academic performance (CGPA). It combines five public student mental-health datasets, trains an ensemble classifier, and provides an interactive widget in Google Colab to try out predictions.

> **Disclaimer:** This is an educational project, **not a medical or diagnostic tool**. If you or someone you know is struggling, please contact a qualified mental health professional or your college counseling service.

---

## Features

- **Multi-dataset pipeline:** loads and standardizes 5 differently structured CSV files into one common format
- **Ensemble model:** soft-voting classifier combining Random Forest and Gradient Boosting
- **Feature importance chart:** interactive Plotly bar chart showing which factors matter most
- **Interactive prediction UI:** sliders for age, stress, sleep, and CGPA built with `ipywidgets`
- **Risk gauge:** Plotly gauge showing risk from 0 to 100%
- **Personalized recommendations:** Low / Medium / High risk suggestions shown in an HTML report
- **Prediction history:** each prediction is stored in a session history list

---

## Datasets

The notebook expects these CSV files (uploaded when you run it):

| File | Notes |
|------|-------|
| `Raw Data.csv` | Survey-style data (anxiety, stress, depression values, CGPA bands) |
| `Student Mental health.csv` | Student mental health survey |
| `MentalHealthSurvey.csv` | Study stress, sleep quality, CGPA, depression |
| `Student Depression Dataset.csv` | Academic pressure, sleep duration, CGPA, depression |
| `mentalhealth_dataset.csv` | Additional mental health records |

After processing, the combined dataset has **30,878 records**.

> Datasets are not included in this repository. Download them from Kaggle (or the original source) and upload them when the notebook asks.

---

## How It Works

1. **Upload:** the user uploads the CSV files in Colab
2. **Load and clean:** each file is detected by its column names, mapped to four common features (`age`, `stress`, `sleep`, `academic_performance`) plus the target `depression`; text categories (such as sleep ranges and CGPA bands) are converted to numbers, and missing values are filled with the median
3. **Preprocess:** features are scaled with `StandardScaler`, then split 80/20 into train and test sets (stratified, `random_state=42`)
4. **Train:** `VotingClassifier` (soft voting) with
   - `RandomForestClassifier` (100 trees)
   - `GradientBoostingClassifier` (100 estimators)
5. **Evaluate:** accuracy on the held-out test set, plus a feature importance chart
6. **Predict:** the user moves the sliders and clicks **Predict Mental Health Status**

### Risk levels

| Predicted probability | Risk level |
|-----------------------|-----------|
| 0.00 to 0.30 | Low |
| 0.30 to 0.70 | Medium |
| Above 0.70 | High |

---

## Results

| Metric | Value |
|--------|-------|
| Test accuracy | **0.71** |

---

## Tech Stack

- **Language:** Python 3
- **Data:** pandas, NumPy
- **ML:** scikit-learn (RandomForest, GradientBoosting, VotingClassifier, StandardScaler)
- **Visualization:** Plotly, Matplotlib, Seaborn
- **Interface:** ipywidgets, IPython display
- **Platform:** Google Colab

---

## How to Run

1. Open `Student_Mental_Health_Prediction.ipynb` in [Google Colab](https://colab.research.google.com/)
2. Run the cell
3. When prompted, upload the 5 dataset CSV files
4. Wait for training to finish and view the accuracy and feature importance chart
5. Use the sliders and click **Predict Mental Health Status**

The notebook uses `google.colab.files`, so it is meant to run in Colab rather than locally.

---

## Limitations

- **Accuracy is moderate (71%):** the model uses only four features, so it misses many factors that affect mental health
- **Mixed data sources:** the datasets use different scales and definitions, which adds noise
  - CGPA is on a 4.0 scale in some files and a 10 scale in others
  - One dataset has no sleep data, so a fixed value (6 hours) is used
  - The depression label is derived differently in each dataset (for example, a score above 15 in one of them)
- **Median imputation:** missing values are filled with the overall median
- **Self-reported data:** survey answers can be subjective
- **Not clinically validated:** predictions should never replace professional assessment

---

## Future Improvements

- Add more features (social support, financial stress, physical activity, and so on)
- Normalize CGPA across datasets to a single scale
- Try other models and tune hyperparameters
- Report precision, recall, F1-score, and a confusion matrix, not just accuracy
- Add cross-validation
- Save the trained model and build a standalone web app (Streamlit or Gradio)

---

## Author

**Tuinkal Sharma**
B.Sc. Computer Science (2026), Dayalbagh Educational Institute, Agra
Aspiring Data Analyst | Interested in Data Analytics and Machine Learning
