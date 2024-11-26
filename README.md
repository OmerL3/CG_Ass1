Computer Graphics – Assignment 1 explanation

The entire code is in main.cpp – all operations implemented as functions within the file.
My idea was to keep the image as pointer to array, as it is contiguous so it’s faster.

Grayscale:
   •	Traversing the buffer for RGBA for every pixel (with I index)
   •	Assigning new values on the same buffer (with j index)
   •	Supporting both Weighted and Average
      in main - releasing the buffer and load it again in Canny as 2 comps grayscale image.
Canny Edge Detector:
   •	Blur:
      o	Supporting both Gaussian and Laplacian filters.
      o	Convolve(buffer, width, height, comps, filter):
         -	Applying 3x3 kernels.
         -	In case of border – use mirror indexing.
      o	getIndex(x, y, width, comps, comp):
         -	Calculate the actual index of buffer array to traverse as matrix indices.
   •	Sobel(buffer, width, height, comps, angles): -> [gradient calculation]
      o	Traversing the image without borders.
      o	Every pixel gets new value – magnitude, the value of the L2 norm of it’s gradient.
      o	Saving the angle values in another array.
   •	nonMaxSuppresion(buffer, width, height, comps, angles):
      o	Normalizing the angle to [-pi/2, pi/2]
      o	For every pixel, apply the method.
      o	Fixing border after the algorithm to discard wrong gradients.
   •	doubleThresholding(buffer, width, height, comps):
      o	Simple “cutoff” if grayscale value below 100. If higher than 170 make it white.
   •	hysteresis(buffer, width, height, comps):
      o	If non black(0) or white(255) check if has 255 neighbor, else make it black.
Halftone:
   •	Create new buffer at main, insert new values with aux-method updateHalftone.
Floyd Steinberg:
   •	Traversing the matrix and give neighbors the error.
   •	New values calculated as ((buffer+8)/16)*16 to simulate the grayscale values.
