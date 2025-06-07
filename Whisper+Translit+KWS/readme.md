# Keyword Spotting with Whisper

This project performs **automatic speech recognition (ASR)** on Hindi audio files using the [Whisper model](https://huggingface.co/openai/whisper-large-v3), followed by **transliteration** to Latin script and **keyword spotting** using both **fuzzy string matching** and **phonetic similarity**.

---

## 🔍 Key Features

- ✅ Transcribes `.wav` files with Hindi speech using OpenAI's Whisper.
- 🔤 Converts Hindi (Devanagari) transcriptions to Latin script.
- 🧠 Detects English keywords using:
  - String similarity (via RapidFuzz)
  - Phonetic similarity (via Double Metaphone)
- 📄 Saves the output (transcriptions and matches) to a text file.

---

## 📁 Folder Structure

```
project-root/
├── main.py              # Main script (this code)
├── hindi_transcriptions.txt  # Output file (auto-generated)
└── storm_vad/           # Folder containing Hindi audio (.wav) files
```

---

## 📦 Dependencies

Install dependencies via pip or conda:

```bash
pip install torch soundfile transformers rapidfuzz Metaphone indicate
```

Note: You may need to install [ffmpeg](https://ffmpeg.org/) separately if using audio files with different encodings.

---

## 🧠 Model Used

- [`openai/whisper-large-v3`](https://huggingface.co/openai/whisper-large-v3)
- Automatically downloaded via Hugging Face Transformers.

---

## 🚀 How to Run

1. Place your Hindi `.wav` audio files in the `storm_vad` directory.
2. Update the `audio_folder` path in `main.py` if necessary.
3. Run the script:

```bash
python main.py
```

4. View results in `hindi_transcriptions.txt`.

---

## 📝 Output Example

For each `.wav` file:
- Hindi Transcription
- Latin Transliteration
- Matching Keywords (with similarity score and match type)

```
🎧 File: example.wav
📝 Hindi: रिपोर्ट कॉलिंग पॉइंट पर वाहन चेकिंग हो रही है
🔤 Latin: report calling point par vaahan checking ho rahi hai
🔎 Keywords found (≥85% similarity or phonetic match): report ~ report (100%, string), calling ~ calling (100%, string), point ~ point (100%, string), checking ~ checking (100%, string), vehicle ~ vaahan (phonetic match)
```

---

## 🛠 Customization

- Modify the `keyword_set` in `main()` to include your own target keywords.
- Adjust the `sim_threshold` to make the matching stricter or more lenient.

---

## 📌 Notes

- Audio must be mono and sampled at **16 kHz**. Other sampling rates will raise an error.
- Empty or unreadable audio files are skipped with error logging.
- Transliteration is performed **only** for Hindi (Devanagari) words.

---

## 📄 License

This project is for academic and research purposes. Attribution required if reused.

---

## 🙋‍♀️ Author

Bijoyashree Das  
M.Tech in Signal Processing and Communication Engineering  
Roll No. 23SP06004
