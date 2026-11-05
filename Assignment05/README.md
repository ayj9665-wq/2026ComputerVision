# Assignment 05 : Linear Classifier on CIFAR-10

Linear classifier $f(x, W) = Wx + b$ on raw CIFAR-10 pixels (3072-dim), trained with SVM (hinge) loss and Softmax (cross-entropy) loss
by mini-batch gradient descent, written with NumPy only.
The learning rate of each loss is selected by 5-fold cross-validation on the 50,000 train images (same folds as Assignment 04).
The 10,000 test images are used only for the final evaluation.

## Files

| Path | Content |
|---|---|
| `CV_Assignment_05.ipynb` | Notebook, with all outputs saved |
| `requirements.txt` | Python packages used by the notebook |

The dataset is the same as in Assignment 04 and is not copied again : the notebook reads `../Assignment04/cifar-10-batches-py/`.

## Contents

| Section | Topic | Details |
|---|---|---|
| 01 | Data preparation | Pixels scaled to [0, 1], mean train image subtracted |
| 02 | Linear classifier | $W$ 10 x 3072, $b$ 10, 10 class scores per image, 30,730 parameters |
| 03_1 | SVM loss | $\sum_{j \neq y_i} \max(0, s_j - s_{y_i} + 1)$, lecture example : $L_i$ = 2.9 / 0 / 12.9, $L$ = 5.27 |
| 03_2 | Softmax function | exp -> normalize, lecture example : 0.13 / 0.87 / 0.00 |
| 03_3 | Softmax loss | $-\log P(\text{correct class})$, compared with the SVM loss |
| 03_4 | Loss with random $W$ | SVM ≈ 9, Softmax ≈ $\log 10$ = 2.303 |
| 04 | Training | Gradients of both losses, mini-batch gradient descent (200 images, 10 epochs), 5-fold CV over $lr$ = 0.0001 ~ 1 |
| 05 | Test evaluation | Scores, per-class report, confusion matrix, rows of $W$ shown as class templates |
| 06 | Comparison | SVM vs Softmax vs KNN of Assignment 04 |

## Run

```bash
cd Assignment05
pip install -r requirements.txt
jupyter notebook CV_Assignment_05.ipynb
```

The notebook reads `../Assignment04/cifar-10-batches-py/` relative to the working directory, so start Jupyter from `Assignment05/`.
The whole notebook runs in about 5 min, most of it the 5-fold cross-validation (about 30 s per learning rate, see 04_1).
The saved outputs were produced with Python 3.13.9.

## Results

| Model | Best setting (5-fold) | 5-fold Accuracy | Test Accuracy | Test Precision | Test Recall | Test F1 | Test time |
|---|---|---|---|---|---|---|---|
| **Softmax** | **lr = 0.1** | **0.4076 ± 0.0053** | **0.4107** | **0.4112** | **0.4107** | **0.4078** | **0.05 s** |
| SVM | lr = 0.01 | 0.3944 ± 0.0052 | 0.3971 | 0.3986 | 0.3971 | 0.3958 | 0.06 s |
| KNN L1 (Assignment 04) | k = 5 | 0.3791 ± 0.0030 | 0.3921 | 0.4560 | 0.3921 | 0.3890 | 302 s |

The linear classifier is about as accurate as KNN, but keeps 30,730 parameters instead of the whole train set
and classifies the test set in 0.05 s instead of 302 s.

## Dataset

Alex Krizhevsky, *Learning Multiple Layers of Features from Tiny Images*, 2009.
https://www.cs.toronto.edu/~kriz/cifar.html
