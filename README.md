# Image Smoothing and Sharpening Using OpenCV

## Aim

To write a Python program using OpenCV to apply different smoothing filters (Averaging, Weighted Averaging, Gaussian, Median) and sharpening filters (Laplacian Kernel and Laplacian Operator) for image enhancement, and display each result separately along with the original image for comparison.

---

## The program performs the following operations:

- Read and display an input image  
- Apply Averaging filter  
- Apply Weighted Averaging filter  
- Apply Gaussian filter  
- Apply Median filter  
- Apply Laplacian sharpening using kernel  
- Apply Laplacian operator  
- Display all outputs for comparison  

---

##  Software Used

- Anaconda – Python 3.7  
- Jupyter Notebook / VS Code  
- OpenCV (cv2)  
- NumPy  
- Matplotlib  

---

##  Algorithm

### Step 1:
Import the required libraries: OpenCV, NumPy, and Matplotlib.
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

### Step 2:
Read the input image (e.g., `image.jpg`).
```python
img = cv2.imread('Downloads/WALT.jpg')

```
### Step 3:
Convert the image from BGR to RGB format for display.
```python
if img is None:
    raise FileNotFoundError("Could not read the image. Check the path and filename.")
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

plt.imshow(img_rgb)
plt.title("Original Image")
plt.axis("off")
plt.show()
```
### Step 4:
Apply Averaging Filter using `cv2.blur()`.
```python
avg_filtered = cv2.blur(img_rgb, (5, 5))

plt.figure(figsize=(10, 5))
plt.subplot(121); plt.imshow(img_rgb); plt.title("Original"); plt.axis("off")
plt.subplot(122); plt.imshow(avg_filtered); plt.title("Averaging Filter (5x5)"); plt.axis("off")
plt.show()
```
### Step 5:
Apply Weighted Averaging Filter using a custom kernel with `cv2.filter2D()`.
```python
# Center pixel gets the highest weight; the kernel sums to 1
kernel_weighted = np.array([[1, 2, 1],
                            [2, 4, 2],
                            [1, 2, 1]], dtype=np.float32) / 16

weighted_filtered = cv2.filter2D(img_rgb, -1, kernel_weighted)

plt.figure(figsize=(10, 5))
plt.subplot(121); plt.imshow(img_rgb); plt.title("Original"); plt.axis("off")
plt.subplot(122); plt.imshow(weighted_filtered); plt.title("Weighted Averaging Filter"); plt.axis("off")
plt.show()
```
### Step 6:
Apply Gaussian Filter using `cv2.GaussianBlur()`.
```python
gaussian_filtered = cv2.GaussianBlur(img_rgb, (5, 5), 0)

plt.figure(figsize=(10, 5))
plt.subplot(121); plt.imshow(img_rgb); plt.title("Original"); plt.axis("off")
plt.subplot(122); plt.imshow(gaussian_filtered); plt.title("Gaussian Filter (5x5)"); plt.axis("off")
plt.show()
```
### Step 7:
Apply Median Filter using `cv2.medianBlur()`.
```python
median_filtered = cv2.medianBlur(img_rgb, 5)   # kernel size must be odd

plt.figure(figsize=(10, 5))
plt.subplot(121); plt.imshow(img_rgb); plt.title("Original"); plt.axis("off")
plt.subplot(122); plt.imshow(median_filtered); plt.title("Median Filter (5x5)"); plt.axis("off")
plt.show()
```
### Step 8:
Apply Laplacian Sharpening using Kernel with `cv2.filter2D()`.
```python
# Laplacian-based sharpening kernel (identity + Laplacian)
kernel_sharpen = np.array([[ 0, -1,  0],
                           [-1,  5, -1],
                           [ 0, -1,  0]], dtype=np.float32)

sharpened = cv2.filter2D(img_rgb, -1, kernel_sharpen)

plt.figure(figsize=(10, 5))
plt.subplot(121); plt.imshow(img_rgb); plt.title("Original"); plt.axis("off")
plt.subplot(122); plt.imshow(sharpened); plt.title("Laplacian Kernel Sharpening"); plt.axis("off")
plt.show()
```
### Step 9:
Convert image to grayscale and apply Laplacian Operator using `cv2.Laplacian()`.
```python
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

laplacian = cv2.Laplacian(gray, cv2.CV_64F)
laplacian_abs = cv2.convertScaleAbs(laplacian)   # convert back to 8-bit for display

plt.figure(figsize=(10, 5))
plt.subplot(121); plt.imshow(gray, cmap='gray'); plt.title("Grayscale"); plt.axis("off")
plt.subplot(122); plt.imshow(laplacian_abs, cmap='gray'); plt.title("Laplacian Operator"); plt.axis("off")
plt.show()
```
### Step 10:
Display all filtered images using a grid layout for comparison.
```python
titles = ["Original", "Averaging", "Weighted Averaging", "Gaussian",
          "Median", "Laplacian Kernel Sharpening", "Grayscale", "Laplacian Operator"]
images = [img_rgb, avg_filtered, weighted_filtered, gaussian_filtered,
          median_filtered, sharpened, gray, laplacian_abs]

plt.figure(figsize=(18, 9))
for i in range(8):
    plt.subplot(2, 4, i + 1)
    if images[i].ndim == 2:
        plt.imshow(images[i], cmap='gray')
    else:
        plt.imshow(images[i])
    plt.title(titles[i])
    plt.axis("off")
plt.tight_layout()
plt.show()
```
<img width="1372" height="716" alt="Screenshot 2026-11-04 083348" src="https://github.com/user-attachments/assets/55ec7aed-7344-44d8-b512-105ed2c02e7d" />

---

##  Developed By

- **Name:** ASHWIN BAALAJI V K
- **Register No:** 212225230026

---

##  Output

### Smoothing Filters

- Averaging filter produces blurred image
<img width="1033" height="532" alt="Screenshot 2026-11-04 083146" src="https://github.com/user-attachments/assets/f449442a-9bc5-462d-849e-6dd78b22966d" />

- Weighted averaging provides smoother result with less distortion
<img width="1037" height="546" alt="Screenshot 2026-11-04 083311" src="https://github.com/user-attachments/assets/0d76957d-ffeb-4062-a202-f84df4c847cb" />

- Gaussian filter preserves edges better while reducing noise
<img width="1027" height="547" alt="Screenshot 2026-11-04 083318" src="https://github.com/user-attachments/assets/4064df13-9cef-4947-a673-1f891a7f7059" />

- Median filter removes salt-and-pepper noise effectively
<img width="1012" height="543" alt="Screenshot 2026-11-04 083324" src="https://github.com/user-attachments/assets/9f0ad6f4-3ada-490b-abd0-86b0a48ac334" />


###  Sharpening Filters

- Laplacian kernel enhances edges and fine details
<img width="1028" height="530" alt="Screenshot 2026-11-04 083330" src="https://github.com/user-attachments/assets/f50e20f0-d272-453e-8c15-319cb874a1fa" />

- Laplacian operator detects edges clearly in grayscale  
<img width="1025" height="537" alt="Screenshot 2026-11-04 083336" src="https://github.com/user-attachments/assets/1061420e-5246-4d8f-ab6a-6cf4d5811da3" />

---

##  Result

Thus, smoothing filters and sharpening filters are successfully implemented using OpenCV.

The smoothing filters reduce noise and improve image quality, while sharpening filters enhance edges and details for better feature extraction.
