# Comparative Analysis of DCGAN and WGAN-GP

## Overview

This project compares the performance of two popular GAN architectures—**DCGAN** and **WGAN-GP**—in generating synthetic images across datasets of increasing complexity:
- **MNIST** (handwritten digits)
- **CIFAR-10** (natural objects)
- **Anime Faces** (high-resolution art)

The full report detailing methods, results, and discussion is available in the `Report` folder:
- ***Final_Report.pdf***

---

## Datasets

| Dataset      | Description                                                                 |
|--------------|-----------------------------------------------------------------------------|
| MNIST        | 28x28 grayscale images of handwritten digits (0–9)                         |
| CIFAR-10     | 32x32 color images from 10 object classes (e.g. dogs, trucks, ships)        |
| Anime Faces  | 64x64 cropped high-resolution anime character faces                         |

- **Source**:
  - MNIST & CIFAR-10: via `torchvision.datasets`
  - Anime Faces: [Kaggle Anime Face Dataset](https://www.kaggle.com/datasets/splcher/animefacedataset)
- Subsets of ~10,000 images were used for CIFAR-10 and Anime Faces due to compute limits.

---

## Models Compared

### 1. DCGAN (Deep Convolutional GAN)
- Based on Radford et al. (2015)
- Convolutional generator & discriminator
- Minimax loss formulation
- Tuned using Optuna (Bayesian hyperparameter search)

### 2. WGAN-GP (Wasserstein GAN with Gradient Penalty)
- Based on Gulrajani et al. (2017)
- Uses Wasserstein-1 distance and gradient penalty for stable training
- No sigmoid output or batch normalization
- Tuned manually due to training instability and compute limits

---

## Evaluation Metrics

- **Frechet Inception Distance (FID)**: Measures similarity between real and generated image distributions
- **Inception Score (IS)**: Measures quality and diversity of generated images

> Quantitative scores were only computed for the Anime Face dataset due to time and dataset size constraints.
> 
> FID score calculation only uses 3k images (not the standard 50k) due to compute limitations --> mainly used to compare DCGAN vs WGAN-GP image qualities NOT to benchmark our results

---

## Key Results

| **Model**   | **FID**   | **IS**    |
|:-----------:|:---------:|:---------:|
| DC-GAN      | 0.0294    | 1.897     |
| WGAN-GP     | 0.0239    | 1.949     |

- **WGAN-GP** produced the most realistic and coherent images on MNIST and Anime Faces
- **DCGAN** slightly outperformed WGAN-GP on CIFAR-10, which had more intra-class variability
- WGAN-GP required significantly more training time, but was more stable overall

---

## Example Outputs

> Generated image samples and training loss plots are included at the end of the full report.

---

## Conclusions

| Dataset     | Best Model | FID Score | Inception Score |
|-------------|------------|-----------|-----------------|
| MNIST       | WGAN-GP    | *N/A*     | *N/A*           |
| CIFAR-10    | DCGAN      | *N/A*     | *N/A*           |
| Anime Faces | WGAN-GP    | 0.0239    | 1.949           |


- **WGAN-GP** excels on visually consistent, high-resolution datasets like Anime Faces
- **DCGAN** may be more efficient for datasets with limited compute or high class variability
- GAN performance is dataset-dependent, and model choice should reflect data characteristics

---

## Future Work

- Extend comparisons to include models like StyleGAN or Diffusion Models
- Evaluate more robust quantitative metrics across all datasets
- Train on full-size CIFAR-10 and Anime datasets to improve performance
- Explore using attention or transformer-based generative models

---

## Acknowledgments

This project was completed for COGS 185 at UC San Diego by:
- Aatyanth Thimma Udayakumar
- Vishal Patel

**Core references**:
- [Goodfellow et al., 2014 – GANs](https://arxiv.org/abs/1406.2661)
- [Radford et al., 2015 – DCGAN](https://arxiv.org/abs/1511.06434)
- [Gulrajani et al., 2017 – WGAN-GP](https://arxiv.org/abs/1704.00028)
