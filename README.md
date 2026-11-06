# STURDY OCTO DISCO – SUNGLASSES OVERLAY USING OPENCV

## Aim
To overlay sunglasses on a face image using Python and OpenCV image processing techniques.

## Description
Sturdy Octo Disco is a fun image processing project that adds sunglasses to individual passport-size photos. It uses image resizing, masking, and arithmetic blending techniques to place sunglasses over the eye region.

## Features
- Loads and displays a face image.
- Loads sunglasses with an alpha channel.
- Resizes sunglasses according to the eye region.
- Separates color and alpha channels.
- Applies image masking techniques.
- Combines the face and sunglasses using arithmetic operations.
- Displays the original and final images.

## Technologies Used
- Python
- OpenCV
- NumPy
- Matplotlib
- Jupyter Notebook

## Input Images
- `Image.png` – Original face image.
- `sunglass-png-trendy-sunglasses-prescription-sunglasses-1024.png` – Sunglasses image.

## Implementation
## NAME: THARSHINI M
## REG NO: 212224230287
### 1. Import Libraries
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

### 2. Load the Face Image
```python
faceImage = cv2.imread('Image.png')
plt.imshow(faceImage[:,:,::-1])
plt.title("Face")
```

### 3. Load the Sunglasses Image
```python
glassPNG = cv2.imread('sunglass-png-trendy-sunglasses-prescription-sunglasses-1024.png', -1)
```

### 4. Resize the Sunglasses
```python
glassPNG = cv2.resize(glassPNG, (360, 140))
```

### 5. Separate Color and Alpha Channels
```python
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
```

### 6. Apply Sunglasses to the Face
```python
faceWithGlassesNaive = faceImage.copy()
faceWithGlassesNaive[390:530, 350:710] = glassBGR
```

### 7. Apply Alpha Masking
```python
glassMask = cv2.merge((glassMask1, glassMask1, glassMask1))
glassMask = glassMask.astype(np.float32) / 255.0

glassBGR = glassBGR.astype(np.float32)
eyeROI = faceImage[390:530, 350:710].astype(np.float32)

maskedEye = cv2.multiply(eyeROI, (1 - glassMask))
maskedGlass = cv2.multiply(glassBGR, glassMask)

eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
```

### 8. Display the Final Output
```python
faceWithGlassesArithmetic = faceImage.copy()
faceWithGlassesArithmetic[390:530, 350:710] = np.uint8(eyeRoiFinal)

plt.figure(figsize=[20,20])

plt.subplot(121)
plt.imshow(faceImage[:,:,::-1])
plt.title("Original Image")

plt.subplot(122)
plt.imshow(faceWithGlassesArithmetic[:,:,::-1])
plt.title("With Sunglasses")

plt.show()
```

## Output
<img width="221" height="266" alt="{E261DF4B-7734-4C7A-AD8B-48CA83A4345F}" src="https://github.com/user-attachments/assets/0cf5bab6-e3e7-4b6a-a179-107f4c5e9648" />
<img width="330" height="181" alt="image" src="https://github.com/user-attachments/assets/d8756890-55fa-44f5-bc18-02cc5fb0b9ad" />
<img width="630" height="120" alt="{C2483CF2-4A2D-4170-8CC1-4E93517CA4CE}" src="https://github.com/user-attachments/assets/9626e677-4cf9-4013-9d72-63022cbc9c47" />
<img width="317" height="396" alt="{EF057ABD-D468-4A92-96F8-D38CA68BB2F3}" src="https://github.com/user-attachments/assets/d0b5e420-6adb-4e9c-9970-7cba8c03b853" />
<img width="547" height="83" alt="image" src="https://github.com/user-attachments/assets/cf450e9e-3e6a-41df-a61c-0ebe365963ae" />
<img width="550" height="344" alt="{D424AD57-B4A0-47C5-940B-87EE51FEDEBF}" src="https://github.com/user-attachments/assets/da402b0b-ab2d-4c20-a372-6aecb216c4fd" />






## Applications
- Digital image processing.
- Face image augmentation.
- Computer vision learning.
- Photo editing and enhancement.
- Image masking and blending practice.

## Conclusion
The project successfully demonstrates sunglasses overlay on a face image using OpenCV, NumPy, and Matplotlib. It helps understand image resizing, alpha masking, and arithmetic blending techniques.
