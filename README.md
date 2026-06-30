# AI-Powered-Digital-Evidence-Classifier
AI-powered digital forensics application built with Python, Streamlit, SQLite, and Scikit-learn. Automates evidence classification, metadata extraction, MD5/SHA256 hashing, risk assessment, PDF report generation, dashboard analytics, and investigation history management.
# 🛡️ AI Powered Digital Evidence Classifier

## 📌 Overview

AI Powered Digital Evidence Classifier is a Digital Forensics application developed using **Python, Streamlit, SQLite, and Scikit-learn**. The application automates the forensic analysis of digital evidence by extracting metadata, generating cryptographic hashes, classifying evidence using a Machine Learning model, assessing risk levels, and generating investigation reports.

The project is designed to assist digital forensic investigators in reducing evidence triage time while improving the efficiency of digital investigations.

---

# 🎯 Project Objectives

- Automate digital evidence analysis.
- Generate forensic hashes (MD5 & SHA256).
- Extract metadata from uploaded files.
- Classify digital evidence using Machine Learning.
- Assess evidence risk levels.
- Maintain investigation history.
- Generate downloadable forensic reports.
- Visualize investigation statistics using dashboards.

---

# ✨ Features

- 📂 Upload Digital Evidence
- 🔐 MD5 Hash Generation
- 🔐 SHA256 Hash Generation
- 📋 Metadata Extraction using ExifTool
- 🤖 AI-Based Evidence Classification
- ⚠️ Risk Level Assessment
- 🖼️ Image Preview
- 📄 PDF Report Generation
- 💾 SQLite Investigation Database
- 📊 Dashboard Analytics
- 📈 Pie Chart & Bar Chart Visualization
- 🔍 Search Investigation History
- 📥 Export Investigation Records (CSV)
- 📜 Chain of Custody
- 🔑 Login Authentication
- 📅 Investigation Timeline

---

# 🛠️ Technologies Used

| Technology | Purpose |
|------------|---------|
| Python | Backend Development |
| Streamlit | Web Interface |
| Scikit-learn | Machine Learning |
| Pandas | Data Processing |
| SQLite | Database |
| Matplotlib | Data Visualization |
| ReportLab | PDF Report Generation |
| Pillow | Image Processing |
| ExifTool | Metadata Extraction |
| Joblib | Model Loading |

---

# 📂 Project Structure

```
AI-Powered-Digital-Evidence-Classifier/
│
├── app.py
├── README.md
├── requirements.txt
├── database.db
│
├── data/
│   └── evidence_dataset.csv
│
├── models/
│   ├── train_model.py
│   ├── evidence_classifier.pkl
│   └── extension_encoder.pkl
│
├── modules/
│   ├── metadata.py
│   ├── database.py
│   ├── report.py
│   ├── dashboard.py
│   ├── login.py
│   └── chain.py
│
├── reports/
├── uploads/
├── screenshots/
└── assets/
```

---

# ⚙️ Installation

### Clone Repository

```bash
git clone https://github.com/yourusername/AI-Powered-Digital-Evidence-Classifier.git
```

### Open Project

```bash
cd AI-Powered-Digital-Evidence-Classifier
```

### Create Virtual Environment

```bash
python3 -m venv venv
```

### Activate Virtual Environment

Linux

```bash
source venv/bin/activate
```

Windows

```bash
venv\Scripts\activate
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Install ExifTool

Kali Linux

```bash
sudo apt install libimage-exiftool-perl
```

### Run Application

```bash
streamlit run app.py
```

---

# 🚀 Workflow

```
Upload Evidence
        │
        ▼
Generate MD5 & SHA256
        │
        ▼
Extract Metadata
        │
        ▼
AI Evidence Classification
        │
        ▼
Risk Assessment
        │
        ▼
Generate PDF Report
        │
        ▼
Store Investigation History
        │
        ▼
Dashboard Analytics
```

---

# 🤖 Machine Learning

The application uses a **Decision Tree Classifier** trained with Scikit-learn.

Training Features include:

- File Extension
- File Size

Prediction Output:

- Image Evidence
- Document Evidence
- Text Evidence
- Log File
- Network Capture
- Executable
- Archive

---

# 📊 Dashboard

The dashboard provides:

- Total Investigations
- High Risk Cases
- Medium Risk Cases
- Low Risk Cases
- Evidence Category Distribution
- Risk Distribution
- Investigation History
- Search Functionality
- CSV Export

---

# 📄 Report Generation

Each investigation can generate a professional forensic report containing:

- Case ID
- Investigation Date
- Evidence Information
- MD5 Hash
- SHA256 Hash
- Metadata
- AI Classification
- Risk Assessment
- Recommendations

---

# 🔒 Digital Forensics Features

- Metadata Extraction
- Cryptographic Hashing
- Chain of Custody
- Evidence Classification
- Risk Analysis
- Investigation Logging
- Dashboard Monitoring

---

# 📸 Screenshots

Add screenshots of:

- Login Page
- Dashboard
- Upload Screen
- Metadata Extraction
- AI Prediction
- Investigation History
- Dashboard Analytics
- PDF Report

---

# 🔮 Future Enhancements

- Deep Learning Based Image Classification
- OCR Integration
- Malware Detection using YARA
- Memory Forensics
- PCAP Analysis
- Timeline Analysis
- Cloud Database Support
- Multi-user Authentication
- REST API Integration

---

# 👩‍💻 Author

**Santhoshi Manaswini Jai**

Aspiring Cybersecurity & Digital Forensics Professional

---

# 📜 License

This project is licensed under the MIT License.

---

# ⭐ Acknowledgements

- Python Community
- Streamlit
- Scikit-learn
- ExifTool
- ReportLab
- SQLite
