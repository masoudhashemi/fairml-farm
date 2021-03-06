# fairml-farm
This repository contains a collection of implementations of fair ML algorithms.
The goal is to have all of these approaches concentrated in the same place and directly comparable to each other, so that we can more quickly compare new approaches against previous ones, and compare and contrast the different algorithms.
The ultimate goal is to provide a playground to help build intuition about different definitions and approaches to fairness.

This is very much a work in progress, and I would love your feedback!
 (On desired features, explanations, or even code quality.)

## Overview
The main components of this project are:

* **Implementations:** a set of implementations of popular fairness approaches, which we'll update periodically
* **Datasets:** functions to easily load popular fairness datasets
	* **Synthetic Datasets:** an interface for creating synthetic fairness datasets (w/ built-in visualizations)
* **Evaluation:** Side-by-side comparisons of different algorithms' behaviors across a slew of fairness metrics

For now, we'll be dealing exclusively with the much-studied problem of group-fairness in classification:

Given data `X`, labels `Yϵ{0, 1}`, and protected attribute `Aϵ{0,1}`, we want to construct some classifier `c(X)` which is both predictive of `Y`, and "fair" with respect to the two groups `A=0` and `A=1`.
 There are many definitions for such fairness, and each algorithm may be tuned to a different definition.
For an introduction to many of these approaches, check out [this page](https://speak-statistics-to-power.github.io/fairness/).

## Getting started

This project runs in Python 3 (recommended 3.5 or later).

To install the various dependencies, navigate to the project's root directory, and call:
```bash
python setup.py install
```
Running all the project's code requires
 `numpy`, `tensorflow>=1.4.0`, `matplotlib>=2.1.1`, `pandas>=0.21.0`, and `sklearn`.
 (The previous command will install these if you don't have them yet).

It's easy to modify the code to add in your own fairness algorithms or datasets.
Just check out [this short guide](how_to_add.md) on where you'll need to modify the code.  
Also, consider submitting a pull-request to add your own stuff in!
 That way, we can build up a comprehensive set of implementations!

### Running the examples

Call `evaluate.py` to watch the training dynamics of a particular fairness algorithm.

Call `train_and_compare.py` to see a side-by-side performance comparison
 of a simple NN with different fairness regularizers. (Be sure to open your local
 [Tensorboard](http://0.0.0.0:6006/)!) The result should look like this:

![legend](/results/paritynn_tensorboardlegend.png) ![tsbd1](/results/paritynn_tensorboard1.png)

![tsbd2](/results/paritynn_tensorboard2.png) ![tsbd3](/results/paritynn_tensorboard3.png)

('simplenn' is a regular neural network; each of the other networks is trained with an added loss penalty for violating a certain type of fairness.
cpe = calibration parity, dpe = demographic parity, fnpe = false negative parity, fppe = false positive parity.)

You can also check out `train_toy_datasets.py` to view how linear classifiers make fair decisions on toy data.
For example, below we see how the decision boundary shifts as we change the hyperparameter weighting classification loss vs. demographic parity fairness loss.
![Results of changing demographic parity error scalar](results/toy_decision_varying_dpe.png)
(The two demographic groups are red and blue, with different local concentrations. Green is a positive sample, while magenta is negative.
 This example is inspired by [Fig. 1 from Zafar et al](https://people.mpi-sws.org/~mzafar/papers/preferential_fairness_nips2017.pdf#page=2).)

You can observe the behavior for different fairness losses, or change the generated distribution being learned.

## Future work
* Add module on fair representation learning algorithms
* Add easy way to add new fairness metrics (non-TF dependent) and add to docs

