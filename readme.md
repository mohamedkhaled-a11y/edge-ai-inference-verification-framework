# 🚀 Edge AI Inference Verification Framework

A **C++-based framework** for validating ONNX model inference results against Python-generated golden outputs — built for real-world embedded AI deployment pipelines.

---

## 📌 Overview

This project provides a cross-language verification pipeline that ensures C++ inference results match reference outputs generated in Python. It is designed for engineers who need to validate AI model behavior across different runtime environments before deploying to edge devices.

---

## ✨ Features

- ✅ ONNX Runtime inference in C++
- ✅ OpenCV image preprocessing
- ✅ Python-based golden output generation
- ✅ Tolerance-based output comparison
- ✅ Clean modular project structure
- ✅ Cross-language verification (Python ↔ C++)

---

## 🎯 Use Cases

- Embedded AI engineers validating model deployment
- Verification engineers testing inference consistency
- Edge AI teams ensuring output parity across runtimes
- Model consistency testing across environments

---

## 📁 Project Structure

```
edge-ai-inference-verification-framework/
│
├── models/                   # ONNX model files
├── test_data/                # Input images for inference
├── golden_outputs/           # Python-generated reference outputs
│
├── scripts/
│   ├── generate_golden.py    # Generates golden JSON outputs using Python
│   └── verify_outputs.py     # (Optional) Python-side verification helper
│
├── src/
│   └── main.cpp              # C++ inference engine + verification logic
│
├── include/                  # Header files (e.g., nlohmann/json)
├── third_party/              # OpenCV and ONNX Runtime libraries
│
├── CMakeLists.txt
└── README.md
```

---

## ⚙️ Requirements

| Dependency       | Version      |
|------------------|--------------|
| C++ Standard     | C++17        |
| CMake            | ≥ 3.10       |
| OpenCV           | Any recent   |
| ONNX Runtime     | Any recent   |
| Python           | 3.x          |
| NumPy            | Latest       |

---

## 🚀 Getting Started

### 1️⃣ Generate Golden Output (Python)

Run the Python script to perform inference and save reference outputs as JSON:

```bash
python scripts/generate_golden.py
```

This will create:

```
golden_outputs/image1_output.json
```

---

### 2️⃣ Build the C++ Project

```bash
mkdir build
cd build
cmake ..
cmake --build . --config Release
```

---

### 3️⃣ Run Inference & Verification

```bash
./edge_verify
```

---

## 🔍 Verification Logic

The C++ binary performs the following steps:

1. Loads the input image and runs ONNX inference
2. Reads the corresponding golden output from JSON
3. Compares each output value element-wise with a tolerance:

```
tolerance = 1e-3
```

### ✅ Sample Output

```
C++: 2.60741 | Golden: 2.60741 | Diff: 0.00001
C++: 1.15432 | Golden: 1.15431 | Diff: 0.00001
...
✅ VERIFICATION PASSED
```

If any value exceeds the tolerance threshold, the output will show:

```
❌ VERIFICATION FAILED — diff exceeded tolerance at index N
```

---

## 🧩 Key Technologies

| Technology          | Role                                  |
|---------------------|---------------------------------------|
| C++17               | Core inference and verification logic |
| ONNX Runtime (C++)  | Model inference on the C++ side       |
| OpenCV              | Image loading and preprocessing       |
| Python + NumPy      | Golden output generation              |
| ONNX Runtime (Py)   | Reference inference in Python         |
| nlohmann/json       | JSON serialization/deserialization    |

---

## ⚠️ Notes

- OpenCV parallel backend warnings (TBB/OpenMP not found) are **expected and harmless**
- Ensure you run `./edge_verify` from the `/build` directory, or use **absolute paths** in the config
- Golden outputs must be regenerated if the model or input data changes

---

## 📈 Roadmap

- [ ] Support batch inference
- [ ] Add CI/CD pipeline (GitHub Actions)
- [ ] Add visual diff output for failed verifications
- [ ] Extend support to multiple models
- [ ] Add configurable tolerance levels per layer

---

## 👨‍💻 Author

**Mohamed Khaled**
*Software Engineer — C++ · Computer Vision · AI Inference*

---

## ⭐ Support

If you find this project useful, please give it a **star on GitHub** — it means a lot and helps others discover it!
