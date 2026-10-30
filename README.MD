<div align="center">

# 🎓 Student Exam Performance Predictor

**An end-to-end machine learning web app that predicts a student's Maths score from demographic details and their Reading and Writing scores.**

[![Live Demo](https://img.shields.io/badge/Live%20Demo-Render-46E3B7?style=for-the-badge&logo=render&logoColor=white)](https://mlproject-dxun.onrender.com)

![Python](https://img.shields.io/badge/Python-3.11-3776AB?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.3.2-F7931E?logo=scikitlearn&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-UI-FF4B4B?logo=streamlit&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-API-000000?logo=flask&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-ready-2496ED?logo=docker&logoColor=white)

[Live Demo](https://mlproject-dxun.onrender.com) · [Features](#-features) · [Quick Start](#-quick-start) · [Deployment](#-deployment) · [Project Structure](#-project-structure)

</div>

---

## 📌 Overview

This project takes a student's profile and predicts their **Maths score** using a trained regression model. It covers the full ML workflow: exploration in notebooks, a reusable preprocessing and prediction pipeline in `src/`, serialized model artifacts, and two ready-to-run front ends (Streamlit and Flask), packaged with Docker and deployed on Render.

## 🚀 Live Demo

Try it here: **[mlproject-dxun.onrender.com](https://mlproject-dxun.onrender.com)**

> The app is hosted on Render. If it has been idle, the first load can take a short while to wake up.

## ✨ Features

- **Maths score prediction** from seven student inputs.
- **Two interfaces** over the same prediction pipeline: a Streamlit app and a Flask app with HTML templates.
- **Reusable pipeline**: inputs are wrapped in a `CustomData` class, converted to a DataFrame, preprocessed, and passed to the trained model by `PredictPipeline`.
- **Input validation in the UI**: dropdowns for categorical fields and bounded number inputs (0 to 100) for scores.
- **Error handling**: failed predictions return a readable message instead of crashing the app.
- **Containerized**: ships with a `Dockerfile` for consistent, one-command deployment.

## 🧾 Model Inputs

| Feature | Type | Allowed values |
|---|---|---|
| Gender | Categorical | `male`, `female` |
| Race / Ethnicity | Categorical | `group A` to `group E` |
| Parental level of education | Categorical | `associate's degree`, `bachelor's degree`, `high school`, `master's degree`, `some college`, `some high school` |
| Lunch type | Categorical | `free/reduced`, `standard` |
| Test preparation course | Categorical | `none`, `completed` |
| Reading score | Numeric | 0 to 100 |
| Writing score | Numeric | 0 to 100 |

**Output:** predicted Maths score (a value from 0 to 100, shown to two decimal places in the Streamlit app).

## ⚙️ How It Works

```
User input ─► CustomData ─► DataFrame ─► Preprocessor ─► Trained model ─► Predicted Maths score
 (UI form)                              (preprocessor.pkl)   (model.pkl)
```

1. The user fills in the student details in the Streamlit form (or the Flask page).
2. The values are wrapped in `CustomData` and converted to a single-row pandas DataFrame.
3. `PredictPipeline` loads the saved preprocessor and model from `artifacts/`.
4. The preprocessor transforms the row, the model predicts, and the score is displayed.

## 🛠️ Tech Stack

| Area | Tools |
|---|---|
| Language | Python 3.11 |
| Data and ML | Pandas, NumPy, SciPy, scikit-learn, XGBoost, CatBoost |
| Visualization | Matplotlib, Seaborn |
| Web | Streamlit, Flask |
| Serialization | dill |
| DevOps | Docker, Git and GitHub, Render |

## ⚡ Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/KanhaMishra7/mlproject.git
cd mlproject
```

### 2. Create and activate a virtual environment

```bash
python -m venv venv
```

macOS / Linux:

```bash
source venv/bin/activate
```

Windows (PowerShell):

```powershell
.\venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the app

**Streamlit** (recommended, this is what the live demo uses):

```bash
streamlit run streamlit_app.py
```

Then open <http://localhost:8501>.

**Flask** (alternative interface):

```bash
python app.py
```

Then open <http://localhost:5000> and go to `/predictdata` for the prediction form.

## 🐳 Docker

```bash
docker build -t student-performance-predictor .
docker run -p 8501:8501 student-performance-predictor
```

The container runs the Streamlit app on port `8501`. Open <http://localhost:8501>.

## ☁️ Deployment

The app is deployed on [Render](https://render.com/) as a Streamlit service. To deploy your own copy:

| Setting | Value |
|---|---|
| Build command | `pip install -r requirements.txt` |
| Start command | `streamlit run streamlit_app.py --server.address 0.0.0.0 --server.port $PORT` |

Alternatively, deploy the included `Dockerfile` directly.

## 📂 Project Structure

```
mlproject/
├── app.py                 # Flask app (routes: / and /predictdata)
├── streamlit_app.py       # Streamlit app (main UI)
├── templates/             # HTML templates for the Flask app
├── src/
│   ├── components/        # Data and model-building components
│   ├── pipeline/
│   │   └── predict_pipeline.py   # CustomData and PredictPipeline
│   ├── exception.py       # Custom exception handling
│   ├── logger.py          # Logging setup
│   └── utils.py           # Shared helper functions
├── artifacts/             # Saved model and preprocessor
├── notebook/              # Exploration and model experiments
├── Dockerfile
├── requirements.txt
├── runtime.txt
├── setup.py
└── README.md
```

## 🔭 Future Improvements

- Add model evaluation metrics (R², MAE, RMSE) and a model comparison table to this README.
- Show additional prediction insights, such as which inputs influenced the score most.
- Strengthen input validation and error handling.
- Improve the user interface.
- Add user authentication.

## ⚠️ Disclaimer

The predicted Maths score is an estimate from a machine learning model trained on historical data. It is meant for learning and demonstration, not as a guaranteed academic result or a basis for decisions about any student.

## 👨‍💻 Author

**Krishna Kant**

- LinkedIn: [krishna-kant-08752a369](https://www.linkedin.com/in/krishna-kant-08752a369/)
- GitHub: [KanhaMishra7](https://github.com/KanhaMishra7)

---

<div align="center">

If you found this project useful, consider giving it a ⭐

</div>
