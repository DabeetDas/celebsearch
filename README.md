# celebsearch
This is a description of the edge detection algorithm developed to detect the edges in the given Mario jpeg image.
Various different methods have been employed to detect edges in the given image. They are:
1.	Sobel Operator (Both kernels)
2.	Scharr Operator
3.	Robert’s Operator
4.	Prewitt’s Operator
PRE-PROCESSING
•	First few lines of the code are self-explanatory, they involve preprocessing of the image. I have used the library open-cv to load the image into the interactive development environment and then convert them into grayscale. 
•	Converting the image into grayscale helps simplify our task as we are able to assign a single numerical value between 0-255 to each cell and in further computations, detecting the change in intensity becomes easier. For instance, had it been still in RGB, our algorithms to detect the change in intensity would have become much lengthier and more complicated. In RGB, algorithms would need to account for variations across all three channels. 
•	To extract the grayscale value for the image, I have divided it into a 160x300 matrix where each cell contains a single integral value ranging from 0-255 with 0 indicating a totally black cell and 255 representing a white cell. This has been called the grid value matrix.
Experiment #1: Use of the grayscale formula v/s the average value calculation for the image:
Initial versions of the code relied on the average grayscale value to construct the grid value matrix. Although insignificant for this code, using the grayscale formula is a better practice as it helps to construct the grid value matrix according to the perceived intensity of each channel. Eg. Maximum intensity of green is perceived to be brighter than that of blue and hence respective weights are assigned to account for these tiny details. 
IMPACT: Due to the simplicity of the image and absence of sharp features, it makes little difference which method we use here. However, for images with more complex details, the grayscale formula provides a more accurate representation of intensity.
•	In essence, to extract features from the image and achieve our goal of detecting edges, we need to perform a convolution. A function, convolve, with inputs as the grid value matrix, the kernel, stride and padding is written out. This function has been used throughout the code to perform convolutions. 
•	In pre-processing, another function, the scaler function has been constructed. This function is responsible for scaling all the values in its input matrix to the grayscale range. This has been done to avoid discrepancies caused by varying value ranges in the input data, ensuring uniformity and consistency during computations and further analysis. By scaling values to the standard grayscale range (0-255), the function helps maintain compatibility with image processing algorithms. 

ALGORITHM IMPLEMENTATION
There are primarily two broad approaches in the edge detection problem – the first approach involves using gradient descent and the other one is the gaussian approach. In this code, I have only used the gradient descent based approaches. 
The gradient descent based algorithms involve analysing changes in intensity to identify edges, by calculating gradients in the image. This code contains the implementation of the four aforementioned gradient descent algorithms. 
•	Sobel-Feldman Operator

