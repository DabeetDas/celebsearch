# Edge Detection Algorithm for Mario JPEG Image

## Overview

This document describes the edge detection algorithm developed to detect edges in the given Mario JPEG image. Various methods employed include:

- **Sobel Operator** (Both kernels)
- **Scharr Operator**
- **Robert’s Operator**
- **Prewitt’s Operator**

---

## Structure and Contents

The repository contains the following files:

1. **week1.ipynb** – Rough work/experiments from the development phase.
2. **week1_final.ipynb** – Final code with results and proper plots for each operation.
3. **Copy of File (2)** – Includes rough work and experiments.
4. **README** – Overview of the code.

---

## Pre-Processing

The initial lines of the code involve preprocessing the image using the `OpenCV` library. The image is converted to grayscale for simplicity, as each cell can be assigned a single numerical value (0-255). This simplifies the detection of intensity changes.

- **Grid Value Matrix:** A 160x300 matrix where each cell contains an intensity value:
  - `0` = Black
  - `255` = White

### Experiment #1: Grayscale Formula vs. Average Value
- **Grayscale Formula:** More accurate for complex images by assigning weights to RGB channels.
- **Impact:** Minimal difference for this simple image, but crucial for complex images.

---

## Algorithm Implementation

Two broad approaches exist for edge detection:
1. **Gradient Descent**
2. **Gaussian Approach**

This code employs gradient descent-based algorithms, including the following:

### Sobel-Feldman Operator
The Sobel operator predicts edges using intensity variations, with two matrices:
- **Sobel-X:** Detects horizontal edges.
- **Sobel-Y:** Detects vertical edges.

#### Combining Both
- **Square-Root Approach:**  
  \( G = \sqrt{G_x^2 + G_y^2} \)  
  - F1 Score: `0.85`
  - Precision: `0.78`
  - Recall: `0.94`

- **Modulus Approach:**  
  \( G = |G_x| + |G_y| \)  
  - F1 Score: `0.86`
  - Precision: `0.81`
  - Recall: `0.91`

The modulus approach offers better precision but slightly lower recall.

---

## Experiments

### Experiment #2: Gaussian Blur
- **Result:** No significant changes due to the image's clear intensity transitions. Excluded from the final code.

### Experiment #3: Adding a Threshold
- **Result:** Algorithm failed to detect certain edges near the character's hand. Excluded from the final code.

### Experiment #4: Comparison with Prewitt’s Operator
- **Result:** Sobel-Feldman outperformed Prewitt’s operator in all evaluation metrics, as Prewitt lacks emphasis on immediate neighbors.

---

## Conclusion

This project explores various edge detection methods, with the Sobel-Feldman operator providing the best results for the given image.
