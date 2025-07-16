import pandas as pd
import numpy as np
import random
from datetime import datetime, timedelta
from sklearn.ensemble import RandomForestClassifier
from sklearn.preprocessing import LabelEncoder
from sklearn.model_selection import train_test_split
import joblib
from reportlab.lib.pagesizes import A4
from reportlab.pdfgen import canvas

# ------------------ STEP 1: Generate Dummy Logs ------------------
def generate_dummy_logs(num_logs=100):
    users = ['alice', 'bob', 'charlie', 'dave', 'eve']
    actions = ['login', 'logout', 'powershell.exe', 'net use', 'rundll32.exe']
    src_ips = ['192.168.1.' + str(i) for i in range(1, 21)]
    logs = []
    for _ in range(num_logs):
        log = {
            '_time': (datetime.now() - timedelta(minutes=random.randint(0, 1440))).isoformat(),
            'user': random.choice(users),
            'action': random.choice(actions),
            'src_ip': random.choice(src_ips)
        }
        logs.append(log)
    return pd.DataFrame(logs)

# ------------------ STEP 2: Feature Engineering ------------------
def extract_features(df):
    df['_time'] = pd.to_datetime(df['_time'], errors='coerce')
    df['hour'] = df['_time'].dt.hour
    df['is_off_hours'] = df['hour'].apply(lambda x: 1 if x < 6 or x > 22 else 0)
    for col in ['src_ip', 'user', 'action']:
        df[col] = df[col].fillna("unknown")
        le = LabelEncoder()
        df[col] = le.fit_transform(df[col])
    return df[['src_ip', 'user', 'action', 'hour', 'is_off_hours']]

# ------------------ STEP 3: Train Model ------------------
def train_model(df, model_path="rf_model.pkl"):
    df['label'] = np.random.randint(0, 2, size=len(df))  # Simulated labels
    features = extract_features(df)
    X_train, X_test, y_train, y_test = train_test_split(features, df['label'], test_size=0.2)
    model = RandomForestClassifier(n_estimators=100)
    model.fit(X_train, y_train)
    joblib.dump(model, model_path)
    print("[+] Trained model saved as rf_model.pkl")

# ------------------ STEP 4: Predict Anomalies ------------------
def predict_anomalies(df, model_path="rf_model.pkl"):
    model = joblib.load(model_path)
    features = extract_features(df)
    df["threat_label"] = model.predict(features)
    df["anomaly_score"] = model.predict_proba(features)[:, 1]
    return df

# ------------------ STEP 5: MITRE ATT&CK Mapping ------------------
def map_to_mitre(row):
    ttp_list = []
    if row["action"] == "powershell.exe" and row["is_off_hours"]:
        ttp_list.append("T1059.001")  # PowerShell
    if row["hour"] < 5 or row["hour"] > 23:
        ttp_list.append("T1078")  # Valid Accounts
    return ttp_list

def apply_mitre_mapping(df):
    df["mitre_ttps"] = df.apply(map_to_mitre, axis=1)
    return df

# ------------------ STEP 6: Alert Triage ------------------
def prioritize_alerts(df):
    df["risk_score"] = df["anomaly_score"] * (1 + df["is_off_hours"])
    return df.sort_values("risk_score", ascending=False)

# ------------------ STEP 7: Generate PDF Report ------------------
def generate_report(df, report_name="threat_hunting_report.pdf"):
    c = canvas.Canvas(report_name, pagesize=A4)
    width, height = A4
    c.setFont("Helvetica-Bold", 16)
    c.drawString(50, height - 50, "AI-Based Threat Hunting Report")
    c.setFont("Helvetica", 10)
    c.drawString(50, height - 70, f"Generated on: {datetime.now().strftime('%Y-%m-%d %H:%M:%S')}")
    total_logs = len(df)
    total_anomalies = df['threat_label'].sum()
    c.drawString(50, height - 100, f"Total logs scanned: {total_logs}")
    c.drawString(50, height - 115, f"Anomalies Detected: {total_anomalies}")
    c.setFont("Helvetica-Bold", 12)
    c.drawString(50, height - 150, "Top 10 Threats:")
    headers = ["Time", "User", "Action", "IP", "Anomaly Score", "Risk", "MITRE TTPs"]
    y = height - 170
    c.setFont("Helvetica-Bold", 9)
    for i, header in enumerate(headers):
        c.drawString(50 + i * 80, y, header)
    top_df = df[["_time", "user", "action", "src_ip", "anomaly_score", "risk_score", "mitre_ttps"]].head(10)
    c.setFont("Helvetica", 8)
    y -= 15
    for index, row in top_df.iterrows():
        col_data = [
            str(row["_time"].strftime("%H:%M %d-%m")),
            str(row["user"]),
            str(row["action"]),
            str(row["src_ip"]),
            f"{row['anomaly_score']:.2f}",
            f"{row['risk_score']:.2f}",
            ','.join(row["mitre_ttps"]) if isinstance(row["mitre_ttps"], list) else str(row["mitre_ttps"])
        ]
        for i, cell in enumerate(col_data):
            c.drawString(50 + i * 80, y, cell[:15])
        y -= 12
        if y < 50:
            c.showPage()
            y = height - 50
    c.save()
    print(f"[+] Report saved as {report_name}")

# ------------------ STEP 8: Main Execution ------------------
def main():
    print("[*] Generating dummy logs...")
    logs_df = generate_dummy_logs(100)
    
    print("[*] Training model on dummy data...")
    train_model(logs_df)
    
    print("[*] Predicting anomalies...")
    detected_df = predict_anomalies(logs_df)
    
    print("[*] Mapping to MITRE ATT&CK techniques...")
    detected_df = apply_mitre_mapping(detected_df)
    
    print("[*] Prioritizing alerts...")
    alerts_df = prioritize_alerts(detected_df)

    print("\n🔐 Top 10 Detected Threats:")
    print(alerts_df[["_time", "user", "action", "src_ip", "anomaly_score", "mitre_ttps", "risk_score"]].head(10))

    print("[*] Generating detailed PDF report...")
    generate_report(alerts_df)

# Run the app
if __name__ == "__main__":
    main()
