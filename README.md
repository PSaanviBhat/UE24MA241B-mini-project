# Image Encryption Tool Using Linear Algebra

## Overview

This project is a Python-based image encryption system that secures full-color RGB images using pure linear algebra. The encryption pipeline transforms an image into a numerical tensor, applies matrix-based scrambling through multiplication with a dynamically generated invertible key matrix, and restores the original image via matrix inversion. The approach guarantees mathematically lossless decryption when the correct key is used.

---

## Features

- Full RGB image encryption and decryption support  
- Lossless restoration through inverse matrix operations  
- Automatic zero-padding for arbitrary image dimensions  
- Side-by-side visualization of:
  - Original Image  
  - Encrypted Image (Static Noise Representation)  
  - Decrypted / Restored Image  

---

## System Architecture

### Image Preprocessing Module
- Uses Pillow (PIL) to load image files  
- Converts images into 3D NumPy tensors of shape:  
  `Height × Width × 3`

### Key Generation & Validation Engine
- Dynamically generates random square key matrices  
- Validates invertibility by checking:  
  `det(Key) ≠ 0`
- Regenerates until a valid key is produced  

### Cryptography Subsystem
- Flattens RGB tensor into 1D numerical vector  
- Computes required zero-padding dynamically  
- Reshapes padded vector into matrix blocks compatible with key size  
- Performs encryption via matrix multiplication  
- Performs decryption via inverse matrix multiplication  
- Reconstructs original 3D RGB tensor  

### Visualization Engine
- Uses Matplotlib for rendering  
- Normalizes encrypted floating-point noise for safe visualization  
- Clips decrypted output to `[0,255]` and casts to `uint8`  

---

## Mathematical Foundation

### Image Representation
A digital RGB image is represented as a 3D tensor:

`I ∈ R^(H × W × 3)`

Where:
- `H` = Height  
- `W` = Width  
- `3` = RGB Channels  

---

### Encryption Formula

`E = I × K`

Where:
- `E` = Encrypted Matrix  
- `I` = Flattened Image Matrix  
- `K` = Invertible Key Matrix  

---

### Decryption Formula

`R = E × K⁻¹`

Where:
- `R` = Restored Image Matrix  
- `K⁻¹` = Inverse of Key Matrix  

---

### Invertibility Requirement

The key matrix must satisfy:

`det(K) ≠ 0`

A zero determinant implies the matrix is singular and non-invertible, making decryption mathematically impossible.

---

## Challenges Faced and Solutions

### Matrix Invertibility
- Implemented determinant validation to ensure only invertible keys are used  

### Data Overflow Prevention
- Converted image data from `uint8` to floating-point before encryption  
- Applied clipping during decryption to restore valid pixel ranges  

### RGB Tensor Handling
- Managed 3D tensor flattening and reconstruction  
- Computed exact padding requirements for arbitrary dimensions  

### Matplotlib Rendering Constraints
- Normalized encrypted noise to `[0,1]` for display  
- Explicitly cast decrypted output to `uint8` before rendering  

---

## Tech Stack

- **Python**
- **NumPy**
- **Pillow (PIL)**
- **Matplotlib**

---

## Output Example

The tool generates a dashboard displaying:

1. Original Image  
2. Encrypted Noise Representation  
3. Perfectly Restored Decrypted Image  

---

## Directory Structure

```bash
UE24MA241B-mini-project/
│── encrypt.ipynb        # Main notebook containing encryption/decryption pipeline
│── sample.png           # Input sample image
│── output.png           # Generated encrypted/decrypted visualization output
│── requirements.txt     # Python dependencies
│── README.md
 ```

--- 

## Installation and running the project

```bash

git clone https://github.com/PSaanviBhat/UE24MA241B-mini-project
cd UE24MA241B-mini-project
pip install -r requirements.txt
jupyter notebook encrypt.ipynb

```

---

## Conclusion

This project demonstrates the practical application of linear algebra in cryptography, showcasing how matrix transformations and inversion can be used to build a reversible image encryption system for secure visual data transmission and storage.

---

## License

This project is licensed under the MIT License.

---

## Team details
 - P Saanvi [PES1UG24AM905]
 - Sonia Sharma [PES1UG24AM904]
 - Kasissnu Ssinha [PES1UG24AM130]
 - Kaustubh Akash [PES1UG24AM131]
 
