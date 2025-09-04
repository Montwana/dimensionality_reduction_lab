# dimensionality_reduction_lab

## 1. Explained Variance

The explained variance decreases with each additional component since the first few capture most of the data’s variability. For the Wine dataset, about 6 principal components are needed to explain 95% of the variance.

## 2. PCA vs. LDA: Compare the PCA and LDA projections of the Wine dataset. Why does LDA typically perform better for classification tasks when used as a preprocessing step?

PCA finds directions (principal components) that maximize the overall variance in the data, without considering class labels. Its goal is data compression and visualization.

LDA finds directions (linear discriminants) that maximize the separation between classes while minimizing within-class scatter, explicitly using the class labels.

### Why LDA often performs better for classification:

Because LDA is supervised, it projects the data onto axes that best separate the classes, making them more distinguishable for classifiers. PCA, being unsupervised, may keep directions of high variance that are not necessarily useful for distinguishing between classes.

## 3. KPCA Gamma Parameter: Experiment with different γ (gamma) values in KPCA on the half-moon dataset. What happens if γ is too small (e.g., 0.01) or too large (e.g., 100)? How does it affect the transformed data and the linear separability of the classes?

Small γ (0.01):
The kernel function becomes very broad. All points look similar in terms of distance, so the transformation does not separate the classes well. The result is underfitting, and the half-moons remain not linearly separable after projection.

Large γ (100):
The kernel becomes very narrow, focusing too much on individual points. This leads to highly complex transformations where each point is separated almost uniquely. The data may become noisy and lose general structure (overfitting).

## 4. Classifier Performance: Apply a classifier (e.g., SVM or Logistic Regression) to the original data, the PCA-transformed data, and the LDA-transformed Wine data. Measure and compare the accuracy and computation time. What do you observe?

### Original Data

Accuracy: High (since the Wine dataset is well-structured and separable).

Computation Time: Longer, because the model works in 13-dimensional space.

Observation: Classifier has more features to process, but also some redundant/noisy ones.

### PCA-Transformed Data

Accuracy: Lower than original, because PCA maximizes variance but does not use class labels, so some class-discriminative information is lost.

Computation Time: Much faster (only 2 dimensions).

Observation: Good for visualization and compression, but weaker for classification

### LDA-Transformed Data (2 components)

Accuracy: Typically highest (better than PCA, often close to or higher than original).

Computation Time: Faster (reduced to 2 dimensions, but with class separation preserved).

Observation: Because LDA is supervised, it projects data to maximize class separability, so classifiers perform better.

## 5. When might standard PCA fail? Provide an example.

PCA assumes that the directions of maximum variance are the most informative. It works well for linearly separable data, but fails when data has nonlinear structures.

### Example:

In the concentric circles dataset, PCA cannot separate the classes because variance is radial not linear, so PCA projections overlap the two circles.

## How does KPCA address this?

Kernel PCA uses the kernel trick (RBF kernel) to project data into a higher-dimensional feature space where nonlinear structures become linear.
