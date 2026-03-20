# ANPR Plate Reader (Rwanda-Focused)

This repository contains a lightweight Automatic Number Plate Recognition (ANPR) pipeline built for real-time plate capture and logging.

It follows this processing chain:

**Detect -> Align -> OCR -> Validate -> Temporal Confirm -> Save**

## What Makes This Project Different
- Designed around practical live-camera usage, not only static images.
- Includes temporal confirmation to reduce one-frame OCR mistakes.
- Stores both plate text and a captured crop for traceability.
- Ships with plate validation patterns that fit common Rwanda-style formats.

## Core Capabilities
- Reads frames from a webcam stream.
- Detects candidate plate regions.
- Corrects plate perspective before OCR.
- Extracts text via Tesseract OCR.
- Filters noisy OCR output using regex validation.
- Confirms a plate only after repeated observations.
- Saves confirmed records to `data/plates.csv`.

## Repository Layout
```text
anpr-project-main/
├── readme.md
├── requirements.txt
├── src/
│   ├── camera.py
│   ├── detect.py
│   ├── align.py
│   ├── ocr.py
│   ├── validate.py
│   ├── temporal.py
│   ├── storage.py
│   └── main.py
├── data/
│   ├── plates.csv
│   └── captures/
└── screenshots/
    ├── detection.png
    ├── alignment.png
    └── ocr.png
```

## Supported Plate Patterns
Validation logic in `src/validate.py` currently supports:
- `^[A-Z]{3}[0-9]{3}[A-Z]?$` (example: `RAB123A` or `RAB123`)
- `^[A-Z]{2}[0-9]{3}[A-Z]{2}$` (example: `RA123BC`)

To support additional regions or formats, extend `PLATE_PATTERNS` in `src/validate.py`.

## Quick Start
1. Install dependencies:
   - `pip install -r requirements.txt`
2. Run the pipeline:
   - `python src/main.py`
3. Check outputs:
   - Plate logs: `data/plates.csv`
   - Plate crops: `data/captures/`

## Screenshots
### Plate Detection
![Plate Detection](screenshots/detection.png)

### Plate Alignment
![Aligned Plate](screenshots/alignment.png)

### OCR Pre-processing
![OCR Process](screenshots/ocr.png)
