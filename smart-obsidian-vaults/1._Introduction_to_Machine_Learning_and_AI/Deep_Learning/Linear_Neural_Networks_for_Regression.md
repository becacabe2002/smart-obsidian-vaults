---
status: finished
tags:
  - machine-learning
  - deep-learning
date: 2026-04-14T00:00:00.000Z
---
# Linear Neural Networks for Regression

## Introduction
Linear regression is a fundamental supervised learning algorithm used to predict numerical values. Serving as a foundational building block for more complex neural network architectures, it represents the simplest form of a single-layer fully connected network. The model assumes a linear relationship between input features and the target output.

## Mathematical Foundation
The linear regression model defines the relationship mathematically using a set of core components:
*   **Features ($\mathbf{x}$):** Input variables used for prediction.
*   **Labels ($y$):** Target numerical values.
*   **Weights ($\mathbf{w}$):** Parameters defining the influence of each feature.
*   **Bias ($b$):** An offset allowing the model to represent affine transformations.

For a vector of features $\mathbf{x}$, the prediction $\hat{y}$ is formulated as:
$$\hat{y} = \mathbf{w}^\top \mathbf{x} + b$$

In vectorized form over a batch of $n$ examples (represented by the design matrix $\mathbf{X}$), the prediction is given by:
$$\mathbf{\hat{y}} = \mathbf{Xw} + b$$

## 3. Training Process
Training aims to find parameters $(\mathbf{w}, b)$ that minimize the prediction error.

### Loss Function: Mean Squared Error (MSE)
The Mean Squared Error (MSE) measures the average of the squared differences between the predicted values ($\hat{y}$) and the actual values ($y$). It is the preferred loss function for regression due to its differentiability.
- **Formula (Mini-batch of size $n$):** 
  $$L(\mathbf{w}, b) = \frac{1}{n} \sum_{i=1}^{n} \frac{1}{2} (\hat{y}^{(i)} - y^{(i)})^2$$
- **Significance:** The factor of $1/2$ simplifies the gradient (canceling the exponent). The squared term heavily penalizes large errors, forcing the model to minimize them.

### Optimization: Minibatch Stochastic Gradient Descent (SGD)
As analytical solutions are often impractical, we use iterative optimization via Minibatch SGD.
- **Update Rule:**
  $$(\mathbf{w}, b) \leftarrow (\mathbf{w}, b) - \eta \cdot \mathbf{g}$$
  where $\mathbf{g}$ is the gradient computed from a minibatch, and $\eta$ is the learning rate.
- **Role of the Learning Rate ($\eta$):** This hyperparameter determines step size. 
  - *Too small*: Slow convergence, potential to get stuck. 
  - *Too large*: Risk of overshooting the minimum, leading to divergence.
  - *Optimal*: Efficient convergence to a stable solution.

## 4. Overcoming Challenges: Regularization
To prevent overfitting (memorization of training data), we employ **Weight Decay** ($L_2$ regularization), which penalizes large weights to favor simpler, more robust models.

### The Penalty Term
The original loss function is modified by adding a penalty proportional to the squared $L_2$ norm of the weights:
$$L(\mathbf{w}, b) + \frac{\lambda}{2} \|\mathbf{w}\|^2$$
- **Regularization Parameter ($\lambda$):** Controls the trade-off between fitting the training data (small $\lambda$) and keeping weights small (large $\lambda$).

### Why "Weight Decay"?
The term arises from how the optimization update is modified:
$$\mathbf{w} \leftarrow (1 - \eta \lambda) \mathbf{w} - \eta \cdot \mathbf{g}$$
At each iteration, the weights are multiplied by $(1 - \eta \lambda)$ (slightly less than 1), effectively shrinking them toward zero regardless of the gradient. This continuous "decay" forces the model to remain simple, reducing sensitivity to noise and enhancing generalization on unseen data.

***
*Sources:*
- [Linear Regression Index | D2L](https://d2l.ai/chapter_linear-regression/index.html)
- [Linear Regression | D2L](https://d2l.ai/chapter_linear-regression/linear-regression.html)
- [Weight Decay | D2L](https://d2l.ai/chapter_linear-regression/weight-decay.html)
- [Generalization | D2L](https://d2l.ai/chapter_linear-regression/generalization.html)

---
Back to: [[Deep_Learning_Overview|Deep Learning Index]]
