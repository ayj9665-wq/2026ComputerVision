# Assignment 04 : KNN on CIFAR-10

KNN classifier on raw CIFAR-10 pixels (3072-dim) with L1 (`manhattan`) and L2 (`euclidean`) distance.
`k` and the distance metric are selected by 5-fold cross-validation on the 50,000 train images.
The 10,000 test images are used only for the final evaluation.

## Files

| Path | Content |
|---|---|
| `CV_Assignment_04.ipynb` | Notebook, with all outputs saved |
| `cifar-10-batches-py/` | CIFAR-10 python version (`data_batch_1` ~ `5`, `test_batch`, `batches.meta`) |
| `requirements.txt` | Python packages used by the notebook |

`cifar-10-batches-py/` is the extracted content of the official `cifar-10-python.tar.gz`
(MD5 `c58f30108f718f92721af3b95e74349a`). The archive itself (163 MB) is not included
because GitHub blocks files larger than 100 MiB; every extracted file is identical to the archive's content.

## Run

```bash
cd Assignment04
pip install -r requirements.txt
jupyter notebook CV_Assignment_04.ipynb
```

The notebook reads `cifar-10-batches-py/` relative to the working directory, so start Jupyter from `Assignment04/`.
Most of the run time is the L1 cross-validation (about 4 min per fold, see 04_1 in the notebook).
The saved outputs were produced with Python 3.9.6.

## Results

| Metric | Best k (5-fold) | 5-fold Accuracy | Test Accuracy | Test Precision | Test Recall | Test F1 |
|---|---|---|---|---|---|---|
| **L1** | **5** | **0.3791 ± 0.0030** | **0.3921** | **0.4560** | **0.3921** | **0.3890** |
| L2 | 5 | 0.3486 ± 0.0029 | 0.3556 | 0.4367 | 0.3556 | 0.3452 |

## Dataset

Alex Krizhevsky, *Learning Multiple Layers of Features from Tiny Images*, 2009.
https://www.cs.toronto.edu/~kriz/cifar.html
