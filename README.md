# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

## Name: Pavithra K

## Reg No: 212224240112

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:

-Detects the face in an image.

-Places a stylish sunglass overlay perfectly on the face.

-Works seamlessly with individual passport-size photos.

-Customizable for different sunglasses styles or photo types.

## Technologies Used:

-Python

-OpenCV for image processing

-Numpy for array manipulations

## How to Use:

-Clone this repository.

-Add your passport-sized photo to the images folder.

-Run the script to see your "cool" transformation!

## Applications:

1.Learning basic image processing techniques.

2.Adding flair to your photos for fun.

3.Practicing computer vision workflows.

Feel free to fork, contribute, or customize this project for your creative needs!

## Program:
```
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load the Face Image
faceImage = cv2.imread('p.png')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
faceImage.shape

#resized_faceImage.shape
faceImage.shape

# Load the Sunglass image with Alpha channel
glassPNG = cv2.imread('b.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")

# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]

# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');

# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[135:185,130:300]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])

# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[135:185,130:300]

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")

plt.figure(figsize=[20,20]);

```

## Output:
<img width="520" height="505" alt="Screenshot 2026-11-18 213707" src="https://github.com/user-attachments/assets/f8335900-fb26-4108-b268-408530abdfa0" />

<img width="672" height="324" alt="Screenshot 2026-11-18 213716" src="https://github.com/user-attachments/assets/e307df1b-66cb-4b3b-8cf2-c87c0c84a3e4" />

<img width="1225" height="258" alt="Screenshot 2026-11-18 220039" src="https://github.com/user-attachments/assets/e9c2276a-0160-4b21-97a3-8a6557215447" />

<img width="530" height="478" alt="Screenshot 2026-11-18 213928" src="https://github.com/user-attachments/assets/aa225e27-3aac-4cba-807b-80f630d82d92" />

<img width="1256" height="185" alt="Screenshot 2026-11-18 213941" src="https://github.com/user-attachments/assets/19a71a21-cd6b-42b7-8981-50ee5c5ba4a5" />

<img width="1229" height="746" alt="image" src="https://github.com/user-attachments/assets/057c8d94-ceed-4697-94cb-6f870afce753" />





