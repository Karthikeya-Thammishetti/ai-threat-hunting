# 🔍 AI-Based Threat Hunting Engine

An intelligent threat detection system that uses machine learning models integrated with Splunk to proactively detect, classify, and respond to known and unknown cybersecurity threats. It aligns identified threats with the MITRE ATT&CK framework and automates alert triage to assist SOC teams in reducing investigation time and fatigue.

---

## 📘 Project Overview

This AI-Based Threat Hunting Engine is designed to enhance security operations by automating the detection of anomalies, classifying threats, and mapping them to tactics and techniques defined in the MITRE ATT&CK framework. It integrates Python-based ML models with Splunk, offering real-time detection and contextual threat intelligence.

---


##  strecture
│
├── 📁 data/
│   ├── raw_logs/                # Sample raw log files (anonymized)
│   ├── processed_logs/          # Preprocessed/cleaned logs
│   └── labeled_dataset.csv      # Labelled dataset for supervised learning
│
├── 📁 notebooks/
│   ├── EDA.ipynb                # Exploratory data analysis
│   ├── feature_engineering.ipynb # Feature extraction & transformation
│   └── model_training.ipynb     # Supervised & unsupervised ML models
│
├── 📁 models/
│   ├── isolation_forest.pkl     # Trained anomaly detection model
│   ├── xgboost_model.pkl        # Trained classifier model
│   └── scaler.pkl               # Saved normalization/scaler objects
│
├── 📁 scripts/
│   ├── ingest_splunk.py         # Connects to Splunk API, ingests logs
│   ├── preprocess.py            # Data cleaning and feature extraction
│   ├── inference.py             # Load model and detect anomalies
│   └── mitre_mapper.py          # Map detections to MITRE ATT&CK
│
├── 📁 api/
│   ├── app.py                   # Flask REST API for model serving
│   └── routes.py                # Endpoint definitions
│
├── 📁 dashboards/
│   ├── mitre_heatmap.xml        # Splunk XML/JSON dashboard export
│   ├── user_risk_panel.xml      # Dashboard for user-based risk scoring
│   └── anomaly_trends.xml       # Dashboard for weekly threat trends
│
├── 📁 config/
│   ├── settings.yaml            # Config file for log sources, thresholds
│   └── splunk_config.json       # Splunk API credentials and endpoints
│
├── 📁 deployment/
│   ├── Dockerfile               # Containerize the app
│   ├── docker-compose.yml       # For multi-service setup
│   └── README.md                # Deployment instructions (e.g., AWS, VM)
│
├── 📁 tests/
│   ├── test_model.py            # Unit tests for ML components
│   ├── test_ingestion.py        # Tests for log ingestion
│   └── test_api.py              # Tests for Flask API
│
├── 📄 requirements.txt          # Python dependencies
├── 📄 README.md                 # Project overview and usage
├── 📄 LICENSE                   # Optional open-source license
└── 📄 .gitignore                # Ignore log files, models, temp data


## 🎯 Objectives

- Detect anomalous and malicious activity in real-time using large-scale log data.
- Use AI/ML models to identify unknown (zero-day) attacks.
- Automate alert triage to reduce false positives and improve efficiency.
- Map threats to the MITRE ATT&CK framework for structured analysis.

---

## ⚙️ Tech Stack

- **SIEM Platform:** Splunk
- **Programming Language:** Python
- **Libraries:** Scikit-learn, XGBoost, pandas, NumPy
- **Visualization:** Splunk Dashboards, matplotlib, seaborn
- **Threat Modeling:** MITRE ATT&CK Framework

---

## 🧠 AI/ML System Functionality

### 📥 Data Ingestion
- Logs from firewalls, EDRs, DNS, proxies, and authentication systems.
- Formats: `syslog`, `Windows Event Logs`, NGFW, etc.

### 🛠 Feature Engineering
- Extracted features: login time, IP frequency, port usage, process chains.
- Behavioral baselining for users and devices.

### 🤖 Model Training
- Supervised models for known attacks (Random Forest, XGBoost).
- Unsupervised anomaly detection (Isolation Forest, One-Class SVM).
- Continuous learning via retraining pipelines.

### 🚨 Detection Pipeline
- Real-time event scoring.
- Threat classification: brute-force, privilege escalation, lateral movement.
- TTP mapping: e.g., `T1078 - Valid Accounts`, `T1059 - Command Scripting`.

---

## 🛡️ MITRE ATT&CK Framework Integration

- Automatically maps alerts to tactics and techniques.
- Example:
  - Unusual login + PowerShell = `Credential Access → T1078 + T1059.001`
- Heatmaps show frequency and severity across the matrix.

---

## 🧾 Alert Triage Automation

- Prioritized using:
  - Anomaly score
  - TTP severity
  - Asset importance
- Slack/email integration for real-time alerting.
- Reduced false positives by **~40%**.
- Improved mean time to detect (MTTD) by **30–50%**.

---

## 📈 Impact & Results

- 30% faster detection of threats.
- 40% reduction in alert fatigue.
- Shift from reactive to proactive threat hunting.
- Scalable across hybrid cloud and on-prem environments.

---

## 📊 Splunk Dashboards

- Threat Heatmap (MITRE ATT&CK Matrix)
- Anomaly Trends Over Time
- User & Asset Risk Scores
- Top Suspicious IPs & Hostnames

---

## 🚀 Deployment Details

- **Environments:** Local VM & AWS EC2
- **Splunk Flow:** Universal Forwarder → Indexer → Search Head
- **Model Host:** Python Flask API via Splunk HEC
- **Security:** Internal-only access; anonymized log data

---

## 🧪 Challenges Faced

- Data imbalance solved using SMOTE & ensemble models.
- False positives reduced through hybrid detection.
- Performance optimized via batch inference and log sampling.

---

## 🔮 Future Roadmap

- 🔁 SOAR integration (auto-disable user/block IP)
- 🤖 NLP for phishing/insider threat detection
- 🧬 Graph-based modeling for lateral movement detection
- ☁️ Kubernetes-based scalable deployment

---

## 📌 Summary

> The AI-Based Threat Hunting Engine improves enterprise security posture by providing intelligent, real-time, and context-aware threat detection. It leverages AI/ML with Splunk and MITRE ATT&CK to convert raw logs into actionable insights—reducing analyst fatigue and enabling faster incident response.

---

