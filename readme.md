# 🚀 Edge AI Inference Verification Framework

A C++-based framework for validating ONNX model inference results against Python-generated golden outputs.

This project demonstrates a **real-world verification pipeline** used in embedded AI systems, ensuring that inference results from C++ match reference outputs generated using Python.

---

## 📌 Features

- ✅ ONNX Runtime inference in C++
- ✅ OpenCV image preprocessing
- ✅ Python-based golden output generation
- ✅ Output comparison with tolerance
- ✅ Clean modular project structure
- ✅ Cross-language verification (Python ↔ C++)

---

## 🧠 Use Case

This framework is designed for:

- Embedded AI Engineers
- Verification Engineers
- Edge AI deployment validation
- Model consistency testing across environments

---

## 📁 Project Structure


edge-ai-inference-verification-framework/
│
├── models/ # ONNX model
├── test_data/ # Input images
├── golden_outputs/ # Python-generated outputs
│
├── scripts/
│ ├── generate_golden.py
│ └── verify_outputs.py
│
├── src/
│ └── main.cpp # C++ inference + verification
│
├── include/ # headers (json, etc.)
├── third_party/ # OpenCV, ONNX Runtime
│
├── CMakeLists.txt
└── README.md


---

## ⚙️ Requirements

- C++17
- CMake ≥ 3.10
- OpenCV
- ONNX Runtime
- Python 3.x (for golden generation)

---

## 🧪 Workflow

### 1️⃣ Generate Golden Output (Python)

```bash
python scripts/generate_golden.py

This creates:

golden_outputs/image1_output.json
2️⃣ Build C++ Project
mkdir build
cd build
cmake ..
cmake --build . --config Release
3️⃣ Run Inference + Verification
./edge_verify
🔍 Verification Logic
Runs inference in C++
Loads golden output from JSON
Compares values with tolerance:
tolerance = 1e-3
Output Example:
C++: 2.60741 | Golden: 2.60741 | Diff: 0.00001
...
✅ VERIFICATION PASSED
🧩 Key Technologies
C++
ONNX Runtime
OpenCV
Python (NumPy, ONNX Runtime)
JSON (nlohmann)
⚠️ Notes
OpenCV parallel backend warnings are normal (TBB/OPENMP not found)
Ensure correct paths when running from /build
Use absolute paths if needed
📈 Future Improvements
🔹 Support batch inference
🔹 Add CI pipeline (GitHub Actions)
🔹 Add visualization of differences
🔹 Extend to multiple models
👨‍💻 Author

Mohamed Khaled

Embedded Software Engineer
C++ / Computer Vision / AI Inference
🌟 If you like this project

Give it a ⭐ on GitHub — it helps a lot!