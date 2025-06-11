# 🎥 Video Captioning with BLIP & BART (Short Video AI Pipeline)

This repository provides a full **AI-powered video captioning pipeline** designed to automatically describe short video clips (e.g. 5–10 seconds) in natural language. The system uses state-of-the-art **vision-language models** (BLIP and BART) to extract, caption, and summarize visual content efficiently — and is **optimized to run in Google Colab** with GPU support.

---

## 🚀 Objective

To generate **descriptive, human-like captions** for short video clips using a combination of:

- 🔍 Frame sampling
- 🧠 Vision-to-language captioning
- 📝 Language summarization

All within a fast, modular Python workflow.

---

## 🧠 Methodology

This pipeline breaks down video captioning into three main stages:

### 1. 🎞️ **Frame Extraction (Video ➝ Images)**
- **Library**: OpenCV
- **Method**: Sample one frame every `N` seconds (default: 1s) to avoid redundancy while still capturing key visual elements.
- **Purpose**: Short videos (~6s) typically only need 2–6 keyframes.

### 2. 🧠 **Image Captioning (Images ➝ Sentences)**
- **Model**: `Salesforce/blip-image-captioning-base`
- **Library**: HuggingFace `transformers`
- **Method**: Each frame is independently captioned using BLIP, a pretrained vision-language model.

    > Example:  
    > Frame 1 → “A man is standing on a sidewalk.”  
    > Frame 2 → “Cars are parked near a building.”

### 3. 📝 **Caption Summarization (Sentences ➝ Final Caption)**
- **Model**: `facebook/bart-large-cnn`
- **Library**: HuggingFace `pipeline`
- **Method**: All frame-level captions are joined and passed through BART to generate a short, single-sentence summary.
  
    > Example Final Summary:  
    > “A man is walking on a street with parked cars around him.”

---

## 🧰 Tools & Models Used

| Task                  | Tool / Model                          | Reason                                       |
|-----------------------|----------------------------------------|----------------------------------------------|
| Frame extraction      | OpenCV                                 | Lightweight, fast, video-compatible          |
| Image captioning      | BLIP Base (`Salesforce/blip...`)       | Great speed/accuracy trade-off               |
| Caption summarization | BART (`facebook/bart-large-cnn`)       | Fine-tuned for news-style summarization      |
| Model framework       | HuggingFace `transformers`, `torch`    | Industry-standard support                    |
| Accelerator           | `accelerate`, `cuda` (if available)    | Enables GPU offloading on Colab              |

---

## 📁 Folder Structure

```bash
video-captioning-blip/
├── video_captioning.py        # Main Python script
├── requirements.txt           # Dependency list
├── example_videos/            # short clips go here
└── README.md                  # You're reading this!
