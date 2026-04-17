# 🎙️ Real-time English-to-Persian Speech Translator

A high-performance, end-to-end pipeline for real-time automatic speech recognition (ASR) and instant translation. This project leverages **Faster-Whisper** and **Hugging Face Transformers** to deliver low-latency translations from English speech to Persian text via WebSockets.

---

## ✨ Key Features

- **Real-time Streaming:** Seamless audio transmission using WebSockets.
- **Advanced Audio Processing:** Client-side downsampling to 16kHz PCM using Web Audio API for minimal bandwidth usage.
- **SOTA AI Models:** Powered by `Faster-Whisper` for transcription and `Hugging Face` models for English-to-Persian translation.
- **Smart Caching:** Local model management to avoid redundant downloads and speed up cold starts.
- **Modern Stack:** Built with **FastAPI** (Asynchronous Backend) and **React.js** (Frontend).

---

## 🏗️ Architecture & Data Flow

1. **Frontend:** Captures microphone input, converts it to 16-bit PCM, and streams chunks to the server.
2. **Backend:** FastAPI receives binary chunks, performs VAD (Voice Activity Detection), and feeds the buffer into the ASR engine.
3. **Inference:** Faster-Whisper transcribes the audio, and the translation model converts the text to Persian.
4. **Broadcast:** Partial and Final results are pushed back to the UI instantly.



---

## 📂 Model Management & Cache

To ensure high performance, this project implements a local caching strategy:
- Models are stored in `backend/model_cache/`.
- The first execution downloads the weights; subsequent runs load directly from the local disk.
- **Note:** This directory is excluded from Git via `.gitignore` to keep the repository lightweight.

---

## 🚀 Getting Started

### Prerequisites
- Python 3.9+
- Node.js & npm
- **FFmpeg** (Required for audio processing)
- NVIDIA GPU (Recommended for CUDA acceleration)

### 1. Backend Setup
```bash
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r ../requirements.txt
# Run the server on port 3000
python -m uvicorn main:app --reload --port 3000


2. Frontend Setup
cd frontend
npm install
# Ensure frontend runs on a different port to avoid conflict
$env:PORT=3001; npm start  # Windows PowerShell

🛠️ Configuration
You can adjust the following parameters in backend/main.py:

model_size: e.g., "base", "small", "medium"

device: "cuda" or "cpu"

compute_type: "float16" (for GPU) or "int8" (for CPU)

🤝 Contact
Atiye Ziaei - (https://www.linkedin.com/in/atiyeziaei/)
Project Link: https://github.com/your-username/your-repo-name
