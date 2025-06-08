
# Whisper+Translit+KWS: Hindi Speech Recognition and Keyword Spotting

## Environment Setup

### 1. Create and Activate Conda Environment
```bash
conda create -n whisenv
conda activate whisenv
```

### 2. Install Required Packages
```bash
pip install pandas tqdm numpy
pip install torch==2.4.1 torchvision==0.19.1 torchaudio==2.4.1 --index-url https://download.pytorch.org/whl/cu118
pip install transformers datasets evaluate peft bitsandbytes accelerate
pip install h5py wrapt librosa
pip install soundfile jiwer
pip install tensorflow keras rich tf-keras
```

---

## Dataset

- **Common Voice Hindi Corpus 21.0**
- Path: `C:/Users/WORKSTATIONS/Desktop/BijoyashreeDas/COMMON_VOICE_HI/cv-corpus-21.0-2025-03-14/hi`
- **Train samples:** 7,563  
- **Test samples:** 3,337

---

## Notebook Overview

All implementation details are available in the notebook: `Whisper+Translit+KWS.ipynb`.

### Steps:

#### 1. Model Setup for Hindi Speech-to-Text with Whisper
- Loads OpenAI Whisper large model for Hindi ASR.
- Initializes tokenizer, feature extractor, and model.
- Sets up the GPU (cuda) for inference.

#### 2. Whisper Processor Initialization
- Combines tokenizer and feature extractor via `WhisperProcessor`.

#### 3. Dataset Processing (train+dev, test)
- Merges `train` and `dev` sets.
- Converts to `DatasetDict`.
- Keeps only `audio` and `sentence` columns.

#### 4. Audio Resampling
- Ensures all audio samples are 16kHz using `torchaudio`.

#### 5. Baseline Evaluation
- Computes WER on train and test sets before fine-tuning.

#### 6. Transcription Examples
- Shows actual vs predicted transcriptions for 10 test samples.

#### 7. Feature Extraction and Tokenization
- Applies log-mel spectrograms + transcription tokenization.

#### 8. LoRA Fine-Tuning (Parameter-Efficient)
- Uses `peft` and `LoRA`:
```python
from peft import LoraConfig, get_peft_model
config = LoraConfig(r=32, lora_alpha=64, target_modules=["q_proj", "v_proj"], lora_dropout=0.05, bias="none")
model = get_peft_model(model, config)
model.print_trainable_parameters()
```
- **Trainable params:** 15,728,640  
- **Total params:** 1,559,033,600  
- **Only 1% of the model is fine-tuned.**

#### 9. Training
- Saves LoRA adapter weights separately (lightweight).

#### 10. Evaluation and Inference
- Loads base Whisper model + LoRA adapters.
- Uses 8-bit mode for efficiency.
- Caches enabled for fast inference.
- Saves combined model and processor.

#### 11. Final Evaluation
- Saves full final model.
- Computes post-training WER again.

(Note that training till higher epochs is increasing the WER, hence trained till only 100 steps)
Refer the jupyter notebook for 100 STEPS


---

This repository combines Whisper for Hindi speech transcription, Indic transliteration, and hybrid keyword spotting using fuzzy and phonetic matching.
