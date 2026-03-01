# SA Saudi License Plate Recognition (ALPR) System

<p>
  <img src="https://img.shields.io/badge/Python-3.10+-blue" />
  <img src="https://img.shields.io/badge/YOLO-v11/v11--Nano-green" />
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen" />
</p>

A robust, multi-stage AI pipeline designed to detect and recognize Saudi Arabian license plates with high precision. This project moves beyond traditional OCR methods, utilizing a **Cascade Object Detection** strategy to handle complex backgrounds, bilingual text, and varying lighting conditions.

---

## 🌟 Key Features

- **Cascade Architecture:** Uses two specialized YOLO models—one to find the plate and one to detect individual characters.

- **Logic-Based Filtering:** Custom geometric algorithms filter out the "KSA" emblem and Arabic script based on vertical positioning, isolating the ID number.

- **Bilingual Output:** Automatically maps detected English characters to their official Arabic counterparts (e.g., `S → س`).

---

## 🏗 Architecture Pipeline

The system processes images in four distinct stages:

1. **Plate Detection:**  
   A custom YOLOv11 model (trained on ~4,500 images) locates the license plate ROI.

2. **Preprocessing:**  
   The ROI is cropped using model coordinates.

3. **Character Detection:**  
   A secondary YOLOv11-Nano model (trained on ~1,300 annotated plates) detects letters and numbers (`0-9`, `A-Z`) as objects.

4. **Post-Processing:**

   - **Sorting:** Detections are sorted Left-to-Right via X-coordinates.
   - **Filtering:** Detections in the top 35% of the plate (logos/Arabic script) are discarded.
   - **Mapping:** English characters are converted to the Saudi Arabic format.
