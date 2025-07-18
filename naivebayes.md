---
layout: page
title: "Naive Bayes Classifier"
permalink: /naivebayes/
---
<!-- # Naive Bayes Classifier -->


This project implements a Naïve Bayes classifier using MLE-based Gaussian modeling to distinguish between two classes of image data using features derived from the mean and standard deviation of pixel intensities. The data consists of `.mat` files containing training and test images for each class. The images are reshaped and preprocessed to extract meaningful features before applying the classifier.

## Workflow Summary

- **Data Loading**: Images were loaded from the MNIST database only for class 0 and class 1. They were split into training and testing sets.

<div class="image-wrapper left-image" style="text-align: center;">
  <img src="https://danhlv.github.io/static/img/example_digits_data.png" alt="Example digits" style="width: 40%; display: block; margin: 0 auto;">
</div>

- **Preprocessing**: Each image was reshaped and two statistical features — mean (μ) and standard deviation (σ) — were extracted. These two values form a 2-dimensional feature vector for each image:

$$
\mathbf{x}_{\text{train}} = (\mu, \sigma)
$$

- **Parameter Estimation**: To model the class distributions, the mean vector $ \boldsymbol{\mu}_i \in \mathbb{R}^2 $ and the covariance matrix $ \Sigma_i \in \mathbb{R}^{2 \times 2} $ were estimated from the training data.

The formulas used for parameter estimation are:

$$
\boldsymbol{\mu}_y = \frac{1}{N_y} \sum_{i=1}^{N_y} \mathbf{x}_i,\quad
\Sigma_y = \frac{1}{N_y - 1} \sum_{i=1}^{N_y} (\mathbf{x}_i - \boldsymbol{\mu}_y)(\mathbf{x}_i - \boldsymbol{\mu}_y)^T
$$

Where $ y \in \{0, 1\} $ and $ N_y $ is the number of training samples for class $ y $ (5923 for class 0 and 6742 for class 1).

## Training

- For each class, the joint distribution of features was modeled using a multivariate Gaussian with the general form:

$$
P(x \mid y) = \frac{1}{(2\pi)^{d/2} \, |\Sigma_y|^{1/2}} \exp\left( -\frac{1}{2}(x - \mu_y)^T \Sigma_y^{-1} (x - \mu_y) \right)
$$

This was implemented using the `scipy.stats.multivariate_normal` module in Python.

<div class="image-wrapper left-image" style="text-align: center;">
  <img src="https://danhlv.github.io/static/img/2D_gaussian_plot_for_naive_bayes_classifier_train_data.png" alt="the multivariate distribution for the training data" style="width: 80%; display: block; margin: 0 auto;">
</div>

## Classification

We want to predict the class label $ \hat{y} \in \{0, 1\} $ that has the highest posterior probability given the observed 2D feature vector $ x = (\mu, \sigma) $:

$$
\hat{y} = \arg\max_y P(y \mid x)
$$

Using Bayes’ Theorem:

$$
P(y \mid x) = \frac{P(x \mid y) \cdot P(y)}{P(x)}
$$

In the binary case:

$$
P(0 \mid x) = \frac{P(x \mid 0) \cdot P(0)}{P(x)}, \quad
P(1 \mid x) = \frac{P(x \mid 1) \cdot P(1)}{P(x)}
$$

Since $ P(x) $ is the same for both classes, it cancels out during comparison:

$$
\hat{y} =
\begin{cases}
0 & \text{if } P(x \mid 0) \cdot P(0) > P(x \mid 1) \cdot P(1) \\
1 & \text{otherwise}
\end{cases}
$$

This approach leverages both the **statistical shape of the data** (via the Gaussian) and the **relative frequency of classes** (via the priors) to make informed predictions.

In our case:
- $ P(y \mid x) $: posterior probability to be maximized
- $ P(y) $: prior estimated from training class frequencies
- $ P(x \mid y) $: likelihood modeled by the class-specific 2D Gaussian PDF

## Final Results

- **Classification Accuracy**: <span style="font-size: 20px; color: red; font-weight: bold;">96.88%</span>


This high accuracy indicates that the model performs extremely well on the test data. The Naïve Bayes classifier effectively captures class-discriminative information using only two simple features — the mean and standard deviation of pixel intensities.











<!-- Add more sections as needed -->