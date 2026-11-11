# Assignment 05 : Linear Classifier on CIFAR-10

Linear classifier $f(x, W) = Wx + b$ on raw CIFAR-10 pixels (3072-dim) with SVM (hinge) loss and Softmax (cross-entropy) loss, using scikit-learn.

- SVM : `SGDClassifier(loss='hinge')`, stochastic gradient descent for 10 epochs
- Softmax : `LogisticRegression`, lbfgs for 100 iterations

The regularization strength is chosen by 5-fold cross-validation (`GridSearchCV`, same folds as Assignment 04).
The 10,000 test images are used only for the final evaluation.

## Files

| Path | Content |
|---|---|
| `CV_Assignment_05.ipynb` | Notebook, with all outputs saved |
| `requirements.txt` | Python packages used by the notebook |

The dataset is the same as in Assignment 04 and is not copied again : the notebook reads `../Assignment04/cifar-10-batches-py/`.

## Run

```bash
cd Assignment05
pip install -r requirements.txt
jupyter notebook CV_Assignment_05.ipynb
```

Start Jupyter from `Assignment05/` so the relative data path works.
The whole notebook takes about 15 min, mostly the 5-fold CV of `LogisticRegression`.
The saved outputs were produced with Python 3.9.6.

## Results

| Model | Best setting (5-fold) | 5-fold Accuracy | Test Accuracy | Test Precision | Test Recall | Test F1 | Test time |
|---|---|---|---|---|---|---|---|
| **Softmax** | **C = 0.001** | **0.4134 ± 0.0048** | **0.4177** | **0.4139** | **0.4177** | **0.4147** | **0.20 s** |
| SVM | alpha = 0.001 | 0.3887 ± 0.0048 | 0.3942 | 0.3980 | 0.3942 | 0.3945 | 0.52 s |
| KNN L1 (Assignment 04) | k = 5 | 0.3791 ± 0.0030 | 0.3921 | 0.4560 | 0.3921 | 0.3890 | 302 s |

## Dataset

Alex Krizhevsky, *Learning Multiple Layers of Features from Tiny Images*, 2009.
https://www.cs.toronto.edu/~kriz/cifar.html
