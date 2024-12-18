# Edge Detection Algorithm for Mario JPEG Image

This is a description of the edge detection algorithm developed to detect the edges in the given Mario JPEG image.

Various different methods have been employed to detect edges in the given image. They are:

- **Sobel Operator** (Both kernels)
- **Scharr Operator**
- **Robert’s Operator**
- **Prewitt’s Operator**

---

## Structure and Contents

The structure and contents of each file in this repository is as follows:

1. **week1.ipynb** – This contains rough work/experiments used in the development phase.
2. **week1_final.ipynb** – This file contains the FINAL code for the project with all the results and proper plots for each operation.
3. **Copy of file(2)** has also been included in this repo, it also contains rough work and experiments.
4. **README** – Overview of the code.

---

## Pre-Processing

The first few lines of the code are self-explanatory; they involve preprocessing of the image. The library `OpenCV` is used to load the image into the interactive development environment and then convert it into grayscale.

Converting the image into grayscale helps simplify our task as we can assign a single numerical value between 0-255 to each cell. Detecting the change in intensity becomes easier. For instance, had it been still in RGB, our algorithms to detect the change in intensity would have become much lengthier and more complicated. In RGB, algorithms would need to account for variations across all three channels.

To extract the grayscale value for the image, I divided it into a 160x300 matrix where each cell contains a single integral value ranging from 0-255:
- `0` indicates a totally black cell
- `255` represents a white cell.

This has been called the **grid value matrix**.

### Experiment #1: Use of Grayscale Formula vs. Average Value Calculation

Initial versions of the code relied on the average grayscale value to construct the grid value matrix. Although insignificant for this code, using the grayscale formula is a better practice as it helps construct the grid value matrix according to the perceived intensity of each channel. For example, the maximum intensity of green is perceived to be brighter than that of blue, and respective weights are assigned to account for these tiny details.

- **Impact:** Due to the simplicity of the image and the absence of sharp features, it makes little difference which method is used here. However, for images with more complex details, the grayscale formula provides a more accurate representation of intensity.

To extract features from the image and achieve the goal of detecting edges, a convolution is performed. A function, `convolve`, with inputs as the grid value matrix, the kernel, stride, and padding, is written out. This function has been used throughout the code to perform convolutions.

In preprocessing, another function, the `scaler` function, has been constructed. This function scales all the values in its input matrix to the grayscale range. This avoids discrepancies caused by varying value ranges in the input data, ensuring uniformity and consistency during computations and further analysis.

---

## Algorithm Implementation

There are primarily two broad approaches in the edge detection problem:
1. **Gradient Descent**
2. **Gaussian Approach**

In this code, I have only used the **gradient descent-based approaches**.

### Gradient Descent-Based Algorithms

These involve analyzing changes in intensity to identify edges by calculating gradients in the image. The code contains the implementation of four gradient descent algorithms:

#### Sobel-Feldman Operator

The **Sobel operator**, sometimes called the Sobel–Feldman operator or Sobel filter, is used in image processing and computer vision, particularly within edge detection algorithms, where it creates an image emphasizing edges. It is named after Irwin Sobel and Gary M. Feldman, colleagues at the Stanford Artificial Intelligence Laboratory (SAIL).

This operator is designed to predict edges using variations in intensity of various cells in the grid value matrix. A Sobel operator consists of two matrices – the Sobel X and Sobel Y, which measure the variation in intensity in the X and Y (horizontal and vertical) directions, respectively.

- **Sobel-X Matrix:**  
  This matrix performs weighted subtractions to detect changes in the horizontal direction. The middle row, containing `2` and `-2`, emphasizes intensity changes in the direct neighborhood of the concerned cell. This design enhances the detection of horizontal edges while reducing the influence of diagonal or vertical intensity variations.

- **Sobel-Y Matrix:**  
  This matrix works similarly to Sobel-X but detects changes in the vertical direction.

#### Combining Both

1. **Square-Root Approach:**  
   After performing convolutions and obtaining the X and Y matrices, the overall change in intensity is computed using a formula analogous to the Pythagorean theorem:  
   \( G = \sqrt{G_x^2 + G_y^2} \)  
   - **F1 Score:** 0.85  
   - **Precision:** 0.78  
   - **Recall:** 0.94  

2. **Modulus Approach:**  
   A simpler formula is used for \( G \):  
   \( G = |G_x| + |G_y| \)  
   - **F1 Score:** 0.86  
   - **Precision:** 0.81  
   - **Recall:** 0.91  

The **modulus approach** provides slightly better precision but lower recall.

---

## Experiments and Observations

### Experiment #2: Gaussian Blur
- **Description:** A Gaussian blur was applied to the input image to test its effect on edge detection.  
- **Result:** Because the image had clear intensity transitions, the blur did not result in significant changes. Edges were already prominent. This was excluded from the final code.

### Experiment #3: Adding a Threshold
- **Description:** A threshold was added in the Sobel function. If the threshold was exceeded, a white response was returned; otherwise, black.  
- **Result:** The algorithm failed to detect certain edges near the character’s hand. This was excluded from the final code.

### Experiment #4: Comparison with Prewitt’s Operator
- **Description:** The Prewitt operator, similar to the Sobel-Feldman operator, emphasizes derivatives of the intensity function to detect edges.  
- **Result:** Prewitt’s operator lagged behind the Sobel-Feldman operator on all evaluation metrics (F1 Score, Precision, Recall). This behavior is expected as Prewitt lacks the emphasis on immediate neighbors, which Sobel-Feldman accounts for.

---

## Conclusion

This project implemented multiple edge detection algorithms, with the **Sobel-Feldman operator** providing the best results for the given image.
