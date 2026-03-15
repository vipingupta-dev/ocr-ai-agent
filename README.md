# OCR AI Agent

A Python project that reads text from images automatically.

What makes it different from a simple OCR tool is that it first looks at the image, figures out what kind of image it is, and then picks the best model for that specific image. I built this in Google Colab using pretrained models so no training from scratch was needed.

---

## What it does

You give it any image that has text in it. The agent analyzes the image, decides which OCR model will work best, and then extracts the text. All of this happens automatically without you having to choose anything manually.

---

## How it works

The agent runs through these steps on every image:

1. **Analyze** — measures contrast, noise, edge density and color variance of the image
2. **Classify** — uses those measurements to decide if the image is a scene photo, a printed document, or handwritten text
3. **Select model** — picks the best pretrained model for that image type
4. **Preprocess** — applies the right preprocessing steps for the selected model
5. **Extract text** — runs the model and pulls out all the text
6. **Output** — shows the result and lets you download it as a text file

---

## Which model gets selected and when

| Image Type | Model Used | Why |
|---|---|---|
| Scene photo (street signs, banners) | EasyOCR (CRAFT + CRNN) | Trained on real world scene text |
| Printed document or digital text | TrOCR printed (ViT + GPT2) | Trained on printed documents |
| Handwritten text | TrOCR handwritten (ViT + GPT2) | Trained on handwriting samples |

All three are pretrained models. This project uses transfer learning meaning I am reusing weights that were already trained by researchers, not training anything from scratch.

---

## Tech stack

- Python
- PyTorch
- EasyOCR
- Microsoft TrOCR (HuggingFace Transformers)
- OpenCV
- Gradio (for the web UI)
- Google Colab

---

## How to run it

**Option 1 — Google Colab (easiest)**

- Open the `ocr_ai_agent.ipynb` file
- Click on the Colab badge or upload it to colab.research.google.com
- Run cells from top to bottom
- The last cell launches a Gradio web app with a public link

**Option 2 — Run locally**

Make sure you have Python installed then run:

```
pip install -r requirements.txt
```

Then open the notebook in Jupyter and run all cells.

---

## Requirements

All dependencies are listed in `requirements.txt`. Main ones are:

```
torch
easyocr
transformers
opencv-python
gradio
Pillow
matplotlib
```

---

## Project structure

```
ocr-ai-agent/
│
├── ocr_ai_agent.ipynb     # main notebook with all the code
├── requirements.txt       # all dependencies
├── README.md              # this file
└── .gitignore             # files excluded from git
```

---

## What I learned building this

The biggest lesson was that no single OCR model works well on all image types. EasyOCR is great on scene photos but struggles on clean digital text. TrOCR is great on documents but was not designed for scene text. Building the agent to automatically route each image to the right model solved this problem cleanly.

I also learned that preprocessing steps that help classical OCR tools (like binarization and thresholding) actually hurt deep learning models like TrOCR and EasyOCR because these models do their own internal preprocessing and expect the original image.

---

## Author

Vipin Gupta
vipingupta.dev@gmail.com
github.com/vipingupta-dev
