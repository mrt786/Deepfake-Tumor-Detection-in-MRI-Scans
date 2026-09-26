# Deepfake Tumor Detection in MRI Scans

This repository contains the complete project work for brain MRI deepfake and synthetic tumor detection. It brings together dataset preparation, model training, evaluation, inference, and synthetic image generation for medical imaging security research.

The project is also documented in the attached PDF report: `DeepfakeTumorDetection.pdf`.

## Project Overview

The main objective of this work is to detect manipulated or synthetic MRI images that may contain tumor-like patterns and to distinguish them from real medical scans. The project explores multiple model families and training strategies, including:

- Lightweight multi-task CNNs for real-vs-fake authenticity and tumor classification
- Adversarial feature fusion and ensemble-based detection
- Hybrid CNN-transformer architectures for medical deepfake detection
- StyleGAN-based synthetic MRI generation for data augmentation and analysis

## Research Focus

The work addresses a clinically important problem: ensuring that MRI-based diagnostics are not misled by GAN-generated or adversarially manipulated images. The notebooks in this repository implement both detection pipelines and synthetic generation workflows.

## Repository Structure

```text
Submission_Files/
├── Readme.md
├── DeepfakeTumorDetection.pdf
├── Code_Files/
│   ├── A2_Testing.ipynb
│   ├── A3_Testing.ipynb
│   ├── Inference.ipynb
│   ├── lc-net050-70-10-20.ipynb
│   ├── lcnet050_visualization.ipynb
│   ├── Parallel_lcnet050.ipynb
│   ├── Viz.ipynb
│   ├── md_cmp.csv
│   ├── EPIC&CSRMendly/
│   │   └── multitask_mri.onnx
│   └── InferenceFiles/
│       ├── fake/
│       └── real/
├── StyleGanDataGeneration/
│   └── CodeFiles/
│       ├── 1.ipynb
│       ├── 2.ipynb
│       ├── PatchManipulation.ipynb
│       ├── Setup.md
│       ├── StyleGAN_Tumor_Synthesis.ipynb
│       ├── models/
│       ├── results/
│       └── StyleGAN/
│           ├── checkpoints/
│           ├── models/
│           ├── Outputs/
│           └── results/
├── results/
│   └── mri_tumor_gan/
├── ResultsGan/
│   └── Outputs/
└── .git/
```

## Major Components

### 1. Detection and classification notebooks

The repository includes several notebooks focused on MRI deepfake detection:

- `Code_Files/A2_Testing.ipynb`
  - Focuses on adversarial feature fusion for tumor deepfake detection
  - Uses deep CNN features, handcrafted HOG features, and SVM classification
  - Mentions a ResNet50 + HOG + RBF-SVM pipeline with adversarial robustness testing

- `Code_Files/A3_Testing.ipynb`
  - Implements a hybrid CNN-transformer architecture with multi-task heads
  - Includes adversarial augmentation, dual-branch feature extraction, fusion, and XAI-style analysis

- `Code_Files/lc-net050-70-10-20.ipynb`
  - Contains a lightweight multi-task MRI CNN based on `lcnet_050`
  - Handles authenticity detection, tumor-type classification, and joint task learning
  - Uses a balanced dataset strategy for real and fake classes

- `Code_Files/Parallel_lcnet050.ipynb`
  - Parallel training/evaluation workflow for the lightweight model variant

- `Code_Files/lcnet050_visualization.ipynb`
  - Visualization and analysis notebook for the lightweight model

### 2. Inference and deployment

- `Code_Files/Inference.ipynb`
  - Runs model inference on MRI scans using the ONNX model in `EPIC&CSRMendly/multitask_mri.onnx`
  - Provides predictions for authenticity and tumor-class labels

- `Code_Files/EPIC&CSRMendly/`
  - Contains the exported model artifact used for inference

### 3. StyleGAN-based synthetic MRI generation

The project also includes a generative modeling pipeline for synthetic tumor MRI data:

