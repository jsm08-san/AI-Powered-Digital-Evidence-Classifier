import streamlit as st
import hashlib
import tempfile
import subprocess
import os
import uuid
from datetime import datetime
import pandas as pd
import matplotlib.pyplot as plt
import joblib
from PIL import Image
from modules.report import generate_report
from modules.database import create_database, save_case, get_cases, get_dataframe
from modules.dashboard import show_dashboard

# ----------------------------
# Page Configuration
# ----------------------------

st.set_page_config(
    page_title="AI Powered Digital Evidence Classifier",
    page_icon="🛡️",
    layout="wide"
)
create_database()
# Load AI Model
model = joblib.load("models/evidence_classifier.pkl")
encoder = joblib.load("models/extension_encoder.pkl")

# ---------------- Dashboard ----------------

st.sidebar.title("📊 Dashboard")

df = get_dataframe()
show_dashboard(df)
total_cases = len(df)

high_cases = len(df[df["risk"] == "High"]) if not df.empty else 0
medium_cases = len(df[df["risk"] == "Medium"]) if not df.empty else 0
low_cases = len(df[df["risk"] == "Low"]) if not df.empty else 0

st.sidebar.metric("Total Cases", total_cases)
st.sidebar.metric("High Risk", high_cases)
st.sidebar.metric("Medium Risk", medium_cases)
st.sidebar.metric("Low Risk", low_cases)

# -------------------------------------------

st.title("🛡️ AI Powered Digital Evidence Classifier")
st.write("Upload digital evidence for forensic analysis.")

uploaded_file = st.file_uploader(
    "Upload Digital Evidence",
    type=["jpg","jpeg","png","pdf","txt","docx","log","pcap","exe","zip"]
)

if uploaded_file:

    file_bytes = uploaded_file.read()

    md5_hash = hashlib.md5(file_bytes).hexdigest()
    sha256_hash = hashlib.sha256(file_bytes).hexdigest()

    with tempfile.NamedTemporaryFile(delete=False) as tmp:
        tmp.write(file_bytes)
        temp_path = tmp.name

    # Metadata
    try:
        result = subprocess.run(
            ["exiftool", temp_path],
            capture_output=True,
            text=True
        )
        metadata = result.stdout
    except:
        metadata = "ExifTool not installed."

    # Classification
    extension = os.path.splitext(uploaded_file.name)[1].replace(".", "").lower()

    size = len(file_bytes)

    try:
      encoded_extension = encoder.transform([extension])[0]

      prediction = model.predict([[encoded_extension, size]])[0]

    except ValueError:
      prediction = "Unknown Evidence"

    category = prediction

    if category in ["Executable", "Network Capture", "Log File"]:
risk = "High"
      score = 90

    elif category in ["Document Evidence", "Archive", "Text Evidence"]:
      risk = "Medium"
      score = 60

    else:
      risk = "Low"
      score = 20 
      case_id = "CASE-" + str(uuid.uuid4())[:8].upper()
      date = datetime.now().strftime("%d-%m-%Y %H:%M:%S")

    save_case(
      case_id,
      uploaded_file.name,
      category,
      risk,
      date
    )

    st.success("Evidence Uploaded Successfully")

    # ----------------------------
    # Case Details
    # ----------------------------

    st.header("📁 Investigation Details")

    col1, col2 = st.columns(2)

    with col1:
        st.write("**Case ID:**", case_id)
        st.write("**Investigation Time:**", datetime.now().strftime("%d-%m-%Y %H:%M:%S"))

    with col2:
        st.write("**Evidence Category:**", category)
        st.write("**Risk Level:**", risk)

    # ----------------------------
    # Image Preview
    # ----------------------------

    if extension in [".jpg", ".jpeg", ".png"]:
        image = Image.open(uploaded_file)
        st.header("🖼 Evidence Preview")
        st.image(image, width=400)

    # ----------------------------
    # File Information
    # ----------------------------

    st.header("📄 Evidence Information")

    st.write("**File Name:**", uploaded_file.name)
    st.write("**File Size:**", len(file_bytes), "Bytes")
    st.write("**File Type:**", uploaded_file.type)

    # ----------------------------
    # Hashes
    # ----------------------------

    st.header("🔐 Digital Fingerprints")

    st.write("### MD5")
    st.code(md5_hash)

    st.write("### SHA256")
    st.code(sha256_hash)

    # ----------------------------
    # Metadata
    # ----------------------------

    st.header("📋 Metadata")

    st.text(metadata)

    # ----------------------------
    # AI Classification
    # ----------------------------

    st.header("🤖 AI Analysis")

    st.metric("Evidence Category", category)

    st.metric("Risk Level", risk)

    st.write("### Risk Score")

    st.progress(score / 100)

    st.write(f"**{score}/100**")

    # ----------------------------
    # Recommendation
# ----------------------------

    st.header("📢 Recommendation")

    if risk == "High":
        st.error("Immediate forensic investigation is recommended.")

    elif risk == "Medium":
        st.warning("Manual review is recommended.")

    else:
        st.success("Low-risk evidence detected.")

    os.remove(temp_path)
# --------------------------
# PDF Report
# --------------------------

report_path = "reports/forensic_report.pdf"

if st.button("📄 Generate PDF Report"):

    generate_report(
        uploaded_file.name,
        category,
        risk,
        md5_hash,
        sha256_hash,
        metadata,
        report_path
    )

    st.success("PDF Report Generated Successfully!")

    with open(report_path, "rb") as pdf:

        st.download_button(
            "⬇ Download Report",
            pdf,
            file_name="Forensic_Report.pdf",
            mime="application/pdf"
        )
# ---------------------------------------
# Investigation History
# ---------------------------------------

st.header("📂 Investigation History")
cases = get_cases()

if cases:
    st.dataframe(
        cases,
        use_container_width=True
    )
else:
    st.info("No investigations found.")

# ---------------- Dashboard Analytics ----------------

st.header("📊 Dashboard Analytics")

df = get_dataframe()

if not df.empty:

    col1, col2 = st.columns(2)

    with col1:

        st.subheader("Evidence Categories")

        fig, ax = plt.subplots(figsize=(5,5))

        df["category"].value_counts().plot(
            kind="pie",
            autopct="%1.1f%%",
            ax=ax
        )

        ax.set_ylabel("")

        st.pyplot(fig, width="stretch")

    with col2:

        st.subheader("Risk Levels")

        fig, ax = plt.subplots(figsize=(5,4))

        df["risk"].value_counts().plot(
            kind="bar",
            ax=ax
)

        ax.set_xlabel("Risk")
        ax.set_ylabel("Cases")

        st.pyplot(fig)
# ---------------- Search ----------------

st.header("🔍 Search Investigation")

search = st.text_input("Enter File Name")

if search:

    filtered = df[df["filename"].str.contains(search, case=False)]

    st.dataframe(filtered, use_container_width=True)

# ---------------- Export ----------------

st.header("📥 Export Investigation History")

csv = df.to_csv(index=False).encode("utf-8")

st.download_button(
    "Download CSV",
    csv,
    "investigations.csv",
    "text/csv"
)






