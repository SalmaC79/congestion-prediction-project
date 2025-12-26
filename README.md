# 🚦 AI-Based Network Congestion Prediction System

## 📌 Overview
This project presents an **AI-driven system for early network congestion prediction**.  
Unlike traditional TCP congestion control mechanisms (e.g. TCP Reno, TCP CUBIC) that react **after packet loss**, this system **predicts congestion in advance** using machine learning and real-time traffic indicators.

The solution combines:
- **Network-level metrics** (RTT, packet spacing, loss bursts)
- **Temporal feature engineering**
- **LightGBM classification**
- **Real-time visualization interface**

---

## 🎯 Objectives
- Predict **network congestion before severe packet loss occurs**
- Provide a **continuous congestion severity score**
- Compare ML-based prediction with **traditional TCP congestion detection**
- Offer a **real-time monitoring interface** for practical analysis

---

## 🧠 Key Idea
Congestion is a **temporal phenomenon**, not a single-packet event.

Therefore, the model focuses on:
- RTT increase trends
- RTT variability
- Packet inter-arrival time
- Loss burst patterns

This allows **early congestion anticipation**, rather than late reaction.

---

## 📊 Features Used
The model is trained using the following features:

| Feature | Description |
|------|-----------|
| RTT | Round-Trip Time |
| Length | TCP payload size |
| loss | Packet loss indicator (retransmissions / duplicate ACKs) |
| delta_time | Inter-packet arrival time |
| rtt_std_5 | Rolling RTT standard deviation (window = 5) |
| loss_burst_5 | Number of losses in last 5 packets |

---

## 🤖 Machine Learning Model
- **Model:** LightGBM Classifier
- **Classes:**  
  - 0 → No congestion  
  - 1 → Moderate congestion  
  - 2 → High congestion
- **Training Strategy:**
  - TCP-only filtering
  - Feature scaling (StandardScaler)
  - Class imbalance handling (`class_weight='balanced'`)

### 📈 Performance
- ** Accuracy:** 90%
- Strong recall for high congestion events (early warning capability)

---

## 🖥️ Real-Time Monitoring Interface
The project includes a **Tkinter-based GUI** that:
- Captures live TCP traffic using `tshark`
- Extracts features in real time
- Predicts congestion probability
- Displays:
  - A **dynamic congestion gauge**
  - A **historical congestion graph**

The predicted class probabilities are converted into a **continuous congestion score (0–100%)**, allowing smooth visualization and interpretation.

---

## 📂 Project Structure
```

ML-Network-project/
│
├── data/
│   └── final_dataset.csv
│
├── models/
│   ├── lgbm_congestion_model.pkl
│   └── scaler.pkl
│
├── notebooks/
│   ├── prepare_model.ipynb
│   └── interface.ipynb
│
└── README.md

```

---

## ⚙️ Technologies Used
- Python
- Pandas / NumPy
- Scikit-learn
- LightGBM
- Tkinter
- Matplotlib
- Tshark
- Joblib

---

## ⚠️ Notes
- A minor `scikit-learn` version warning may appear when loading the saved model.  
  This does not affect prediction correctness and can be resolved by pinning library versions.

---

## 🚀 Future Improvements
- Replace synthetic fallback data with full live RTT estimation
- Support additional TCP variants comparison
- Export metrics for long-term analysis
- Web-based dashboard (Flask / React)

---

## 👩‍💻 Authors
**Salma Choukrani & Nezha Halla**  
Cybersecurity & Networking Engineering Student  
AI • Networking • Machine Learning

---

## 📜 License
This project is for academic and research purposes.
