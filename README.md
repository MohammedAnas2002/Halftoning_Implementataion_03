# Halftoning_Implementataion_03
# Halftone Image Quality Evaluation

This repository contains an **experimental study on how internal parameters influence halftone image quality**, both quantitatively and visually.  

---

## 🔹 Goal
To evaluate how different halftone generation parameters affect image quality using **quantitative metrics** (PSNR, SSIM) and **visual inspection**.

---

## 🔹 Parameters Studied

| Method             | Parameter       | Description                                    |
|-------------------|----------------|-----------------------------------------------|
| Global Thresholding | Threshold Value | Single global intensity cutoff               |
| Ordered Dithering   | Matrix Size     | Size of dithering matrix (2×2, 4×4, …)      |
| Error Diffusion     | Kernel Type     | Diffusion algorithm (FS, Jarvis, Stucki, Sierra, Atkinson) |

**Metrics Used:**  
- **PSNR (Peak Signal-to-Noise Ratio):** Pixel-level fidelity  
- **SSIM (Structural Similarity Index):** Perceptual similarity  

---

## 🔹 Experimental Setup

- **Environment:** Python (`NumPy`, `PIL`, `Matplotlib`, `scikit-image`)  
- **Platform:** Jupyter Notebook  
- **Test Image:** `apple.png` resized to 512×512  
- **Evaluation Metrics:** PSNR and SSIM  

---

## 🔹 Global Thresholding – Quantitative Results

| Threshold | PSNR | SSIM |
|-----------|------|------|
| 64        | 7.04 | 0.446 |
| 128       | 8.85 | 0.318 |
| 192       | 6.65 | 0.059 |

<img width="547" height="272" alt="image" src="https://github.com/user-attachments/assets/5a34b1f2-cb9c-45e3-a0b0-c97fe5e645a2" />


**Observations:**  
- Lower threshold (64) → higher SSIM, better perceptual detail in darker regions  
- Threshold 128 → balanced PSNR and moderate structural similarity  
- Threshold 192 → washes out image details  

**✅ Best Threshold:** **128**

---

## 🔹 Ordered Dithering – Quantitative Results

| Matrix Size | PSNR | SSIM |
|------------|------|------|
| 2×2        | 6.52 | 0.031 |
| 4×4        | 6.68 | 0.036 |
| 8×8        | 6.68 | 0.036 |
| 16×16      | 6.69 | 0.036 |

<img width="517" height="268" alt="image" src="https://github.com/user-attachments/assets/68bc9caf-7e54-49aa-b2c7-f414a42e73f3" />



**Observations:**  
- Increasing matrix size smooths tone transitions  
- Visual grain decreases with larger matrices  
- Improvements plateau beyond 8×8  

**✅ Optimal Matrix Size:** **4×4 or 8×8**

---

## 🔹 Error Diffusion – Quantitative Results

| Kernel Type      | PSNR | SSIM |
|-----------------|------|------|
| Floyd–Steinberg  | 6.70 | 0.039 |
| Jarvis           | 6.76 | 0.051 |
| Stucki           | 6.74 | 0.047 |
| Sierra           | 6.75 | 0.049 |
| Atkinson         | 7.71 | 0.120 |

<img width="483" height="297" alt="image" src="https://github.com/user-attachments/assets/a1330324-595a-42d5-93d1-d4ab04c729d4" />


**Observations:**  
- Atkinson → highest SSIM, smoother tonal transitions, better edge preservation  
- Jarvis and Stucki → strong fine-grained diffusion  
- Floyd–Steinberg → computationally efficient, acceptable quality  

**✅ Best Performer:** **Atkinson Kernel**

---

## 🔹 PSNR Comparison

- Ordered dithering → consistent PSNR  
- Error diffusion → slightly higher PSNR for Atkinson kernel  
- Threshold-based methods → strong variation with intensity  

<img width="694" height="392" alt="image" src="https://github.com/user-attachments/assets/0ddb0756-4fe6-4179-9ba8-9969e55cf18a" />  
<img width="679" height="375" alt="image" src="https://github.com/user-attachments/assets/ce6bfe91-693c-4b06-bf5a-d8725a2d0c27" />  
<img width="679" height="375" alt="image" src="https://github.com/user-attachments/assets/ce6bfe91-693c-4b06-bf5a-d8725a2d0c27" />  

---

## 🔹 SSIM Comparison

- Atkinson kernel → superior structural retention  
- Threshold 64 and ordered dithering (8×8) → smoother perceptual structure  
<img width="694" height="392" alt="image" src="https://github.com/user-attachments/assets/52d5a776-cde8-4fff-bbf8-87576f12a58c" />
<img width="679" height="375" alt="image" src="https://github.com/user-attachments/assets/381e4bed-2c55-4e63-bde6-2e07ea0f1cf4" />
<img width="662" height="372" alt="image" src="https://github.com/user-attachments/assets/cb83de6e-b903-43b1-887a-108e4e66dda2" />
---

## 🔹 Visual Results
<img width="591" height="291" alt="image" src="https://github.com/user-attachments/assets/b2c3fb74-2a8f-4c38-a288-64f3429148ad" /> <img width="590" height="327" alt="image" src="https://github.com/user-attachments/assets/c9716c94-2860-49f5-96ab-b785f3a61d3f" />  <img width="591" height="319" alt="image" src="https://github.com/user-attachments/assets/2082246d-3a15-4f06-9a82-db43f3134e25" />
The figures shows the global threshold experiments
<img width="504" height="220" alt="image" src="https://github.com/user-attachments/assets/c26b8d7a-79f2-45ce-8df0-e0dc260d0b25" />




 

- **Global Threshold:** 64, 128, 192  
- **Ordered Dithering:** 2×2, 4×4, 8×8, 16×16  
- **Error Diffusion:** FS, Jarvis, Stucki, Sierra, Atkinson  

**Observations:**  
- Ordered and error diffusion methods → more natural tonal transitions  
- Larger matrices and advanced kernels → reduced visible artifacts  

*🖼 Add a side-by-side image grid for visual comparison.*

---

## 🔹 Analytical Summary

| Method             | Best Parameter | Result |
|-------------------|----------------|--------|
| Global Thresholding | 128            | Balanced PSNR and visibility |
| Ordered Dithering   | 8×8            | Fine tone rendering |
| Error Diffusion     | Atkinson       | Best overall quality (SSIM = 0.120) |

**Conclusion:**  
- Proper parameter tuning significantly affects halftone quality.  
- **Diffusion kernel type** and **threshold selection** are crucial for optimal results.
