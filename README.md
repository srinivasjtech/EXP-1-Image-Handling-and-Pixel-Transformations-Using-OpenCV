<img width="389" height="389" alt="download" src="https://github.com/user-attachments/assets/92bc6fa2-4018-4e1c-b6e0-e48fb2904363" /># Ex. No. 01  Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## Program Developed By:
- **Name:** Srinivas J
- **Register Number:** 212225230276

## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program:

#### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread() as a grayscale image.
```python

import cv2
import numpy as np
import matplotlib.pyplot as plt
img = cv2.imread('Eagle_in_Flight.jpg', 0)

```

#### 2. Print the image width, height & Channel.
```python
h, w = img.shape
print("Width:", w, "Height:", h, "Channels: 1")
```

#### 3. Display the image using matplotlib imshow().
```python
plt.imshow(img, cmap='gray')
plt.show()
```

#### 4. Save the image as a PNG file using OpenCV imwrite().
```python
cv2.imwrite('Eagle_in_Flight.jpg', img)
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```python
color = cv2.imread('Eagle_in_Flight.jpg')
color = cv2.cvtColor(color, cv2.COLOR_BGR2RGB)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```python
print("Color image shape:", color.shape)
plt.imshow(color)
plt.show()
```

#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```python
crop = color[100:400, 100:400]
```

#### 8. Resize the image up by a factor of 2x.
```python
resize = cv2.resize(crop, None, fx=2, fy=2)
```

#### 9. Flip the cropped/resized image horizontally.
```python
flip = cv2.flip(resize, 1)
plt.imshow(flip)
plt.show()
```

#### 10. Read in the image ('Apollo-11-launch.jpg').
```python
apollo = cv2.imread('Apollo-11-launch.jpg')
```

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```python
h, w = apollo.shape[:2]
text = 'Apollo 11 Saturn V Launch, July 16, 1969'
font_face = cv2.FONT_HERSHEY_PLAIN
size = cv2.getTextSize(text, font_face, 1, 1)[0]
x = (w - size[0]) // 2
cv2.putText(apollo, text, (x, h-20), font_face, 1,(255, 255, 255), 2)
```

#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```python
cv2.rectangle(apollo, (100, 50), (400, h-50), (255, 0, 255), 2)
```

#### 13. Display the final annotated image.
```python
plt.imshow(cv2.cvtColor(apollo, cv2.COLOR_BGR2RGB))
plt.show()
```

#### 14. Read the image ('Boy.jpg').
```python
img = cv2.imread('Boy.png')
```

#### 15. Adjust the brightness of the image.
```python
matrix_ones = np.ones(img.shape, dtype=np.float64) * 50
matrix = matrix_ones.astype(np.uint8)
```

#### 16. Create brighter and darker images.
```python
img_brighter = cv2.add(img, matrix)
img_darker = cv2.subtract(img, matrix)
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
for x in [img, img_darker, img_brighter]:
    plt.imshow(cv2.cvtColor(x, cv2.COLOR_BGR2RGB))
    plt.axis('off')
    plt.show()
```

#### 18. Modify the image contrast.
```python
matrix1 = np.ones(img.shape, dtype=np.float64) * 1.1
matrix2 = np.ones(img.shape, dtype=np.float64) * 1.2
img_higher1 = cv2.multiply(img.astype(np.float64), matrix1)
img_higher2 = cv2.multiply(img.astype(np.float64), matrix2)
img_higher1 = np.clip(img_higher1, 0, 255).astype(np.uint8)
img_higher2 = np.clip(img_higher2, 0, 255).astype(np.uint8)
img_lower = cv2.convertScaleAbs(img, alpha=0.8)
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
for x in [img, img_lower, img_higher1, img_higher2]:
    plt.imshow(cv2.cvtColor(x, cv2.COLOR_BGR2RGB))
    plt.axis('off')
    plt.show()
```

#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```python
B, G, R = cv2.split(img)
for x in [B, G, R]:
    plt.imshow(x, cmap='gray')
    plt.axis('off')
    plt.show()
```

#### 21. Merged the R, G, B , displays along with the original image
```python
merged_rgb = cv2.merge([R, G, B])
plt.imshow(merged_rgb)
plt.title("Merged RGB Image")
plt.axis('off')
plt.show()
```

#### 22. Split the image into the H, S, V components & Display the channels.
```python
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
H, S, V = cv2.split(hsv)
for x in [H, S, V]:
    plt.imshow(x, cmap='gray')
    plt.axis('off')
    plt.show()
```
#### 23. Merged the H, S, V, displays along with original image.
```python
merged_hsv = cv2.merge([H, S, V])
merged_rgb = cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2RGB)
plt.imshow(merged_rgb)
plt.title("Merged HSV Image")
plt.axis('off')
plt.show()
```

## Output:

<img width="529" height="417" alt="download" src="https://github.com/user-attachments/assets/0694e379-8a92-4810-8408-4112cc466268" />

<img width="562" height="380" alt="download" src="https://github.com/user-attachments/assets/a35874cb-9451-4544-a898-98be890a0ba5" />

<img width="529" height="417" alt="download" src="https://github.com/user-attachments/assets/a338bcd7-cf13-48bb-babf-65e890e32131" />

<img width="389" height="389" alt="download" src="https://github.com/user-attachments/assets/c8c6a29f-4e45-44a4-bde5-3db937302b65" />

<img width="548" height="418" alt="download" src="https://github.com/user-attachments/assets/7adedbc3-1e9b-49a5-b9b2-13769c48dfbf" />

<img width="389" height="389" alt="download" src="https://github.com/user-attachments/assets/9bcad5ec-2e59-4092-a7f2-a9836cbbf835" />

<img width="389" height="389" alt="download" src="https://github.com/user-attachments/assets/9214a6ab-58d6-4dba-a668-7fab39e47eac" />

<img width="389" height="389" alt="download" src="https://github.com/user-attachments/assets/2c6b8999-8eda-40ca-baaa-446f1c9806d1" />

<img width="389" height="389" alt="download" src="https://github.com/user-attachments/assets/d8fbc080-5e21-450b-896d-5c483e3083d5" />

<img width="389" height="389" alt="download" src="https://github.com/user-attachments/assets/0ffdd0ff-0aa9-41bb-b6d7-b576848d8926" />

<img width="389" height="389" alt="download" src="https://github.com/user-attachments/assets/cbe0452e-9673-4739-a512-32a2e8df2634" />

<img width="389" height="389" alt="download" src="https://github.com/user-attachments/assets/0df8eee3-22bb-4041-9767-1564cc368f00" />

<img width="389" height="389" alt="download" src="https://github.com/user-attachments/assets/2d965c59-065c-4312-a653-4f07c9bfeaa0" />

<img width="389" height="411" alt="download" src="https://github.com/user-attachments/assets/1e74a165-501d-4b66-afff-e35a90a1408e" />

<img width="389" height="389" alt="download" src="https://github.com/user-attachments/assets/4998192c-b36e-4814-b664-0c8f88379956" />

<img width="389" height="389" alt="download" src="https://github.com/user-attachments/assets/7aa25a4c-7121-46b8-802f-8352d6824360" />

<img width="389" height="389" alt="download" src="https://github.com/user-attachments/assets/146d84b6-5ec4-4e7e-aac4-f057c6a8f41f" />

<img width="389" height="411" alt="download" src="https://github.com/user-attachments/assets/268469e1-051c-4a53-813b-e26ae648e92d" />


## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.

