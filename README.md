# 🏥 Medical Transcription & SOAP Note Generation Pipeline

## 📌 Overview

This project implements an end-to-end pipeline that:

1. Converts **medical dictation audio → text (Speech-to-Text)**
2. Transforms **unstructured transcript → structured SOAP note**

The system is designed with a focus on:

* ⚡ Performance (low latency)
* 🔒 Privacy-aware architecture
* 🧠 Practical production considerations

---

## ⚙️ Tech Stack

| Component              | Tool Used                    |
| ---------------------- | ---------------------------- |
| Speech-to-Text         | Whisper (local)              |
| LLM (SOAP Generation)  | Groq API (LLaMA-based model) |
| Language               | Python                       |


---

## 🏗️ Architecture

```
Audio Input (.mp3)
        ↓
Whisper Model (Local)
        ↓
Transcript (text)
        ↓
LLM via API (Groq)
        ↓
Structured SOAP JSON
        ↓
Validation Layer
```

---

## 🚀 Features

* ✅ Local transcription using Whisper (no external dependency)
* ✅ Fast SOAP generation using open-source LLM via API
* ✅ Strict JSON output format
* ✅ Validation layer to ensure:

  * No subjective leakage into objective
  * All SOAP sections present
  

---



---

## 🔧 Setup Instructions

### 1. Clone Repository

```
git clone <your-repo-link>
cd medical-soap-pipeline
```

---

### 2. Install Dependencies

```
pip install openai-whisper groq python-dotenv
apt-get install ffmpeg -y
```

---

### 3. Add API Key

Create a `.env` file:

```
GROQ_API_KEY=your_api_key_here
```

---

### 4. Run Notebook

Open the Jupyter/Colab notebook and run all cells in order:

1. Install dependencies
2. Upload audio file
3. Transcribe using Whisper
4. Generate SOAP using API
5. Validate output

---

## 🧠 Design Decisions

### 🔹 Whisper (Local)

* Avoids sending sensitive medical audio externally
* Reliable and accurate for transcription

### 🔹 API-based LLM (Groq)

* Eliminates model loading latency
* Provides near real-time inference (~1–2 sec)
* Uses open-source models under the hood

### 🔹 Prompt Engineering

* Strict constraints ensure:

  * Clean separation of SOAP sections
  * Concise clinical summaries
  * Structured JSON output

### 🔹 Validation Layer

* Detects:

  * Subjective language in Objective
  * Missing sections
* Acts as a safety check for model output

---

## 📊 Performance

| Step            | Time         |
| --------------- | ------------ |
| Transcription   | ~1 minute    |
| SOAP Generation | ~1–2 seconds |
| Total           | ~1–2 minutes |

---

## ⚠️ Challenges & Solutions

### ❌ Local LLM Slow on CPU

* Issue: High latency & memory usage
* ✅ Solution: Switched to API-based inference

### ❌ JSON Formatting Issues

* Issue: Model returning extra text
* ✅ Solution: Strict prompt + regex extraction

### ❌ Section Mixing (S/O)

* Issue: Model confusion
* ✅ Solution: Prompt constraints + validator

---

## 🔮 Future Improvements

* Add **medical NER (Named Entity Recognition)**
* Implement **confidence scoring**
* Build **FastAPI backend for real-time usage**
* Add **RAG-based clinical reasoning**
* Support **streaming transcription**

---

## 💬 cons

* Hybrid architecture (local + API)
* Handling latency vs privacy trade-offs
* Prompt engineering for structured output
* Validation layer for clinical correctness
* Scalability using API-based inference

---

## ✅ Output Example

```json
{
  "Subjective": "Patient reports right elbow pain for several months, worsening, rated 4/10.",
  "Objective": "Tenderness over lateral elbow, pain on wrist extension, full range of motion.",
  "Assessment": "Lateral epicondylitis (tennis elbow).",
  "Plan": "Activity modification, NSAIDs, physical therapy."
}
```

---

## 📌 Conclusion

This project demonstrates a **practical, production-aware approach** to transforming unstructured medical audio into structured clinical documentation, balancing:

* Accuracy
* Performance
* Scalability
* Security

---

## 👨‍💻 Author

Developed as part of a technical assessment for Medical NLP pipeline development.

---
