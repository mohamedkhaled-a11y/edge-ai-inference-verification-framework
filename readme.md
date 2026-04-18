# 🚀 Edge AI Inference Verification Framework

A C++-based framework to verify consistency between Python and C++ AI inference using ONNX Runtime.

---

## 🎯 Overview

This project simulates a real-world Edge AI deployment scenario where model outputs from a C++ inference engine are validated against Python-generated reference outputs (golden data).

---

## ⚙️ Features

- ONNX model inference in C++
- Image preprocessing using OpenCV
- Golden output generation in Python
- Automated verification (PASS / FAIL)
- Tolerance-based comparison

---

## 🧠 Workflow






---

## 🛠️ Tech Stack

- C++
- ONNX Runtime
- OpenCV
- Python (NumPy)

---

## ▶️ How to Run

### 1. Generate Golden Output

```bash
python scripts/generate_golden.py