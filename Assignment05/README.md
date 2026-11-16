# Assignment 05 : Linear Classifier with Random Weights on CIFAR-10

How a linear classifier $f(x) = Wx + b$ computes class scores and predictions with randomly initialized weights. The model is not trained.

- $W$ : 10 x 3072 from $N(0, 0.01^2)$ with seed 1, $b$ : zeros
- Class scores and predictions for 10 example images (first test image of each class)
- Multiclass SVM hinge loss, checked with the lecture example ($L$ = 5.27)
- Softmax : scores vs probabilities, every row sums to 1
- Correct and misclassified examples
- Each row of $W$ shown as a 32 x 32 x 3 image

## Files

| Path | Content |
|---|---|
| `CV_Assignment_05.ipynb` | Notebook, with all outputs saved |
| `requirements.txt` | Python packages used by the notebook |

The dataset is the same as in Assignment 04 and is not copied again : the notebook reads `../Assignment04/cifar-10-batches-py/test_batch`.

## Run

```bash
cd Assignment05
pip install -r requirements.txt
jupyter notebook CV_Assignment_05.ipynb
```

Start Jupyter from `Assignment05/` so the relative data path works. The notebook runs in a few seconds.
The saved outputs were produced with Python 3.9.6.

## Results

| | Value |
|---|---|
| Average SVM loss (10 images) | 9.189 (about 9 is expected for an untrained model) |
| Softmax probabilities | 0.039 ~ 0.180, every row sums to 1 |
| Correct among the 10 examples | 1 (airplane) |
| Correct on all 10,000 test images | 1013 (about chance level, 10%) |

## Dataset

Alex Krizhevsky, *Learning Multiple Layers of Features from Tiny Images*, 2009.
https://www.cs.toronto.edu/~kriz/cifar.html
