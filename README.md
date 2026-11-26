## 🎯 Goal
Find customers who are about to cancel, so the business can offer them a discount **before** they leave and save revenue.

## ✨ Features
- 🧹 Data cleaning and missing value handling
- 🛠️ 5 engineered features and scaled numbers
- 🤖 3 models tuned with cross-validation
- 📊 Evaluation with ROC-AUC and Precision-Recall
- 💰 Model chosen by **business profit**, not just accuracy
- 🚀 REST API with automatic docs

## 🧰 Tech Stack
`Python` · `Pandas` · `Scikit-learn` · `FastAPI` · `Uvicorn` · `Pytest`

## 🔄 Workflow
| Step | What we did |
|---|---|
| 1️⃣ Clean | Removed ID, fixed missing values, one-hot encoded categories |
| 2️⃣ Features | `tenure_group`, `avg_monthly_spend`, `num_addon_services`, `charge_delta`, `has_protection` |
| 3️⃣ Scale | Standardized numeric columns |
| 4️⃣ Train | Logistic Regression, Random Forest, Gradient Boosting |
| 5️⃣ Tune | 5-fold cross-validated grid search |
| 6️⃣ Evaluate | ROC-AUC, PR-AUC, precision, recall, F1 |
| 7️⃣ Select | Highest expected retention profit |
| 8️⃣ Deploy | FastAPI service |

## 📈 Results
| Model | ROC-AUC | PR-AUC |
|---|---|---|
| Logistic Regression | 0.839 | 0.641 |
| Random Forest | 0.843 | 0.663 |
| Gradient Boosting ⭐ | 0.841 | 0.650 |

⭐ Gradient Boosting was selected for the highest expected campaign profit.

## ⚙️ How to Run
```bash
python -m pip install -r requirements.txt
python -m src.train
python -m uvicorn app.main:app --reload
```
Then open 👉 `http://127.0.0.1:8000/docs`

## 🔌 API Usage
**`POST /predict`**
```json
{
  "gender": "Female", "SeniorCitizen": 0, "Partner": "Yes", "Dependents": "No",
  "tenure": 5, "PhoneService": "Yes", "MultipleLines": "No",
  "InternetService": "Fiber optic", "OnlineSecurity": "No", "OnlineBackup": "No",
  "DeviceProtection": "No", "TechSupport": "No", "StreamingTV": "Yes",
  "StreamingMovies": "Yes", "Contract": "Month-to-month", "PaperlessBilling": "Yes",
  "PaymentMethod": "Electronic check", "MonthlyCharges": 89.5, "TotalCharges": 440.2
}
```
**Response**
```json
{
  "churn_probability": 0.71,
  "churn_prediction": 1,
  "risk_level": "high",
  "threshold": 0.21,
  "model": "gradient_boosting"
}
```

| Endpoint | Purpose |
|---|---|
| `POST /predict` | Score one customer |
| `POST /predict/batch` | Score many customers |
| `GET /health` | Check the server |
| `GET /model-info` | Model details |

## 📁 Project Structure
```
churn-prediction-api/
├── app/
│   ├── main.py        # FastAPI app
│   └── schemas.py     # Input/output validation
├── src/
│   ├── config.py      # Settings
│   ├── features.py    # Cleaning + feature engineering
│   └── train.py       # Training and evaluation
├── tests/             # API tests
├── data/              # Dataset
├── models/            # Saved model
└── reports/           # Metrics and curves
```

## 👩‍💻 Author
**Siddhi Mhatre**
🔗
