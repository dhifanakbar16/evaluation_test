
# Cockpit Display Evaluation Tool (Python Scaffold)

This repository is a **starter scaffold** for a tool that:
1. **Loads a cockpit display image**.
2. **Detects elements** (gauges, numbers, shapes) using OpenCV and (optionally) Tesseract OCR.
3. **Measures properties** (size, center coordinates, colors, color proportions).
4. **Evaluates design laws/principles** (configurable in YAML) for each element.
5. **Exports results** as **CSV** and **annotated images**, plus a **heatmap**.
6. Offers both a **CLI (command line interface)** and a basic **Streamlit app** UI.

> **Beginner-friendly glossary:**  
> - **Module**: a `.py` file with Python code.  
> - **Package**: a folder with an `__init__.py` file; lets Python treat it as a group of modules.  
> - **API**: the set of functions/classes other code can call.  
> - **CLI**: run the tool from the terminal with commands.  
> - **YAML**: a human-readable text format for settings (like JSON but easier to read).

## Quick Start (Windows, with Visual Studio Code or Visual Studio)

1. **Install Python 3.10+**: https://www.python.org/downloads/
2. **(Optional) Create a virtual environment**:
   ```bash
   python -m venv .venv
   .venv\Scripts\activate
   ```
3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
4. **Install Tesseract OCR (optional but recommended)**:  
   - Windows: https://github.com/UB-Mannheim/tesseract/wiki (Note the install path, e.g. `C:\Program Files\Tesseract-OCR\tesseract.exe`).  
   - macOS: `brew install tesseract`.  
   - Linux: `sudo apt-get install tesseract-ocr`.
   - If needed, set the path in `src/cockpit_eval/ocr/ocr.py`.

5. **Try the CLI** on a sample image:
   ```bash
   python scripts/run_cli.py --image data/samples/sample_display.png --output data/output
   ```

6. **Try the Streamlit app**:
   ```bash
   streamlit run app/streamlit_app.py
   ```

## Repository Structure

```
cockpit-eval-tool/
├── app/                     # small Streamlit UI
│   └── streamlit_app.py
├── data/
│   └── samples/             # put a few example images here
├── scripts/
│   └── run_cli.py           # command-line entry point
├── src/
│   └── cockpit_eval/
│       ├── __init__.py
│       ├── config.py        # configuration helpers
│       ├── io/
│       │   └── image_io.py  # load/save images and CSV
│       ├── detect/
│       │   ├── detector.py  # find elements with OpenCV
│       │   └── color_analysis.py
│       ├── ocr/
│       │   └── ocr.py       # text recognition via Tesseract
│       ├── laws/
│       │   ├── law_registry.py
│       │   └── law_definitions.yaml
│       ├── evaluate/
│       │   └── evaluator.py # apply laws to elements
│       ├── visualize/
│       │   ├── overlay.py   # draw bounding boxes/labels
│       │   └── reports.py   # heatmap & plots
│       └── utils/
│           ├── geometry.py
│           └── image_utils.py
├── tests/
│   └── test_smoke.py
├── .gitignore
├── pyproject.toml
├── requirements.txt
└── README.md
```

## Packaging into an App

- **Desktop app**: You can bundle the CLI into a one‑file executable with **PyInstaller**.
- **Simple Web UI**: This repo includes a **Streamlit** app; you can deploy it to Streamlit Community Cloud or run locally.
- **API server**: Use **FastAPI** if you later want a backend service that other tools can call.

## Notes

- The detection/evaluation logic is **placeholder**—you can gradually replace the stub functions with real algorithms.
- The `laws/law_definitions.yaml` file is where you define your **29 laws** (22 with rules now). Each law can specify ranges or thresholds per element type.