- `StyleGanDataGeneration/CodeFiles/StyleGAN_Tumor_Synthesis.ipynb`
- `StyleGanDataGeneration/CodeFiles/2.ipynb`
- `StyleGanDataGeneration/CodeFiles/PatchManipulation.ipynb`

These notebooks are designed to generate realistic brain MRI images with tumor-like patterns, helping explore synthetic data generation and fake-image creation as part of the deepfake detection problem.

## Dataset Organization

The notebooks assume a dataset structure similar to the following:

```text
dataset/
├── real/
│   ├── glioma/
│   ├── meningioma/
│   ├── notumor/
│   └── pituitary/
└── fake/
    ├── gan/
    ├── attacks/
    └── other synthetic variants/
```

The lightweight notebook also balances the dataset using a target proportion strategy based on real and fake class groups to reduce class imbalance during training.

## Model Categories in This Work

### Lightweight Multi-Task CNN

The project uses a compact backbone (`lcnet_050`) with multi-task output heads to perform:

- Authenticity classification: real vs fake
- Tumor-type classification: no tumor / glioma / meningioma / pituitary
- Joint task prediction for combined decision analysis

This is the main architecture used in the repository’s training notebooks.

### Hybrid CNN-Transformer Model

A second pipeline uses a dual-branch network combining:

- CNN backbone for local spatial feature extraction
- Vision Transformer branch for global contextual representation
- Feature fusion and multi-head classification for fake detection and localization

### Ensemble / Feature Fusion Model

The project also explores a feature-fusion method where deep visual features and handcrafted descriptors are concatenated and passed to a classifier for more robust deepfake detection on MRI scans.

## Training and Evaluation Workflow

Typical workflow:

1. Prepare and organize MRI dataset
2. Balance real and fake classes
3. Train one or more detection architectures
4. Evaluate through validation and test splits
5. Run inference on unseen MRI samples
6. Visualize feature importance and model outputs
7. Use synthetic generated samples to study fake-image behavior

## Requirements

The notebooks require a Python environment with common deep learning libraries such as:

- Python 3.10+
- PyTorch
- torchvision
- timm
- albumentations
- OpenCV
- scikit-learn
- matplotlib
- seaborn
- ONNX / ONNX Runtime
- transformers

Some notebooks were run in Kaggle or GPU environments, so GPU support is recommended for training and experimentation.

## Setup Guide

1. Clone or download this repository.
2. Place the MRI dataset in a structure compatible with the notebook paths.
3. Open the relevant notebook from `Code_Files/`.
4. Update dataset paths if necessary.
5. Run the cells in order to prepare data, train models, and evaluate.

For the StyleGAN pipeline, use the setup instructions in:

- `StyleGanDataGeneration/CodeFiles/Setup.md`

## Usage Notes

- `A2_Testing.ipynb` and `A3_Testing.ipynb` are useful for experimental model testing.
- `lc-net050-70-10-20.ipynb` is the core lightweight training notebook.
- `Inference.ipynb` is used for model inference on real or fake MRI samples.
- `StyleGanDataGeneration/CodeFiles` focuses on synthetic MRI generation and augmentation.

## Results and Outputs

The repository contains generated outputs and model-related artifacts in directories such as:

- `results/`
- `ResultsGan/`
- `StyleGanDataGeneration/CodeFiles/results/`
- `StyleGanDataGeneration/CodeFiles/models/`

These folders contain training outputs, generated samples, and visualization artifacts from the project.

## Summary

This project combines medical imaging security, deepfake detection, and generative modeling to investigate whether synthetic or manipulated brain MRI data can be accurately detected and separated from authentic scans. It is a practical research-oriented repository for AI-based MRI forensic analysis.

## Citation

If this work is used for academic or research purposes, please cite the attached project PDF/report as the main reference and mention the repository as the implementation source.

---

This README was prepared to summarize the full scope of the project, including the detection models, synthetic augmentation workflow, and the repository structure used in the work.
