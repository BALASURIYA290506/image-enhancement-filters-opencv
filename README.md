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
img = cv2.imread('image.jpg')

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

---

##  Developed By

- **Name:** M BALASURIYA
- **Register No:** 212224240021

---

##  Output
<img width="578" height="342" alt="image" src="https://github.com/user-attachments/assets/fe47b090-a392-4d45-9fc5-2db10f8f300a" />


### Smoothing Filters

- Averaging filter produces blurred image
<img width="817" height="247" alt="image" src="https://github.com/user-attachments/assets/a634472d-7df7-4ba6-9557-56b5dc0efa0e" />





- Weighted averaging provides smoother result with less distortion
<img width="830" height="252" alt="image" src="https://github.com/user-attachments/assets/1f3d42e0-e8fe-40fc-9e2a-59a37dd9f833" />


- Gaussian filter preserves edges better while reducing noise
<img width="827" height="257" alt="image" src="https://github.com/user-attachments/assets/36af0a8d-5b61-4bf4-9000-4d05392b2a40" />


- Median filter removes salt-and-pepper noise effectively
<img width="815" height="248" alt="image" src="https://github.com/user-attachments/assets/8c1a6c06-4383-4366-9510-92e98cb43899" />



###  Sharpening Filters

- Laplacian kernel enhances edges and fine details
<img width="815" height="247" alt="image" src="https://github.com/user-attachments/assets/b4b7b0f6-30ad-45d9-b8dc-2e8fdd53a416" />


- Laplacian operator detects edges clearly in grayscale  
<img width="837" height="252" alt="image" src="https://github.com/user-attachments/assets/1ca702eb-6676-4d5f-a65e-1b03088f69bb" />

<img width="1002" height="380" alt="image" src="https://github.com/user-attachments/assets/81535960-df79-41c9-acc3-89f0d6a43a7c" />


---

##  Result

Thus, smoothing filters and sharpening filters are successfully implemented using OpenCV.

The smoothing filters reduce noise and improve image quality, while sharpening filters enhance edges and details for better feature extraction.
