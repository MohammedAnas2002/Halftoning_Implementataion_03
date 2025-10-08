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

*📊 Include a bar chart here comparing PSNR values for all methods.*

---

## 🔹 SSIM Comparison

- Atkinson kernel → superior structural retention  
- Threshold 64 and ordered dithering (8×8) → smoother perceptual structure  

*📊 Include a bar chart here for SSIM comparison.*

---

## 🔹 Visual Results

**Sample outputs:**  

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
