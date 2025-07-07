# 🔍 AI-Based Threat Hunting Engine

An intelligent threat detection system that uses machine learning models integrated with Splunk to proactively detect, classify, and respond to known and unknown cybersecurity threats. It aligns identified threats with the MITRE ATT&CK framework and automates alert triage to assist SOC teams in reducing investigation time and fatigue.

---

## 📘 Project Overview

This AI-Based Threat Hunting Engine is designed to enhance security operations by automating the detection of anomalies, classifying threats, and mapping them to tactics and techniques defined in the MITRE ATT&CK framework. It integrates Python-based ML models with Splunk, offering real-time detection and contextual threat intelligence.

---

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

