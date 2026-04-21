# 🚀 Edge AI Inference Verification Framework

## 🎯 Overview

This project implements a complete pipeline to verify consistency between Python-based AI inference and C++ deployment using ONNX Runtime.

It simulates a real-world Edge AI workflow where outputs from a reference implementation (Python) are compared against a production-ready implementation (C++).

---

## 🧠 Problem Statement

When deploying AI models to edge devices, inference is often rewritten in C++ for performance.

However, ensuring that:

> **C++ inference == Python inference**

is critical.

This project solves that using a verification framework that compares outputs with a defined tolerance.

---

## 🏗️ System Architecture


Python (Golden Output Generator)
↓
Saved JSON Output
↓
C++ Inference Engine (ONNX Runtime)
↓
Verification Engine (Tolerance-based)
↓
PASS / FAIL


---

## ⚙️ Features

- 🔥 ONNX model inference in C++
- 🖼️ Image preprocessing using OpenCV
- 🐍 Golden output generation using Python (NumPy + ONNX Runtime)
- 📊 JSON-based output comparison
- ✅ Tolerance-based verification system
- ⚡ Lightweight and edge-ready pipeline

---

## 🛠️ Tech Stack

- **C++**
- **ONNX Runtime**
- **OpenCV**
- **Python**
- **NumPy**
- **nlohmann/json**

---

## 📁 Project Structure


edge-ai-inference-verification-framework/
│
├── models/ # ONNX model
├── test_data/ # Input images
├── golden_outputs/ # Python-generated outputs
├── scripts/
│ ├── generate_golden.py
│ └── verify_outputs.py
├── src/
│ └── main.cpp # C++ inference + verification
├── include/ # headers (json, etc.)
├── third_party/ # OpenCV, ONNX Runtime
├── CMakeLists.txt
└── README.md


---

## ▶️ How to Run

### 1️⃣ Generate Golden Output (Python)

```bash
python scripts/generate_golden.py
2️⃣ Build C++ Project
mkdir build
cd build
cmake ..
cmake --build .
3️⃣ Run Inference + Verification
.\Debug\edge_verify.exe
📊 Example Output
Inference ran successfully!

Comparing first 10 values:
C++: 2.60741 | Golden: 2.60741 | Diff: 0.000001

✅ VERIFICATION PASSED
⚠️ Notes
OpenCV DLLs must be available in PATH or copied into the build folder
ONNX Runtime DLL must be accessible
Ensure correct relative paths when running from /build
💡 Why This Project Matters

This project demonstrates a real industry problem:

Ensuring correctness when moving AI models from research (Python) → deployment (C++ / Edge)

This workflow is widely used in:

Autonomous systems 🚗
Embedded AI 🤖
Medical imaging 🏥
Edge devices 📱
🚀 Future Improvements
🔍 Full tensor comparison (not just first values)
📈 Error metrics (MSE, Max Error)
📦 Batch testing on multiple images
⚡ Performance benchmarking (latency, FPS)
🧪 Unit testing integration
👨‍💻 Author

Mohammed Khaled

Embedded Systems Engineer
C++ Developer
FPGA & AI Enthusiast
⭐ Support

If you find this project useful, consider giving it a star ⭐ on GitHub!