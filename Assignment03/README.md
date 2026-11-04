# Assignment 03 : Morphology on a Text Image

Dilation, erosion, opening and closing on an English text image with four structuring elements,
followed by two noise experiments: opening against salt noise and closing against pepper noise.

## Files

| Path | Content |
|---|---|
| `CV_Assignment_03.ipynb` | Notebook, with all outputs saved |
| `beatles_zoom.png` | Text image (173x615, bright letters on a dark background, strokes ~4 px) |
| `requirements.txt` | Python packages used by the notebook |

## Contents

| Section | Topic | Details |
|---|---|---|
| 02 | Dilation | Vertical 3x1, horizontal 1x3, square 3x3, circle/disk 3x3 (cross) with same-size padding; 7x7 toy array, then the text |
| 03 | Erosion | Same four structuring elements; toy array is a 5x5 block plus one isolated dot |
| 04 | Opening / Closing | Opening = erosion -> dilation, closing = dilation -> erosion, shown next to plain erosion / dilation |
| 05 | Noise | Opening removes salt noise on the background, closing fills pepper holes in the strokes |
| 06 | Comparison | All four operations with the square 3x3 element |

## Run

```bash
cd Assignment03
pip install -r requirements.txt
jupyter notebook CV_Assignment_03.ipynb
```

The notebook reads `beatles_zoom.png` relative to the working directory, so start Jupyter from `Assignment03/`.
The saved outputs were produced on Google Colab.

## Results

Change of bright pixels (> 128) against the original (20,754).

| Structuring element | Dilation | Erosion | Opening | Closing |
|---|---|---|---|---|
| Vertical 3x1 | +32.1% | -32.0% | -2.5% | +2.4% |
| Horizontal 1x3 | +37.4% | -38.0% | -1.7% | +5.4% |
| Square 3x3 | +70.0% | -68.9% | -8.4% | +8.4% |
| Circle/disk 3x3 | +53.4% | -52.7% | -2.1% | +5.3% |

Dilation and erosion change the letter weight a lot, while opening and closing stay close to the original:
they filter by size without rescaling the strokes.

| Experiment (square 3x3) | Noise | Result |
|---|---|---|
| Opening | Salt, 2% of background (1,636 specks) | **95.9%** removed, strokes kept at 100.3% of the noise-free opening |
| Closing | Pepper, 10% of strokes (2,054 holes) | **84.0%** filled |
