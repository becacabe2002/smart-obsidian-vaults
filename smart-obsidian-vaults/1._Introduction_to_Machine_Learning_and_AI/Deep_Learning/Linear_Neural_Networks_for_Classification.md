---
tags:
  - deep-learning
  - machine-learning
  - classification
  - finished
date: 2026-04-14T00:00:00.000Z
status: finished
---
# Linear Neural Networks for Classification

## Introduction
Classification addresses "which category?" questions, distinguishing it from regression, which answers "how much?". It is a foundational task in deep learning where models predict categorical labels for given inputs.

## Classification Concepts
* **Representing Labels:** Since categories often lack a natural ordering, they are typically represented using **one-hot encoding**. For $q$ categories, a label is a $q$-dimensional vector where the index of the correct category is 1 and all others are 0.
* **Linear Model Architecture:** To predict $q$ classes from $d$ features, the model uses $q$ affine functions (one per output). This results in a fully connected layer where the output vector $\mathbf{o}$ is calculated as $\mathbf{o} = \mathbf{W}\mathbf{x} + \mathbf{b}$, with $\mathbf{W} \in \mathbb{R}^{q \times d}$.
* **Hard vs. Soft Assignments:** While we often only care about the "hard" assignment (the single most likely class), models typically produce "soft" assignments—probabilities that each category applies.

## Softmax Regression
Raw outputs (logits) from a linear model can be any real value, which is unsuitable for probability.
* **The Softmax Function:** To transform logits into a valid probability distribution (non-negative and summing to 1), the softmax operation is applied:
  $$\hat{y}_i = \frac{\exp(o_i)}{\sum_{j=1}^q \exp(o_j)}$$
* **Properties:** The softmax function preserves the ordering of the logits. Therefore, to find the most likely class (hard prediction), one can simply take the `argmax` of the logits without computing the exponential.
* **Vectorization:** For efficiency, calculations are performed in minibatches $\mathbf{X} \in \mathbb{R}^{n \times d}$, allowing the dominant operation to be a matrix-matrix product $\mathbf{O} = \mathbf{X}\mathbf{W} + \mathbf{b}$.

## Loss Functions for Classification
The goal is to maximize the likelihood of the observed data, which is equivalent to minimizing the negative log-likelihood.
* **Cross-Entropy Loss:** For a one-hot label vector $\mathbf{y}$ and predicted probability vector $\mathbf{\hat{y}}$, the loss is:
  $$l(\mathbf{y}, \mathbf{\hat{y}}) = -\sum_{j=1}^q y_j \log \hat{y}_j$$
* **Information Theory Perspective:** 
  * **Entropy:** The minimum number of nats needed to encode data from a distribution.
  * **Surprisal:** $-\log P(j)$, representing how "surprised" we are by an event.
  * **Cross-Entropy:** The expected surprisal of an observer with subjective probabilities $\mathbf{\hat{y}}$ when the data actually follows distribution $\mathbf{y}$.
* **Gradients:** A key advantage of combining softmax with cross-entropy is the simple derivative: $\frac{\partial l}{\partial o_j} = \hat{y}_j - y_j$. The gradient is simply the difference between the model's prediction and the actual label.

## Generalization in Classification
Generalization is the model's ability to perform well on unseen data, as high training accuracy can often be achieved through mere memorization.
* **Empirical vs. Population Error:** We minimize empirical error (on the training set) to approximate the population error (the true error over the entire underlying distribution).
* **Statistical Bounds:** 
  * **Central Limit Theorem:** Suggests that test error converges to population error at a rate of $O(1/\sqrt{n})$.
  * **Hoeffding’s Inequality:** Provides finite sample bounds to determine the number of samples needed for a specific confidence level.
* **Test Set Reuse:** Repeatedly evaluating models on the same test set leads to **adaptive overfitting** and the problem of **false discovery**, where the test set eventually "leaks" into the modeling process.

## Environment and Distribution Shift
Models often fail when the distribution of data at deployment (target) differs from the training data (source).
* **Types of Shift:**
  * **Covariate Shift:** The distribution of inputs $P(\mathbf{x})$ changes, but the labeling function $P(y|\mathbf{x})$ remains the same.
  * **Label Shift:** The prevalence of labels $P(y)$ changes, but $P(\mathbf{x}|y)$ is fixed.
  * **Concept Shift:** The definition of a label changes over time or geography.
* **Correction Strategies:**
  * **Covariate Shift Correction:** Requires reweighting training examples by $\beta_i = P_{target}(\mathbf{x}_i) / P_{source}(\mathbf{x}_i)$, often estimated using a binary classifier.
  * **Label Shift Correction:** Can be addressed by estimating the target label distribution using the model's confusion matrix and mean outputs.

## Implementation Details
### From Scratch vs. Concise
* **From Scratch:** Focuses on building core components using low-level tensor operations. It involves manually implementing the softmax function (`torch.exp(X) / partition`) and cross-entropy loss. This approach is prone to numerical instability (overflow/underflow) if logits are too large or small.
* **Concise:** Leverages high-level framework features (e.g., `nn.Sequential`, `nn.CrossEntropyLoss`). 
* **The LogSumExp Trick:** Modern frameworks combine softmax and cross-entropy into a single numerically stable function. It subtracts the maximum logit ($\bar{o} = \max(o_k)$) from all logits before exponentiation, preventing overflow and ensuring robust calculations without encountering `NaN` or `inf` values.

## Sources
- https://d2l.ai/chapter_linear-classification/index.html
- https://d2l.ai/chapter_linear-classification/softmax-regression.html
- https://d2l.ai/chapter_linear-classification/image-classification-dataset.html
- https://d2l.ai/chapter_linear-classification/classification.html
- https://d2l.ai/chapter_linear-classification/softmax-regression-scratch.html
- https://d2l.ai/chapter_linear-classification/softmax-regression-concise.html
- https://d2l.ai/chapter_linear-classification/generalization-classification.html
- https://d2l.ai/chapter_linear-classification/environment-and-distribution-shift.html

---
Back to: [[Deep_Learning_Overview|Deep Learning Index]]
