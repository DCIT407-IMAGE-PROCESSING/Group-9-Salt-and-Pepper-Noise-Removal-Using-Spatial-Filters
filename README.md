# Adaptive Spatial Filtering and Performance Evaluation

---

## Adaptive Spatial Filter

An adaptive spatial filter was implemented to selectively replace corrupted pixels caused by salt-and-pepper noise.

Salt-and-pepper noise introduces extreme intensity values (0 or 255) into an image. The adaptive filter operates by identifying these corrupted pixels and replacing them using statistical information from their local neighborhood.

### Method Description

- Each pixel is examined individually.
- If the pixel value is **0 or 255**, it is considered corrupted.
- A fixed-size window (e.g., 5×5) is extracted around the pixel.
- Neighboring pixels that are **not equal to 0 or 255** are considered valid.
- The corrupted pixel is replaced with the **mean of the valid neighboring pixels**.
- If no valid pixels exist in the window, the original value is retained.

### Purpose

This approach attempts to:

- Preserve uncorrupted pixels.
- Avoid unnecessary smoothing.
- Correct only those pixels that are truly corrupted.
- Maintain structural information in the image.

Although adaptive filtering is theoretically advantageous for impulse noise, its effectiveness depends heavily on window size and noise density.

---

## 3. Evaluation Metrics

Restoration performance was evaluated using two widely accepted image quality metrics:

- Peak Signal-to-Noise Ratio (PSNR)
- Structural Similarity Index (SSIM)

---

### Peak Signal-to-Noise Ratio (PSNR)

PSNR measures pixel-level reconstruction quality by comparing the restored image with the original clean image.

It is derived from the Mean Squared Error (MSE) between two images.

Higher PSNR values indicate lower reconstruction error and better restoration quality.

#### General Interpretation of PSNR

- **< 20 dB** → Poor quality  
- **20–30 dB** → Acceptable quality  
- **30–40 dB** → Very good quality  
- **> 40 dB** → Excellent quality  

---

### Structural Similarity Index (SSIM)

SSIM measures perceptual similarity between two images by comparing:

- Luminance
- Contrast
- Structural information

Unlike PSNR, SSIM considers human visual perception and image structure.

#### SSIM Range

- **0** → Completely different images  
- **1** → Identical images  

Higher SSIM values indicate better structural preservation and perceptual similarity.

---

## Results Summary

Average performance across the dataset:

| Method   | PSNR (dB) | SSIM   |
|----------|-----------|--------|
| Median   | 33.20     | 0.9241 |
| Adaptive | 22.56     | 0.6510 |

---

## Interpretation of Results

- The **Median Filter** achieved significantly higher PSNR and SSIM values.
- The **Adaptive Filter** performed moderately but did not surpass the median approach.
- Median filtering demonstrated strong structural preservation and effective noise suppression.

These results indicate that the classical median filter remains highly effective for salt-and-pepper noise removal, particularly at moderate noise levels.

---

## Key Learnings

- Classical spatial filters remain highly effective for salt-and-pepper noise removal.
- Median filtering is particularly robust for impulse noise.
- Adaptive filters require careful design and tuning to outperform optimized classical methods.
- Proper dataset alignment (matching filenames and dimensions) is critical for valid evaluation.
- Objective metrics such as PSNR and SSIM are essential for fair and scientific comparison.

---

## How to Run the Project

### 1. Install Dependencies

Ensure Python 3.12 is installed.

Install required libraries in the project root directory:

```
pip install -r requirements.txt
```

---

### 2. Prepare Dataset

Place:

Noisy grayscale images in:
```
data\noisy
```

Corresponding clean images in:
```
data\cleaned
```


Ensure filenames match (excluding the `noisy_` prefix if applicable).

---

### 3. Run the Notebook

Navigate to the `notebooks` directory:

```
cd notebooks
```

Launch Jupyter:

```
jupyter notebook
```

Open:

```
salt_pepper_denoising.ipynb
```

Run all cells sequentially.

Cleaned images will automatically be saved to:

```
data/cleaned/
```


---

## Conclusion

This project investigated the effectiveness of spatial filtering techniques for removing salt-and-pepper noise from grayscale images.

Two approaches were implemented and evaluated:

- Classical Median Filter
- Adaptive Spatial Filter

Experimental results demonstrated that the **Median Filter significantly outperformed** the implemented Adaptive Filter across the dataset.

The Median Filter achieved:

- **Average PSNR:** 33.20 dB  
- **Average SSIM:** 0.9241  

In contrast, the Adaptive Filter achieved:

- **Average PSNR:** 22.56 dB  
- **Average SSIM:** 0.6510  

Although adaptive filtering is theoretically designed to selectively correct corrupted pixels, the simplified implementation used in this project was less effective than the optimized median filtering algorithm provided by OpenCV.

These findings highlight that classical spatial filters remain highly competitive and robust solutions for impulse noise removal, particularly at moderate noise densities.

---

## Future Work

- Implement adaptive window expansion strategies.
- Evaluate performance at varying noise densities.
- Extend experiments to colored images.
- Compare spatial filters with CNN-based denoising methods.
- Incorporate error map visualization and histogram analysis for deeper evaluation.
