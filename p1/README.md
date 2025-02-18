### Recurrent Neural Networks

Important note 1: There'll be no focus on organizing code. The goal of these exercises is to implement and understand how these models work not to create well-structured libraries. So some exercises might even be done in one python file.

Important note 2: This is numerical code i.e. the central goal of our code is to compute a bunch of numbers. It is hard to debug this kind of code unless you have an expectation of what output you'll get (for example, in scientific computing i.e. physics, chemistry, biology etc. and even in these fields, debugging is tricky). Using tensor shapes and playing around with small examples in ipython/jupyter is crucial. Please do not write code and hope it'll work - be paranoid about checking.

Suggested reading order:
* rnn.py
* test_rnn.py
* train.py

Reference: [RNN paper](https://apps.dtic.mil/dtic/tr/fulltext/u2/a164453.pdf)

Consider the following problem: Given an array of numbers, compute the sum. A basic loop would look like:

```
data = [...]
sum = 0

for d in data:
    sum = sum + d
```

This can be generalized to:

```
data = [...]
sum = 0

for d in data:
    sum = f(d, sum)
```

where ```f(d, sum) = lambda d, sum: d + sum```.

This version makes a few things explict:
* data is an array of numbers
* the variable sum represents persistent state
* f() updates the state (sum) based on the current state value and the current data value (variable d)

For a neural network, data and state are vectors. Another primitive operation in doing a linear projection and applying a non-linearity i.e.

```python
import numpy as np

data = Vec(...)
sum = Vec(...)

for d in data:
    sum = $\sigma$(W d + U sum + b)
```

where $\sigma$ is a general non-linearity (relu, sigmoid, pick your choice), W and U are matrices acting on d and sum respectively and b is a bias vector.

This loop is a recurrent neural network (RNN).

General note:
* If you are used to thinking of neural networks as multi-layer perceptrons, this might look funny. You should instead think of neural networks as computations that take vectors (or tensors) as inputs and apply a sequence of differentiable operations.

Exercises:
1. Generate a train and test set of sequences of numbers of fixed length (say 20). Compute the train and test mean sequared error losses.
2. Train on length L and evaluate on tests sets of various lengths (both < L as well as > L). What happens to test performance as a function of L?
3. On the training set where gradients are computed, plot the distribution of gradients across epochs and for each iteration (is this possible in PyTorch?)
4. Pick a realistic sequence prediction task and train an RNN. Papers are a good place to look for examples. Please, no stock prediction based on a single time-series - no one on Wall Street does this - see this [book](https://press.princeton.edu/books/paperback/9780691134796/asset-price-dynamics-volatility-and-prediction) for a better introduction to understanding asset prices.