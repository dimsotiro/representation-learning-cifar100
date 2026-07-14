# Representation Learning for Image Classification using Autoencoders and Pretrained Embeddings

## Overview

This project investigates how different image representations affect the performance of a distance-based classifier.

Instead of comparing different classifiers, a fixed **3-Nearest Neighbors (3-NN)** classifier is used throughout all experiments, allowing the study to focus exclusively on the quality of the learned feature representations.

The project compares:

- Raw pixel representations
- Fully Connected Autoencoder (FCAE)
- Convolutional Autoencoder (CAE)
- OpenAI CLIP embeddings
- ResNet-18 embeddings

All experiments were performed on a subset of the **CIFAR-100** dataset consisting of 10 randomly selected classes. :contentReference[oaicite:0]{index=0}

---

# Motivation

Image representations play a crucial role in the performance of machine learning models.

Rather than training increasingly complex classifiers, this project explores how improving the underlying feature representation can significantly enhance classification performance—even when using a simple distance-based algorithm such as k-NN.

---

# Experimental Pipeline

```
Input Images
      │
      ▼
Representation Learning
(Raw Pixels / Autoencoder / CLIP / ResNet)
      │
      ▼
Feature Embeddings
      │
      ▼
3-Nearest Neighbors
      │
      ▼
Classification Performance
```

---

# Dataset

**Dataset:** CIFAR-100

- 100 image classes
- Images resized to 32×32 pixels
- Random subset of 10 classes
- Fixed random seed for reproducibility
- Pixel values normalized to [0,1] :contentReference[oaicite:1]{index=1}

---

# Models Evaluated

## Raw Pixels

Baseline using flattened image vectors.

---

## Fully Connected Autoencoder

Architecture:

```
3072
 ↓
1024
 ↓
512
 ↓
128 (Latent Space)
 ↓
512
 ↓
1024
 ↓
3072
```

Experiments included:

- Baseline architecture
- MSE reconstruction loss
- Huber (SmoothL1) reconstruction loss
- Deeper fully-connected architecture

---

## Convolutional Autoencoder

Experiments included:

- Baseline convolutional autoencoder
- Huber loss
- Deeper convolutional architecture
- Dimension-matched comparison with the fully connected autoencoder

---

## Pretrained Embeddings

The learned representations were compared against two pretrained computer vision models:

- OpenAI CLIP
- ResNet-18

Embeddings were extracted without fine-tuning and evaluated using the same 3-NN classifier. :contentReference[oaicite:2]{index=2}

---

# Results

| Representation | Embedding Size | Accuracy |
|---------------|---------------:|----------:|
| Raw Pixels | 3072 | 35.3% |
| Fully Connected AE | 128 | 40.8% |
| Convolutional AE | 512 | 42.2% |
| ResNet-18 | 512 | 83.7% |
| **CLIP** | **512** | **86.1%** |

The results demonstrate the significant impact that feature representation has on classification performance. Pretrained embeddings substantially outperform both raw pixels and representations learned from scratch on the limited training dataset. :contentReference[oaicite:3]{index=3}

---

# Visualizations

The project also includes:

- PCA visualization
- t-SNE visualization
- Confusion matrices
- Autoencoder architecture diagrams

These visualizations provide additional insight into class separability and the geometry of the learned embedding spaces.

---

# Key Findings

- Learned embeddings outperform raw pixel representations.
- Convolutional Autoencoders perform better than Fully Connected Autoencoders when larger latent spaces are available.
- Simply increasing model complexity does not necessarily improve representation quality.
- CLIP embeddings achieved the highest classification accuracy among all evaluated methods.
- Representation quality is more influential than classifier complexity for distance-based classification. :contentReference[oaicite:4]{index=4}

---

# Technologies

- Python
- PyTorch
- NumPy
- Scikit-learn
- Matplotlib
- OpenAI CLIP
- Torchvision

---

# Repository Structure

```
.
├── DeepLearning.ipynb
├── report.pdf
├── requirements.txt
├── images/
│   ├── architecture.png
│   ├── comparison_table.png
│   ├── tsne.png
│   ├── pca.png
│   └── confusion_matrix.png
└── README.md
```

---

# References

- Hinton & Salakhutdinov (2006), *Reducing the Dimensionality of Data with Neural Networks*
- Radford et al. (2021), *Learning Transferable Visual Models From Natural Language Supervision*
- He et al. (2016), *Deep Residual Learning for Image Recognition*

---

## Author

**Dimitris Sotiropoulos**

MSc in Cybersecurity & Data Science  
University of Piraeus
