# Whisper Fine-Tuning for Air Traffic Control (ATC) Speech Recognition

This project focuses on fine-tuning all parameters of OpenAI's Whisper model for a domain-specific speech dataset: **Air Traffic Control (ATC)**. The pipeline supports preprocessing, transcription, and evaluation using metrics like WER (Word Error Rate).

---

## 🚀 Environment Setup

### 🧪 Step 1: Package Installation

```bash
# Required libraries
pip install "datasets>=2.6.1"
pip install "evaluate>=0.30"
pip install librosa
pip install jiwer
pip install transformers

# Reinstall compatible PyTorch stack (for CUDA 12.1)
pip uninstall torch torchvision torchaudio -y
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
