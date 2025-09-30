# 🌲 Forest Cover Type Prediction Challenge

## 📌 Project Overview
This project was carried out as part of my program at **École Polytechnique** and **HEC Paris**.  
We had **2 days** to build a machine learning model capable of predicting the **forest cover type** of a given 30x30m area based on cartographic variables.  

The task was framed as a **multiclass classification problem** (7 classes).  
Our final model achieved **83% accuracy on the professor’s private test set** and up to **87% validation accuracy** during training.

---

## 🎯 Challenge Description
The goal of the challenge was:

> Predict the forest cover type (a categorical variable) from various cartographic variables.  
> The metric used to evaluate performance is **accuracy** on a hidden test set.

The dataset was provided by the US Forest Service (USFS) and US Geological Survey (USGS).  
It contains **only cartographic features** (no remotely sensed data).  
Forest cover type was determined from USFS Region 2 Resource Information System (RIS) data.

---

## 📊 Data Description
- Each observation corresponds to a **30m x 30m cell** in Roosevelt National Forest (Colorado, USA).  
- The study area covers **four wilderness areas**: Neota, Rawah, Comanche Peak, and Cache la Poudre.  
- Features include:
  - **Elevation**, **Slope**, **Aspect**
  - Distances to hydrology, roadways, fire points
  - Hillshade indices (9am, Noon, 3pm)
  - 4 binary wilderness area indicators
  - 40 binary soil type indicators
- Target: **Forest Cover Type (1–7)**  
  - 1 = Spruce/Fir  
  - 2 = Lodgepole Pine  
  - 3 = Ponderosa Pine  
  - 4 = Cottonwood/Willow  
  - 5 = Aspen  
  - 6 = Douglas-fir  
  - 7 = Krummholz  

---

## ⚙️ Methodology
We used **Python (pandas, numpy, scikit-learn, LightGBM)** to preprocess and model the data.

### 🔑 Key steps:
1. **Feature Engineering**
   - Aspect transformed into sine/cosine
   - Euclidean hydrology distance
   - Road/Fire/Hydro combinations
   - Elevation interactions
   - Hillshade averages and ranges
   - Encoding Soil and Wilderness as categorical variables
2. **Modeling**
   - **LightGBM (LGBMClassifier)** with early stopping
   - Hyperparameters tuned for regularization (num_leaves, min_child_samples, subsample, colsample_bytree, etc.)
   - Used **early stopping** to find optimal iterations
3. **Final Training**
   - Retrained on the **entire dataset** with the best iteration
   - Exported predictions in CSV and ZIP format for submission

---

## 📈 Results
- **Validation Accuracy:** ~87%  
- **Private Test Accuracy (professor’s set):** **83%**  
- **Best iteration (early stopping):** ~2600–3000 rounds  

---

## 📂 Repository Structure
- `train.csv` – training dataset  
- `test-full.csv` – test dataset (no labels)  
- `submission.csv` – final predictions  
- `GBBoost.ipynb` – main notebook with training and evaluation  
- `explorations.ipynb` – exploratory data analysis  

---

## 🚀 How to Run
```bash
pip install -r requirements.txt
python train_and_predict.py
