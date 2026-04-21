diff --git a/readme.md b/readme.md
index 65133a9381bd62e67041c4bfd32083691ed1875d..d123246d5ea6b79bdfa284195d11eb79587c1636 100644
--- a/readme.md
+++ b/readme.md
@@ -1,135 +1,213 @@
-# 🚀 Edge AI Inference Verification Framework
+# Edge AI Inference Verification Framework
 
-## 🎯 Overview
+A practical framework for validating that **edge-deployed C++ inference** matches a **Python reference implementation** for ONNX models.
 
-This project implements a complete pipeline to verify consistency between Python-based AI inference and C++ deployment using ONNX Runtime.
-
-It simulates a real-world Edge AI workflow where outputs from a reference implementation (Python) are compared against a production-ready implementation (C++).
+This repository is designed to support model deployment workflows where numerical consistency must be proven before release.
 
 ---
 
-## 🧠 Problem Statement
+## Table of Contents
+- [Overview](#overview)
+- [Why This Project Exists](#why-this-project-exists)
+- [Architecture](#architecture)
+- [Key Capabilities](#key-capabilities)
+- [Technology Stack](#technology-stack)
+- [Suggested Repository Layout](#suggested-repository-layout)
+- [Quick Start](#quick-start)
+- [Verification Methodology](#verification-methodology)
+- [Example Console Output](#example-console-output)
+- [Operational Notes](#operational-notes)
+- [Roadmap](#roadmap)
+- [Contributing](#contributing)
+- [License](#license)
 
-When deploying AI models to edge devices, inference is often rewritten in C++ for performance.
+---
 
-However, ensuring that:
+## Overview
 
-> **C++ inference == Python inference**
+The **Edge AI Inference Verification Framework** provides a repeatable pipeline to:
 
-is critical.
+1. Run model inference in Python and generate a **golden output**.
+2. Run the same model in C++ using ONNX Runtime.
+3. Compare outputs with configurable numerical tolerance.
+4. Produce a clear **PASS/FAIL** verification result.
 
-This project solves that using a verification framework that compares outputs with a defined tolerance.
+This process helps teams catch preprocessing mismatches, tensor ordering issues, precision drift, and runtime integration regressions early.
 
 ---
 
-## 🏗️ System Architecture
+## Why This Project Exists
+
+In production edge systems, models are frequently trained and validated in Python, then deployed in C++ for performance and platform constraints. Even when using the same ONNX model, output differences can occur because of:
 
+- Input preprocessing inconsistencies (resize, normalization, channel order)
+- Data type/precision changes (FP32 vs FP16, quantization effects)
+- Tensor shape or layout mistakes
+- Runtime/provider differences
 
-Python (Golden Output Generator)
-↓
-Saved JSON Output
-↓
-C++ Inference Engine (ONNX Runtime)
-↓
-Verification Engine (Tolerance-based)
-↓
-PASS / FAIL
+This framework standardizes cross-language verification so deployment decisions can be made with confidence.
 
+---
+
+## Architecture
+
+```text
+Python Reference Inference
+        |
+        v
+Golden Output (JSON)
+        |
+        v
+C++ Inference (ONNX Runtime)
+        |
+        v
+Tolerance-Based Comparator
+        |
+        v
+Verification Result (PASS / FAIL)
+```
 
 ---
 
-## ⚙️ Features
+## Key Capabilities
 
-- 🔥 ONNX model inference in C++
-- 🖼️ Image preprocessing using OpenCV
-- 🐍 Golden output generation using Python (NumPy + ONNX Runtime)
-- 📊 JSON-based output comparison
-- ✅ Tolerance-based verification system
-- ⚡ Lightweight and edge-ready pipeline
+- Reference (golden) output generation in Python
+- C++ inference execution for deployment parity checks
+- JSON-based exchange format for deterministic comparisons
+- Tolerance-based numeric validation
+- Lightweight workflow suitable for CI and edge deployment gates
 
 ---
 
-## 🛠️ Tech Stack
+## Technology Stack
 
 - **C++**
-- **ONNX Runtime**
-- **OpenCV**
 - **Python**
+- **ONNX Runtime**
+- **OpenCV** (for image preprocessing)
 - **NumPy**
 - **nlohmann/json**
 
 ---
 
-## 📁 Project Structure
+## Suggested Repository Layout
 
+> Note: adapt paths as needed based on your final implementation.
 
+```text
 edge-ai-inference-verification-framework/
-│
-├── models/ # ONNX model
-├── test_data/ # Input images
-├── golden_outputs/ # Python-generated outputs
+├── models/                  # ONNX model files
+├── test_data/               # Sample inputs (images/tensors)
+├── golden_outputs/          # Python-generated expected outputs
 ├── scripts/
-│ ├── generate_golden.py
-│ └── verify_outputs.py
+│   ├── generate_golden.py   # Creates golden outputs
+│   └── verify_outputs.py    # Optional comparison utility
 ├── src/
-│ └── main.cpp # C++ inference + verification
-├── include/ # headers (json, etc.)
-├── third_party/ # OpenCV, ONNX Runtime
+│   └── main.cpp             # C++ inference + verification runner
+├── include/                 # Headers
+├── third_party/             # External dependencies
 ├── CMakeLists.txt
-└── README.md
-
+└── readme.md
+```
 
 ---
 
-## ▶️ How to Run
+## Quick Start
 
-### 1️⃣ Generate Golden Output (Python)
+### 1) Generate Golden Outputs (Python)
 
 ```bash
 python scripts/generate_golden.py
-2️⃣ Build C++ Project
-mkdir build
+```
+
+### 2) Build the C++ Verifier
+
+```bash
+mkdir -p build
 cd build
 cmake ..
-cmake --build .
-3️⃣ Run Inference + Verification
-.\Debug\edge_verify.exe
-📊 Example Output
-Inference ran successfully!
-
-Comparing first 10 values:
-C++: 2.60741 | Golden: 2.60741 | Diff: 0.000001
-
-✅ VERIFICATION PASSED
-⚠️ Notes
-OpenCV DLLs must be available in PATH or copied into the build folder
-ONNX Runtime DLL must be accessible
-Ensure correct relative paths when running from /build
-💡 Why This Project Matters
-
-This project demonstrates a real industry problem:
-
-Ensuring correctness when moving AI models from research (Python) → deployment (C++ / Edge)
-
-This workflow is widely used in:
-
-Autonomous systems 🚗
-Embedded AI 🤖
-Medical imaging 🏥
-Edge devices 📱
-🚀 Future Improvements
-🔍 Full tensor comparison (not just first values)
-📈 Error metrics (MSE, Max Error)
-📦 Batch testing on multiple images
-⚡ Performance benchmarking (latency, FPS)
-🧪 Unit testing integration
-👨‍💻 Author
-
-Mohammed Khaled
-
-Embedded Systems Engineer
-C++ Developer
-FPGA & AI Enthusiast
-⭐ Support
-
-If you find this project useful, consider giving it a star ⭐ on GitHub!
\ No newline at end of file
+cmake --build . --config Release
+```
+
+### 3) Run Verification
+
+Linux/macOS:
+
+```bash
+./edge_verify
+```
+
+Windows (example):
+
+```powershell
+.\Release\edge_verify.exe
+```
+
+---
+
+## Verification Methodology
+
+Typical comparison flow:
+
+1. Load C++ inference output tensor.
+2. Load Python golden tensor from JSON.
+3. Compare element-wise using absolute and/or relative tolerance.
+4. Report summary metrics and final status.
+
+Recommended metrics to report:
+
+- Max absolute error
+- Mean absolute error
+- Number/ratio of elements above tolerance
+- Optional per-layer diagnostics
+
+---
+
+## Example Console Output
+
+```text
+Inference completed successfully.
+Loaded golden output from golden_outputs/sample.json
+Compared 1000 values
+Max abs diff: 0.000012
+Mean abs diff: 0.000001
+Result: VERIFICATION PASSED
+```
+
+---
+
+## Operational Notes
+
+- Ensure ONNX Runtime and OpenCV binaries are available at runtime.
+- Keep preprocessing logic strictly aligned between Python and C++.
+- Use fixed random seeds and deterministic test assets for reproducibility.
+- Store golden outputs as versioned artifacts when used in CI.
+
+---
+
+## Roadmap
+
+- Full tensor comparison across all model outputs
+- Extended error analytics (MSE, percentile errors)
+- Batch verification over datasets
+- Automated performance benchmarks (latency/FPS)
+- CI integration with threshold-based quality gates
+
+---
+
+## Contributing
+
+Contributions are welcome. For major changes, open an issue first to discuss scope and design.
+
+Suggested contribution flow:
+
+1. Fork the repository
+2. Create a feature branch
+3. Add/update tests and verification assets
+4. Open a pull request with clear validation evidence
+
+---
+
+## License
+
+Add your project license here (for example, MIT, Apache-2.0, or proprietary internal license).
