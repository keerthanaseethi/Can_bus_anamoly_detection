---

# 🚗 Real-Time CAN Bus Anomaly Detection System

A real-time intrusion detection system (IDS) for in-vehicle Controller Area Network (CAN) traffic, designed to detect cyberattacks such as DoS, spoofing, and replay attacks using machine learning and statistical feature analysis.

This system combines **time-windowed feature engineering**, **supervised and unsupervised ML models**, and a **live monitoring dashboard** to provide low-latency, deployable automotive security monitoring.

---

## 📌 Motivation

Modern vehicles rely on the CAN protocol for communication between Electronic Control Units (ECUs).
However, CAN was designed **without authentication or encryption**, making it vulnerable to attacks such as:

* Message injection
* Spoofing
* Replay attacks
* Denial-of-Service (DoS) flooding

This project addresses these limitations by learning **normal CAN traffic behavior** and detecting deviations in real time.

---

## 🧠 System Overview

The system operates as a **streaming anomaly detection pipeline**:

1. **Raw CAN frames** are ingested
2. Traffic is segmented into **fixed time windows**
3. Statistical and entropy-based features are extracted
4. ML models classify traffic as **normal or anomalous**
5. Results are visualized via a **real-time dashboard**

---

## 🏗️ Architecture

```
CAN Logs / Stream
        ↓
Preprocessing & Windowing
        ↓
Feature Engineering
(Frequency, Entropy, Statistics)
        ↓
ML Models
(Random Forest | Isolation Forest)
        ↓
Real-Time Dashboard & Alerts
```

---

## 🔍 Feature Engineering

CAN messages are analyzed using **non-overlapping time windows (1s)**.

### Extracted Features

#### Frequency-Based

* Message count per CAN ID
* Message rate (messages/second)

#### Payload Statistics

* Mean byte value
* Variance
* Byte distribution patterns

#### Entropy-Based

* Shannon entropy of payload bytes
* Effective for detecting spoofing and injection attacks

This hybrid feature set allows detection of both **timing-based** and **payload-based** attacks.

---

## 🤖 Machine Learning Models

### 1. Random Forest (Supervised)

* Trained on labeled CAN traffic
* Multi-class classification:

  * Normal
  * DoS
  * Spoofing
  * Replay
* High accuracy for known attack types
* Provides feature importance for interpretability

### 2. Isolation Forest (Unsupervised)

* Trained only on normal traffic
* Detects **previously unseen attack patterns**
* Useful when labeled attack data is limited

Both models are optimized for **low-latency inference**.

---

## ⚡ Real-Time Performance

* **Inference latency:** < 5 ms per time window
* **Throughput:** 400+ windows/second
* **Accuracy:** ~94% attack classification accuracy
* Designed for **edge or gateway-level deployment**

---

## 📊 Web Dashboard

The system includes a real-time monitoring dashboard that provides:

* Live anomaly detection status
* Attack type visualization
* Time-series plots of CAN activity
* Event logs for forensic analysis

The dashboard communicates with the backend via **Socket.IO** for real-time updates.

---

## 🧪 Dataset

The system has been evaluated using publicly available automotive intrusion datasets, including:

* Normal CAN traffic
* DoS attacks
* Spoofing attacks
* Replay attacks

Datasets are preprocessed to ensure:

* Consistent timestamp formats
* Standardized CAN ID representation
* Clean payload parsing

---

## 🚀 Installation

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/your-username/can-bus-anomaly-detection.git
cd can-bus-anomaly-detection
```

### 2️⃣ Create Virtual Environment

```bash
python -m venv venv
source venv/bin/activate      # Linux / macOS
venv\Scripts\activate         # Windows
```

### 3️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```

---

## ▶️ Running the System

### Train Models

```bash
python train_supervised.py
python train_unsupervised.py
```

### Start Backend Server

```bash
python app.py
```

### Open Dashboard

Navigate to:

```
http://localhost:5000
```

---

## 📁 Project Structure

```
can-bus-anomaly-detection/
├── data/                  # CAN datasets
├── features/              # Feature extraction logic
├── models/                # Trained ML models
├── training/              # Model training scripts
├── dashboard/             # Frontend assets
├── app.py                 # Backend server
├── utils.py               # Helper functions
├── requirements.txt
└── README.md
```

---

## 🛡️ Use Cases

* In-vehicle intrusion detection
* Automotive cybersecurity research
* Edge ML for real-time systems
* Security monitoring in connected vehicles
* Dataset benchmarking for CAN IDS research

---

## ⚠️ Limitations

* Performance depends on dataset diversity
* CAN encryption is not addressed (detection-only system)
* Simulated datasets may not capture all real-world noise
* Requires retraining for new vehicle models

---

## 🔮 Future Work

* Deep learning models (LSTM / CNN)
* Online learning for adaptive detection
* ECU-level deployment optimization
* Federated learning across vehicle fleets
* Multi-protocol support (LIN, FlexRay, Ethernet)

---

## 📜 License

This project is licensed under the **MIT License**.

---

## 📬 Contact

For questions, discussions, or collaboration:

**Sujal Dixit**
📧 [sujalrdixit@gmail.com](mailto:sujalrdixit@gmail.com)
🔗 LinkedIn / GitHub (see profile)

---
