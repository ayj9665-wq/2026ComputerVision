# Assignment 02 & 03 : Binarization, Arithmetic / Logical Operations, Dilation & Erosion

Basic grayscale image processing with OpenCV: four thresholding methods on the rice image,
pixel-wise arithmetic and logical operations on two bolt images, and dilation / erosion with
four small structuring elements on a photo and a text image.

## Files

| Path | Content |
|---|---|
| `CV_Assignment_02_03.ipynb` | Notebook, with all outputs saved |
| `images/01_arithmetic/` | `A_bolt.png`, `B_bolt.png` (Week 2-2, slides 14 and 16) |
| `images/02_morphology/` | `parrots_gray.png`, `beatles.png` (text image) |
| `images/03_binarization/` | `rice_gray.png`, `rice_binary_ref.png` (Week 1-2, slide 20) |
| `requirements.txt` | Python packages used by the notebook |

## Contents

| Section | Topic | Details |
|---|---|---|
| 02 | Binarization | Global (T=127), adaptive mean / Gaussian (block 31, C=-5), Otsu, minimum error (Kittler-Illingworth, implemented from the histogram) |
| 03 | Arithmetic | Addition, subtraction (+ `absdiff`), multiplication (mask ROI), division (background correction of the rice image before Otsu) |
| 04 | Logical | AND, OR, NOR, NOT on the binarized bolt images, with a truth table |
| 05 | Dilation | Vertical 3x1, horizontal 1x3, square 3x3, circle/disk 3x3 (cross) with same-size padding; 7x7 toy array, parrots, text |
| 06 | Erosion | Same four structuring elements and images as 05 |

## Run

```bash
cd Assignment02_03
pip install -r requirements.txt
jupyter notebook CV_Assignment_02_03.ipynb
```

The notebook reads `images/` relative to the working directory, so start Jupyter from `Assignment02_03/`.
If `images/` is missing it extracts `images.zip` instead, which is the easier way to upload the images on Google Colab.
The saved outputs were produced on Google Colab.

## Results

### Binarization (rice_gray.png)

| Method | Threshold | Foreground (%) |
|---|---|---|
| Global | 127 | 26.97 |
| **Otsu** | **131** | **25.94** |
| Minimum Error | 157 | 19.38 |

### Dilation / Erosion

Parrots: change of mean intensity (original 109.13, resized to 640x428).
Text: change of bright pixels (> 128, original 43,339).

| Structuring element | Parrots dilation | Parrots erosion | Text dilation | Text erosion |
|---|---|---|---|---|
| Vertical 3x1 | +2.55 | -2.55 | +58.6% | -54.8% |
| Horizontal 1x3 | +2.91 | -2.91 | +69.9% | -72.4% |
| Square 3x3 | +5.28 | -5.26 | +128.4% | -99.8% |
| Circle/disk 3x3 | +3.90 | -3.89 | +101.5% | -94.4% |

The strokes in `beatles.png` are thinner than the square element, so erosion with it removes almost all text (-99.8%).
[Assignment 03](../Assignment03/) repeats the morphology on a zoomed text image with wider strokes and adds opening and closing.
