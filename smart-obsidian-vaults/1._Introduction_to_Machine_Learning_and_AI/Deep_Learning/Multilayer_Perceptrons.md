---
status: finished
tags:
  - machine-learning
  - deep-learning
date: 2026-04-14T00:00:00.000Z
---

# Multilayer Perceptrons

## Introduction
A Multilayer Perceptron (MLP) is a foundational deep neural network architecture consisting of multiple layers of neurons—an input layer, one or more hidden layers, and an output layer—where each layer is fully connected to the adjacent layers. Hidden layers allow the model to learn intermediate representations, overcoming the limitations of simpler linear models. MLPs act as universal approximators and represent a core architecture in [[Deep_Learning_Overview|Deep Learning]] (see also [[AI_ML_DL_Overview]]).

## Mathematical Foundation & Activation Functions
The essential characteristic of an MLP is the use of non-linear **activation functions**. Without them, stacking multiple layers would be mathematically equivalent to a single linear layer, defeating the purpose of depth. This non-linearity is what enables MLPs to approximate complex functions.
Common activation functions include:
- **ReLU (Rectified Linear Unit)**: 
$$ReLU(x) = \max(0, x)$$
This is the most popular choice due to its simplicity and its ability to mitigate the vanishing gradient problem.
- **Sigmoid**: 
$$\sigma(x) = 1 / (1 + \exp(-x))$$
Squashes inputs to the range $(0, 1)$. While historically popular, it is prone to causing vanishing gradients.
- **Tanh (Hyperbolic Tangent)**: 
$$tanh(x) = (1 - \exp(-2x)) / (1 + \exp(-2x))$$
Squashes inputs to $(-1, 1)$ and is point-symmetric about the origin.

## The Training Process
### Forward and Backward Propagation
- **Forward Propagation (Feedforward)**: The process where input data travels through the network's layers to produce a prediction. For each neuron $j$ in a layer, a weighted sum of inputs $x_i$ from the previous layer (plus a bias $b_j$) is calculated:
$$a_j = \sum_i (w_{ji} \cdot x_i) + b_j$$
An activation function $f$ is then applied to introduce non-linearity and produce the neuron's output:
$$y_j = f(a_j)$$
This sequential calculation continues from the input layer to the output layer.
- **Backpropagation (Backward Pass)**: An algorithm used to train the network by minimizing the error between predicted and actual outputs. The process involves:
  - **Error Calculation**: A loss function, such as Mean Squared Error (MSE), measures the difference between target values $t$ and predictions $y$:
$$E = \frac{1}{2} \sum_j (t_j - y_j)^2$$
  - **Gradient Computation**: Utilizing the **Chain Rule** of calculus, the algorithm calculates the gradient of the loss function with respect to each weight, traversing the network in reverse. It computes error signals ($\delta$) for each unit:
    - For output units:
$$\delta_j = (t_j - y_j) \cdot f'(a_j)$$
    - For hidden units:
$$\delta_j = (\sum_k \delta_k w_{kj}) \cdot f'(a_j)$$
  - **Weight Updates**: Weights are adjusted in the direction that minimizes the error, scaled by a learning rate ($\eta$):
$$\Delta w_{ji} = \eta \cdot \delta_j \cdot y_i$$
leading to the update rule:
$$w_{ji}^{(new)} = w_{ji}^{(old)} + \Delta w_{ji}$$
This requires storing intermediate activations, making training consume significantly more memory than inference.
- **Computational Graphs**: Used to track dependencies between variables and operators during the forward and backward passes.

### Numerical Stability & Initialization
Training deep MLPs requires careful initialization to avoid instability:
- **Vanishing and Exploding Gradients**: Gradients can become extremely small or excessively large as they propagate back, disrupting the learning process.
- **Symmetry Breaking**: Random initialization is crucial to ensure that neurons in the same layer do not perform the exact same calculation.
- **Xavier (Glorot) Initialization**: A heuristic that scales initial weights based on the number of input and output units to keep activation and gradient variances consistent:
$$\sigma^2 = 2 / (n_{in} + n_{out})$$

## Generalization and Regularization
Deep networks have a tendency to easily overfit (interpolation) training data, presenting a generalization gap between training error and test error. Regularization techniques are necessary:
- **Weight Decay ($L_2$ Regularization)**: Penalizes large weights to encourage smoother models.
- **Dropout**: Randomly zeroes out a fraction of neurons during training to prevent co-adaptation, effectively acting as an ensemble of sub-networks. The remaining neurons are often scaled by a factor to maintain expected values:
$$1/(1-p)$$
Dropout is disabled during inference.
- **Early Stopping**: Halting the training process when validation error stops improving to prevent fitting to noise.

## Practical Implementation
Deploying MLPs involves key practical steps:
- **Data Preprocessing**: Essential techniques include standardization, handling missing values (e.g., via mean imputation), and one-hot encoding categorical features.
- **Hyperparameter Tuning**: Utilizing techniques like K-fold cross-validation to select optimal hyperparameters (see [[Hyperparameter_Optimization]]).
- **Metrics**: Using appropriate evaluation metrics, such as Root Mean Squared Logarithmic Error (RMSLE), for relative error evaluation.

***
*Sources:*
- [D2L Multilayer Perceptrons](https://d2l.ai/chapter_multilayer-perceptrons)
- [GeeksforGeeks: Backpropagation in Neural Network](https://www.geeksforgeeks.org/machine-learning/backpropagation-in-neural-network/)

***

Back to: [[Deep_Learning_Overview|Deep Learning Index]]
