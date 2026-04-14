---
status: need-review
tags:
  - deep-learning
  - cnn
  - computer-vision
date: 2025-05-22
---

# Convolutional Neural Networks (CNNs)

Convolutional Neural Networks (CNNs) are a specialized class of neural networks designed to process data with a known grid-like topology, most notably images. Unlike standard [[Multilayer_Perceptrons]] (MLPs), CNNs exploit spatial hierarchies and local patterns, making them the cornerstone of modern [[Computer_Vision]].

## Introduction
The primary challenge with using MLPs for high-resolution images is the sheer number of parameters. For a $1000 \times 1000$ RGB image, a single hidden layer with 1000 units would require 3 billion weights. CNNs overcome this by leveraging two key inductive biases: **translation invariance** and **locality**.

## Fundamental Principles

### Translation Invariance
A feature detector (e.g., an edge detector or a "cat ear" detector) should be equally effective regardless of where the feature appears in the image. In a CNN, this is achieved through **weight sharing**: the same set of weights (the kernel) is applied to every possible position in the input.

> [!NOTE] Key Insight
> Translation invariance means that the identity of an object doesn't change if it shifts slightly. CNNs are naturally suited for this because the convolution operation is equivariant to translation.

### Locality
In natural images, pixels that are close to each other are highly correlated, while pixels far apart are relatively independent. CNNs enforce locality by restricting neurons to only "look" at a small local neighborhood of the input, known as the **receptive field**.

---

## Components of a Convolutional Layer

### Cross-Correlation vs. Convolution
While mathematically "convolution" involves flipping the kernel before sliding it across the input, most deep learning frameworks (like PyTorch and TensorFlow) actually implement **cross-correlation**.

$$ (I * K)(i, j) = \sum_{m} \sum_{n} I(i+m, j+n) K(m, n) $$

In practice, the distinction is minor because the network learns the kernel weights; if a flipped kernel is better, the network will simply learn the flipped values.

### Padding and Strides
To control the output dimensions and ensure edge pixels are sufficiently represented, we use:
*   **Padding ($p$):** Adding extra rows/columns (usually zeros) around the input boundary.
*   **Strides ($s$):** The number of pixels the kernel moves at each step.

The output size $(H_{out}, W_{out})$ for an input $(H_{in}, W_{in})$ with kernel size $k$ is calculated as:

$$ H_{out} = \lfloor \frac{H_{in} + 2p - k}{s} \rfloor + 1 $$
$$ W_{out} = \lfloor \frac{W_{in} + 2p - k}{s} \rfloor + 1 $$

### Multiple Channels
Modern CNNs work with 3D tensors (height, width, channels).
*   **Input Channels:** For RGB images, this is 3. The kernel must have the same number of input channels.
*   **Output Channels:** We use multiple kernels to detect different features simultaneously. Each kernel produces one output channel (feature map).
*   **1x1 Convolutions:** These act as per-pixel fully connected layers, allowing the network to change the number of channels without affecting spatial resolution.

---

## Pooling Layers
Pooling layers are used to reduce the spatial resolution of feature maps, which decreases the parameter count and provides further translation invariance.
*   **Max Pooling:** Outputs the maximum value in each window. It is robust to small spatial shifts.
*   **Average Pooling:** Outputs the average value. It was common in early networks like LeNet but is less frequent in modern architectures.

---

## Case Study: LeNet-5 Architecture
Developed by Yann LeCun in the 1990s for digit recognition, LeNet-5 was one of the first successful CNNs. It follows a pattern of alternating convolution and pooling layers:

1.  **Conv Block 1:** $5 \times 5$ Convolution (6 channels) $\to$ Sigmoid $\to$ $2 \times 2$ Average Pooling.
2.  **Conv Block 2:** $5 \times 5$ Convolution (16 channels) $\to$ Sigmoid $\to$ $2 \times 2$ Average Pooling.
3.  **Dense Block:** Flatten $\to$ FC (120 units) $\to$ Sigmoid $\to$ FC (84 units) $\to$ Sigmoid $\to$ Output (10 units).

---

## Summary
CNNs revolutionized [[Deep_Learning]] by providing a parameter-efficient way to process spatial data. By combining local receptive fields, shared weights, and spatial downsampling, they can learn complex hierarchical features—from simple edges to complete objects.

***

### Ingestion Log & Sources
*   2025-05-22 - [Dive into Deep Learning (D2L): Convolutional Neural Networks](https://d2l.ai/chapter_convolutional-neural-networks/index.html)
*   2025-05-22 - [D2L: Why Convolutions?](https://d2l.ai/chapter_convolutional-neural-networks/why-conv.html)
*   2025-05-22 - [D2L: Convolutional Layers](https://d2l.ai/chapter_convolutional-neural-networks/conv-layer.html)
*   2025-05-22 - [D2L: Padding and Strides](https://d2l.ai/chapter_convolutional-neural-networks/padding-and-strides.html)
*   2025-05-22 - [D2L: Multiple Channels](https://d2l.ai/chapter_convolutional-neural-networks/channels.html)
*   2025-05-22 - [D2L: Pooling](https://d2l.ai/chapter_convolutional-neural-networks/pooling.html)
*   2025-05-22 - [D2L: LeNet Architecture](https://d2l.ai/chapter_convolutional-neural-networks/lenet.html)

***

Back to: [[Deep_Learning_Overview|Deep Learning Index]]
