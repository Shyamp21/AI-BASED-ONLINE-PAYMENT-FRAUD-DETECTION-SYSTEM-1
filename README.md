# FraudGuard: AI-Based Online Payment Fraud Detection System & Suspicious Account Network Analysis

> **Academic Final-Year Engineering Capstone Project**  
> *Combining Transaction Classification, Account-Network Graph Analysis, Hybrid Prediction, and Explainable AI (CatBoost, XGBoost, GraphSAGE, and SHAP).*

---

## 1. Project Overview

**FraudGuard** is an advanced, multi-tiered payment fraud detection and forensic investigation system. Unlike legacy fraud filters that analyze individual transactions in isolation, FraudGuard combines:
1. **Transaction-Level Gradient Boosting**: High-throughput tabular classifiers (**CatBoost** and **XGBoost**) tuned for severe class imbalance.
2. **Account Network Graph Analysis**: Inductive graph neural networks (**GraphSAGE** via PyTorch Geometric) to map complex transaction topologies, detecting money mule rings, fan-in funnels, and cyclic routing.
3. **Calibrated Hybrid Fusion**: Meta-ensemble model calibrated on validation data that fuses tabular probabilities and network risk into a unified **0 to 100 Risk Score** with uncertainty bounds.
4. **Explainable AI (XAI)**: **SHAP (SHapley Additive exPlanations)** attributing exact dollar impacts and topological flags into human-readable investigative findings.
5. **Modern Security Management UI**: Responsive white and navy-blue fintech dashboard, real-time transaction analyzer with sample pre-fill scenarios, fraud alert ledger, and interactive SVG network graph.

---

## 2. Technology Stack

- **Frontend**: HTML5, CSS3, JavaScript (ES6+), Bootstrap 5, Chart.js, SVG Network Visualizer.
- **Backend**: Python 3.10+, Flask REST API.
- **Machine Learning & Graph Analytics**:
  - `CatBoost` (Categorical Gradient Boosted Trees)
  - `XGBoost` (Regularized Extreme Gradient Boosting)
  - `PyTorch` & `PyTorch Geometric` (2-Layer Inductive GraphSAGE)
  - `Scikit-learn` (Evaluation metrics, isotonic/logistic calibration)
  - `SHAP` (TreeExplainer for local feature attribution)
  - `NetworkX` (Topological graph construction and ego-network extraction)
- **Database**:
  - Primary: MySQL (with complete `schema.sql`)
  - Standalone/Fallback: SQLite (`fraudguard.db` automatic fallback for zero-dependency local runs)
- **Dataset**: PaySim synthetic financial benchmark (`sample_transactions.csv`).

---

## 3. Directory Structure

```text
FraudGuard/
├── app.py                      # Flask Application Factory & Entrypoint
├── config.py                   # Global System Configuration & Risk Thresholds
├── requirements.txt            # Python Dependencies
├── README.md                   # Project Documentation & Execution Guide
├── database/
│   ├── schema.sql              # MySQL DDL Schema Definition
│   └── db_manager.py           # Database Manager with MySQL/SQLite Driver
├── dataset/
│   ├── sample_transactions.csv # PaySim Synthetic Transaction Dataset
│   └── generate_data.py        # Reproducible Dataset Generator
├── models/
│   ├── train_catboost.py       # CatBoost Training & PR-AUC Evaluation
│   ├── train_xgboost.py        # XGBoost Training with Class Weighting
│   ├── train_graphsage.py      # PyTorch Geometric GraphSAGE Trainer
│   ├── hybrid_model.py         # Validation-Calibrated Meta-Ensemble Model
│   ├── train_pipeline.py       # Master End-to-End Model Training Pipeline
│   ├── inference.py            # Unified Multi-Model Inference Pipeline
│   └── saved/                  # Serialized Model Artifacts & Metrics
│       ├── catboost_model.cbm
│       ├── xgboost_model.json
│       ├── graphsage_model.pt
│       ├── account_graph.pkl
│       ├── hybrid_meta.json
│       └── evaluation_metrics.json
├── services/
│   ├── preprocessing.py        # Feature Engineering & Leakage Prevention
│   ├── graph_builder.py        # Temporal Directed Graph Construction
│   ├── explainability.py       # SHAP Attribution & Natural Language Reasoning
│   └── fraud_detection.py      # Orchestration of Prediction, XAI & DB
├── routes/
│   ├── auth_routes.py          # Admin Authentication & Session Management
│   ├── prediction_routes.py    # REST APIs (/predict, /batch-predict, /account-network)
│   └── dashboard_routes.py     # Views & Analytics APIs (/health, /dashboard-stats)
├── templates/
│   ├── base.html               # Master Layout & Sidebar Navigation
│   ├── login.html              # Professional Navy/White Login Screen
│   ├── dashboard.html          # Executive Telemetry & Benchmark Charts
│   ├── analyzer.html           # Real-Time Transaction Analyzer & Ego Graph
│   ├── alerts.html             # Fraud Alerts Ledger
│   └── reports.html            # Comprehensive Evaluation Reports
├── static/
│   ├── css/
│   │   ├── style.css           # Core Fintech Design System
│   │   ├── login.css
│   │   ├── dashboard.css
│   │   └── analyzer.css
│   └── js/
│       ├── dashboard.js        # Chart.js Visualizations
│       ├── analyzer.js         # Interactive Prediction Form Controller
│       └── network.js          # SVG Force/Radial Ego Graph Renderer
├── tests/
│   ├── test_prediction.py      # Preprocessing & ML Unit Tests
│   └── test_api.py             # Flask REST API Integration Tests
└── docs/
    ├── PROJECT_REPORT.md       # Comprehensive Final-Year Project Report
    ├── VIVA_QUESTIONS_AND_ANSWERS.md # Examiner Q&A Guide
    └── SYSTEM_ARCHITECTURE_AND_UML.md # System Architecture & UML Diagrams
```

---

## 4. Windows Installation and Execution

### Step 1: Clone or Navigate to the Project Directory
```powershell
cd C:\Users\yadha\.gemini\antigravity\scratch\FraudGuard
```

### Step 2: Set Up Python Virtual Environment (Optional but Recommended)
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

### Step 3: Install Required Dependencies
```powershell
pip install -r requirements.txt
```

### Step 4: (Optional) Re-train All Models
The repository includes pre-trained model weights in `models/saved/`. To re-train all models from scratch:
```powershell
python models\train_pipeline.py
```

### Step 5: Launch the Application
```powershell
python app.py
```
Open your web browser and navigate to:
```
http://127.0.0.1:5000
```

### Default Login Credentials
- **Username**: `admin`
- **Password**: `Admin@12345`

---

## 5. API Endpoints Reference

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/health` | System health check and model loading status |
| `POST` | `/predict` | Real-time single transaction analysis |
| `POST` | `/batch-predict` | Upload CSV for batch transaction scoring |
| `GET` | `/account-network/<account_id>` | 1-hop ego network for visual forensics |
| `GET` | `/dashboard-stats` | Summary statistics and fraud rates |
| `GET` | `/fraud-alerts` | High-risk alert events ledger |
| `GET` | `/model-metrics` | Precision, recall, F1, PR-AUC, and ROC-AUC |

---

## 6. Academic Disclaimer
This software is an academic engineering prototype developed for research, education, and final-year evaluation using synthetic PaySim transaction records. It is not directly integrated into proprietary banking switches (e.g., NPCI, SWIFT, Google Pay, PhonePe) without authorized institutional gateway agreements.
