<div align="center">

<img src="./image/Baiji_Team.png" alt="Baiji Team Logo" width="1000" height="500"/>

<br/>

# TurnSense

### 🎯 Lightweight · Accurate · Three-Class — Redefining Speech Turn Detection

<br/>

<center><strong>47M Parameters ｜ English & Chinese Turn Detection ｜ F1 up to 96.35% ｜ Invalid Utterance Filtering</strong></center>

<br/>

[![GitHub](https://img.shields.io/badge/GitHub-brgroup--Team/TurnSense-181717?style=for-the-badge&logo=github)](https://github.com/Bairong-Xdynamics/TurnSense)
[![Hugging Face](https://img.shields.io/badge/🤗_Hugging_Face-brgroup--Team-yellow?style=for-the-badge)](https://huggingface.co/brgroup/TurnSense)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue?style=for-the-badge)](./LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen?style=for-the-badge)](https://github.com/Bairong-Xdynamics/TurnSense)

</div>

<br/>

**Language**: **English** | [中文](./README.md)

<br/>

> **⭐ If TurnSense is useful to you, please give us a Star!** This helps us continue improving the model and documentation.

<br/>

## 📖 Table of Contents

- [News](#-news)
- [Why TurnSense](#-why-turnsense)
- [Introduction](#-introduction)
- [Core Features](#-core-features)
- [Model Size Comparison](#-model-size-comparison)
- [Benchmark Results](#-benchmark-results)
- [Quick Start](#-quick-start)
- [Evaluation Guide](#-evaluation-guide)
- [Citation](#-citation)
- [Questions and Contact](#-questions-and-contact)
- [License](#-license)

<br/>

---

## 📰 News

- **2026.05.22**: **TurnSense 1.1** is released. This version focuses on improving English turn-taking detection, especially the distinction between `complete` and `incomplete` utterances. The model is available on Hugging Face: [brgroup/TurnSense](https://huggingface.co/brgroup/TurnSense).

<br/>

## 🏆 Why TurnSense

<div align="center">

| Dimension | TurnSense Performance |
| :---: | :---: |
| 🎯 **Accuracy** | F1 **96.35%** on `easyturn_real_test_ZH` — best among comparable models |
| 🌐 **Language Support** | TurnSense 1.1 improves English turn detection and supports both Chinese and English scenarios |
| 📦 **Model Size** | Only **47M** parameters, with an INT8 version of about **50MB** |
| 🧠 **Classification Ability** | The first open-source model to natively support **complete / incomplete / invalid** three-class detection |
| 🚫 **Invalid Filtering** | Invalid utterance F1 reaches **94.34%**, effectively reducing noise-triggered false activations |
| 🤗 **Open-Source Friendly** | Provides FP32 / INT8 ONNX models, ready to use out of the box |

</div>

<br/>

---

<br/>

## 📌 Introduction

**TurnSense** is a **three-class semantic turn detection model** designed for human-machine speech interaction. It focuses on a core problem in conversational systems:

> **Should the system respond immediately while the user is speaking, or should it keep waiting?**

Traditional approaches usually perform only binary "end-of-turn" detection. **TurnSense goes further** by jointly modeling semantic completeness and invalid input detection. This helps systems achieve more natural turn-taking in complex real-world scenarios and significantly reduces premature interruption, overlapping speech, and invalid triggers.

<div align="center">
  <img src="./image/TurnSense.svg" alt="TurnSense three-class diagram" width="820"/>
</div>

<br/>

<div align="center">

## 🎬 Demo Video

<p align="center">
  <a href="https://huggingface.co/brgroup/TurnSense/blob/main/image/PR_new.mp4">
    <img src="./image/PR视频-封面.jpg" width="820" alt="TurnSense demo video">
  </a>
</p>

TurnSense classifies user input into three semantic states:

| State | Meaning | Example |
| :---: | :--- | :--- |
| ✅ **Complete** | The user's expression forms a complete intent, and the system can respond | `"Please check tomorrow's weather in Shanghai."` |
| ⏳ **Incomplete** | The user's expression is not finished and may continue after a pause or truncation | `"I want to ask about that order from yesterday..."` |
| 🔇 **Invalid** | The input does not form valid semantic content and should not trigger a response | `"...(continuous noise / nonverbal vocalization)"` |

</div>

These three labels allow the system to determine not only **"whether it should take the turn"**, but also **"whether the input is worth responding to"**. This improves interaction naturalness and system stability in voice assistants, real-time calls, intelligent customer service, and other speech interaction scenarios.

<br/>

---

<br/>

## ✨ Core Features

### 🧠 Semantic-Level Three-Class Detection

TurnSense jointly models `complete / incomplete / invalid` states. Compared with traditional binary turn detection, this is closer to real conversational behavior. It is also the only open-source solution that natively supports invalid semantic detection.

### 🌐 TurnSense 1.1: Enhanced English Capability

TurnSense 1.1 keeps the `complete / incomplete / invalid` three-class capability while focusing on improving semantic completeness detection in English scenarios.

Compared with the initial version, TurnSense 1.1 is better suited for bilingual voice assistants, English customer service, real-time meeting transcription, and cross-lingual human-machine interaction. It more reliably distinguishes complete English intent from unfinished English utterances.

### 📦 Lightweight Deployment

TurnSense maintains a lightweight design with about **47M** parameters and provides FP32 / INT8 ONNX versions, making it easy to integrate into CPU environments and edge deployment scenarios.

### 🎯 Strong Accuracy

On `easyturn_real_test_ZH` with 300 samples, TurnSense achieves **F1 96.35%** for `complete` and **F1 96.32%** for `incomplete`. On `semantic_test_ZH` with 2000 samples, it achieves **F1 92.30%** for `complete` and **F1 91.62%** for `incomplete`, reaching best or second-best performance among comparable models.

### 🚫 Invalid Input Filtering

On the NonverbalVocalization dataset, invalid utterance detection reaches **100% precision**, **90.37% recall**, and **94.34% F1**, effectively suppressing false activations caused by nonverbal vocalizations and noise.

### ⚖️ More Robust Turn-Taking Decisions

TurnSense balances precision and recall in semantically ambiguous, paused, or colloquial speech scenarios, reducing premature responses and missed responses.

### 📊 Reproducible Evaluation Pipeline

The project includes a complete evaluation workflow and scripts, supporting unified metric comparison and performance regression analysis to ensure reproducibility.

### 🤗 Open-Source Friendly and Ready to Use

TurnSense provides a standardized repository structure and FP32 / INT8 ONNX models. Installation and inference can be completed within minutes.

<br/>

---

<br/>

## 📐 Model Size Comparison

<div align="center">

| Model | Parameters | Three-Class | Link |
| :--- | :---: | :---: | :--- |
| TEN-Turn | **7B** | ❌ | [TEN-framework/TEN_Turn_Detection](https://huggingface.co/TEN-framework/TEN_Turn_Detection) |
| Easy-Turn | 850M | ❌ | [ASLP-lab/Easy-Turn](https://huggingface.co/ASLP-lab/Easy-Turn) |
| NAMO-Turn-Detector (ZH) | 66M | ❌ | [videosdk-live/Namo-Turn-Detector-v1-Multilingual](https://huggingface.co/videosdk-live/Namo-Turn-Detector-v1-Multilingual) |
| **⭐ TurnSense** | **47M** | **✅** | [**Baiji-Team/TurnSense**](https://huggingface.co/brgroup/TurnSense) |
| Smart-Turn-v3 | 8M | ❌ | [pipecat-ai/smart-turn-v3](https://huggingface.co/pipecat-ai/smart-turn-v3) |
| FireRedChat-turn-detector | -- | ❌ | [FireRedTeam/FireRedChat-turn-detector](https://huggingface.co/FireRedTeam/FireRedChat-turn-detector) |

</div>

> 💡 With only **47M** parameters, TurnSense provides native three-class detection and achieves a strong balance between accuracy and model size.

<br/>

---

<br/>

## 📊 Benchmark Results

> The following results cover Chinese, English, and invalid-utterance test sets. Chinese results mainly demonstrate the capability of the initial TurnSense version, while English results show the enhanced performance of TurnSense 1.1.

<br/>

### 📋 easyturn_real_test_ZH（300 samples）

> Data source: real samples from [Easy-Turn-Testset](https://huggingface.co/datasets/ASLP-lab/Easy-Turn-Testset)

| Model | P (complete) | R (complete) | **F1 (complete)** | P (incomplete) | R (incomplete) | **F1 (incomplete)** | p50 Latency | p90 Latency |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Easy-Turn | 97.26% | 94.67% | 95.95% | 94.81% | 97.33% | 96.05% | 183.87 (GPU) | 300.37 (GPU) |
| Smart-Turn-v3 | 64.97% | 76.67% | 70.34% | 71.54% | 58.67% | 64.47% | 36.84 | 39.10 |
| TEN-Turn | **99.25%** | 88.00% | 93.29% | 89.22% | **99.33%** | 94.01% | 17.66 (GPU) | 19.41 (GPU) |
| FireRedChat | 70.65% | 94.67% | 80.91% | 91.92% | 60.67% | 73.09% | 98.30 | 99.42 |
| NAMO-Turn | 81.53% | 85.33% | 83.39% | 84.62% | 80.67% | 82.59% | 3.60 | 83.44 |
| **⭐ TurnSense** | 96.03% | **96.67%** | **🏆 96.35%** | **96.64%** | 96.00% | **🏆 96.32%** | 54.65 | 58.00 |

> **🔍 Key finding:** TurnSense achieves the highest F1 for both `complete` and `incomplete`, and is the only model that reaches F1 > 96% with CPU p50 latency below 60ms.

<br/>

### 📋 semantic_test_ZH（2000 samples）

> Data source: Chinese test set from [KE-Team/SemanticVAD-Dataset](https://huggingface.co/datasets/KE-Team/SemanticVAD-Dataset)

| Model | P (complete) | R (complete) | **F1 (complete)** | P (incomplete) | R (incomplete) | **F1 (incomplete)** | p50 Latency | p90 Latency |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Easy-Turn | 78.14% | 98.30% | 87.07% | 97.64% | 70.30% | 81.74% | 183.87 (GPU) | 300.37 (GPU) |
| Smart-Turn-v3 | 59.25% | 88.10% | 70.85% | 76.80% | 39.40% | 52.08% | 36.84 | 39.10 |
| TEN-Turn | 85.25% | **99.60%** | 91.87% | **99.52%** | 82.70% | 90.33% | 17.66 (GPU) | 19.41 (GPU) |
| FireRedChat | 66.76% | 99.40% | 79.87% | 98.83% | 50.50% | 66.84% | 98.30 | 99.42 |
| NAMO-Turn | 71.48% | 86.70% | 78.36% | 83.10% | 65.40% | 73.20% | 3.60 | 83.44 |
| **⭐ TurnSense** | **88.96%** | 95.90% | **🏆 92.30%** | 95.55% | **88.00%** | **🏆 91.62%** | 54.65 | 58.00 |

> **🔍 Key finding:** On the larger 2000-sample test set, TurnSense continues to maintain the best F1 performance, demonstrating strong generalization.

<br/>

### 📋 TurnSense 1.1 English Enhancement Results

> Model download: [Hugging Face - brgroup/TurnSense](https://huggingface.co/brgroup/TurnSense)

> TurnSense 1.1 focuses on improving semantic completeness detection in English scenarios. The following results show its complete / incomplete performance on English test sets.

#### ten_test_EN

| Model | P (complete) | R (complete) | **F1 (complete)** | P (incomplete) | R (incomplete) | **F1 (incomplete)** |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| Smart-Turn-v3 | 70.66% | 72.46% | 71.55% | 65.05% | 63.02% | 64.02% |
| TEN-Turn | **98.61%** | 90.25% | **94.25%** | 89.15% | **98.44%** | **93.56%** |
| FireRedChat | 76.41% | **97.46%** | 85.66% | **95.28%** | 63.02% | 75.86% |
| NAMO-Turn | <u>92.65%</u> | 26.69% | 41.45% | 51.94% | <u>97.40%</u> | 67.75% |
| **⭐ TurnSense 1.1 int8** | 83.01% | 91.10% | 86.87% | 87.57% | 77.08% | <u>81.99%</u> |

#### semantic_test_EN

| Model | P (complete) | R (complete) | **F1 (complete)** | P (incomplete) | R (incomplete) | **F1 (incomplete)** |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| Smart-Turn-v3 | 68.18% | 75.00% | 71.43% | 72.22% | 65.00% | 68.42% |
| TEN-Turn | **97.98%** | 97.00% | **97.49%** | **97.03%** | **98.00%** | **97.51%** |
| FireRedChat | 72.06% | **98.00%** | 83.05% | 96.88% | 62.00% | 75.61% |
| NAMO-Turn | <u>93.55%</u> | 87.00% | <u>90.16%</u> | 87.85% | <u>94.00%</u> | <u>90.82%</u> |
| **⭐ TurnSense 1.1 int8** | 74.60% | 94.00% | 83.19% | <u>91.89%</u> | 68.00% | 78.16% |

<br/>

### 📋 NonverbalVocalization_invalid（728 samples）

> Data source: OpenSLR [Deeply Nonverbal Vocalization Dataset（SLR99）](https://openslr.elda.org/99/)

| Model | R (invalid) |
| :--- | :---: |
| **⭐ TurnSense** | **90.37%** |

> **🔍 Key finding:** TurnSense supports invalid semantic detection and can effectively reduce system responses triggered by nonverbal vocalizations or noise.

<br/>

---

<br/>

## 🚀 Quick Start

### 1. Installation

```bash
git clone https://github.com/Bairong-Xdynamics/TurnSense.git
cd TurnSense

pip install -U numpy onnxruntime torch librosa soundfile pandas scikit-learn huggingface_hub
```

### 2. Download Model Weights

TurnSense model weights are available on Hugging Face: [brgroup/TurnSense](https://huggingface.co/brgroup/TurnSense)

| Version | Description | Use Case |
| :--- | :--- | :--- |
| TurnSense | Initial three-class turn detection model | Chinese turn detection and invalid utterance filtering |
| TurnSense 1.1 | English-enhanced version | English / Chinese-English mixed turn detection |
| FP32 | Full-precision version | Accuracy-first scenarios |
| INT8 | Quantized version | Deployment-first scenarios |

**Download options:**

**Option 1: Automatic download (recommended)**

The inference script includes Hugging Face download logic and will automatically download and cache the model during the first run.

**Option 2: Git LFS**

```bash
git lfs install
git clone https://huggingface.co/brgroup/TurnSense
```

**Option 3: Hugging Face Hub**

```python
from huggingface_hub import snapshot_download
snapshot_download(repo_id="brgroup/TurnSense")
```

### 3. Inference

```bash
python infer.py
```

Example output:

```text
Loading model from brgroup/TurnSense...
Running inference on: "I want to ask about that order from yesterday..."

Results:
  Input: "I want to ask about that order from yesterday..."
  TurnSense Detection Result: "incomplete"
```

<br/>

---

<br/>

## 🧪 Evaluation Guide

### 1. Evaluation Pipeline

1. Read test datasets in `.jsonl` format.
2. Warm up each model first. The default value is `warmup_iters=20`.
3. Run inference sample by sample and collect classification and performance metrics.
4. Automatically export summary reports and detailed result files.

Output files include:

| File | Description |
| :--- | :--- |
| `report.md` | Summary evaluation report |
| `results.json` | Structured evaluation results |
| `config.json` | Evaluation configuration |
| `per_sample__*.jsonl` | Per-sample prediction results |

### 2. Data Format Requirements（JSONL）

Each line should be a JSON object containing at least the following fields:

| Field | Description |
| :--- | :--- |
| `audio_path` | Path to the audio file |
| `text` | Text content |
| `label` | Label: `complete` / `incomplete` / `invalid` |

Example:

```jsonl
{"audio_path":"/001.wav","text":"Please check tomorrow's weather in Shanghai.","label":"complete"}
{"audio_path":"/002.wav","text":"I want to ask about that order from yesterday...","label":"incomplete"}
{"audio_path":"/003.wav","text":"uh... hmm... continuous noise","label":"invalid"}
```

### 3. Run Evaluation

```bash
python TurnSense/Turn_benchmark/benchmark.py
```

<br/>

---

<br/>

## 📚 Citation

If you use TurnSense in your research or product, please cite:

```bibtex
@misc{turnsense2026,
  author       = {Baiji Team},
  title        = {TurnSense and TurnSense 1.1: Three-Class Semantic Turn Detection for Chinese and English Speech Interaction},
  year         = {2026},
  publisher    = {Hugging Face},
  howpublished = {\url{https://huggingface.co/brgroup/TurnSense}},
}
```

<br/>

<br/>

## ❓ Questions and Contact

If you have questions or suggestions, feel free to contact us through the following channels:

| Channel | Contact |
| :--- | :--- |
| 📧 Email | [huan.shen@brgroup.com](mailto:huan.shen@brgroup.com) ・ [yingao.wang@brgroup.com](mailto:yingao.wang@brgroup.com) ・ [wei.zou@brgroup.com](mailto:wei.zou@brgroup.com) |
| 💬 WeChat | h2538406363 |
| 👥 WeChat Group | Scan the QR code to join the group<br><img src="image/wechat.png" alt="WeChat group QR code" width="220" /> |
| 🐛 Issues | [GitHub Issues](https://github.com/Bairong-Xdynamics/TurnSense/issues) |
| 🔀 PR | [Pull Requests](https://github.com/Bairong-Xdynamics/TurnSense/pulls) |

<br/>

## 📄 License

This project is released under the **Apache License 2.0** with additional specific restrictions. See [LICENSE](./LICENSE) for details.

<br/>

---

<div align="center">

**Built with ❤️ by [Baiji Team](https://github.com/Bairong-Xdynamics)**

</div>
