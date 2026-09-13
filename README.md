# 🌿 AgriLens

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?logo=tensorflow&logoColor=white)
![TensorFlow Lite](https://img.shields.io/badge/TensorFlow%20Lite-FF6F00)
![Flutter](https://img.shields.io/badge/Flutter-02569B?logo=flutter&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?logo=opencv&logoColor=white)
![Grad-CAM](https://img.shields.io/badge/Grad--CAM-XAI-blue)

### Offline Multi-Crop Plant Disease Detection System Using Deep Learning for Edge Deployment

AgriLens is an end-to-end deep learning system designed for offline plant disease detection on mobile devices. The project combines transfer learning, explainable AI (Grad-CAM), confidence-based prediction validation, an advisory engine, TensorFlow Lite deployment, and a Flutter mobile application to deliver practical disease diagnosis directly on the device.

The objective of AgriLens is not only to classify plant diseases with high accuracy but also to build a deployable system that is reliable, interpretable, and useful for real-world agricultural applications.

---

# Features

- Offline plant disease detection using TensorFlow Lite
- Supports **38 plant disease classes**
- MobileNetV2 transfer learning model
- Validation accuracy of **98.8%**
- Confidence score reporting for prediction reliability
- Grad-CAM based explainability during model development
- Disease advisory engine providing:
  - Disease description
  - Symptoms
  - Causes
  - Treatment recommendations
  - Prevention measures
- Flutter mobile application
- Camera and Gallery image support
- Lightweight edge deployment

---

# Application Preview

| Home Screen | Disease Prediction |
|-------------|--------------------|
| ![](screenshots/home_screen.jpeg) | ![](screenshots/result_display1.jpeg) |

| About Screen | Prediction Details |
|--------------|--------------------|
| ![](screenshots/about_screen1.jpeg) | ![](screenshots/result_display2.jpeg) |

---

# Project Overview

The project follows a complete machine learning engineering pipeline.

```
Dataset
    ↓
Exploratory Data Analysis
    ↓
Baseline CNN
    ↓
Transfer Learning (MobileNetV2)
    ↓
Model Evaluation
    ↓
Confidence Analysis
    ↓
Grad-CAM Explainability
    ↓
Disease Advisory Engine
    ↓
TensorFlow Lite Conversion
    ↓
Flutter Mobile Application
```

---

# Repository Structure

```
AgriLens
│
├── app/                    # Flutter mobile application
├── data/                   # Knowledge base, class mappings and utilities
├── docs/                   # Product requirements and technical design
├── image/
│   └── gradcam_examples/
├── models/                 # TensorFlow Lite deployment model
├── notebooks/              # Complete ML development pipeline
│   ├── 01_dataset_exploration.ipynb
│   ├── 02_baseline_cnn.ipynb
│   ├── 03_transfer_learning.ipynb
│   ├── 04_model_evaluation.ipynb
│   ├── 05_confidence_analysis.ipynb
│   ├── 06_gradcam_generation.ipynb
│   ├── 07_gradcam_analysis.ipynb
│   ├── 08_advisory_engine.ipynb
│   └── 09_tflite_deployment_pipeline.ipynb
│
├── reports/                # Analysis and Evaluation reports
├── screenshots/            # Application screenshots
├── requirements.txt
├── LICENSE
├── README.md
└── .gitignore
```

---

# Dataset

Dataset: **New Plant Diseases Dataset (Augmented)**

- 38 plant disease classes
- 87,867 RGB images
- Training Images: 70,295
- Validation Images: 17,572

The dataset was explored to analyze:

- Class distribution
- Image dimensions
- Duplicate images
- Channel statistics
- Data quality

---

# Model Development

## Baseline Model

A custom CNN was initially developed to establish a baseline for comparison.

---

## Transfer Learning

The final model uses:

- MobileNetV2
- ImageNet pretrained weights
- Fine-tuning
- Input size: **224 × 224**

Transfer learning significantly improved both convergence and final accuracy while keeping the model lightweight enough for mobile deployment.

---

# Model Performance

**Validation Accuracy: 98.8%**


Additional evaluation included:


- Confusion Matrix
- Classification Report (- Precision, Recall, F1-Score)
- Misclassification Analysis

---

# Reliability Layer

A confidence-based rejection mechanism was developed to improve deployment reliability.

Instead of forcing a prediction for every image, the application rejects predictions whose confidence falls below a selected threshold and asks the user to capture a better image.

This reduces the likelihood of presenting incorrect predictions caused by blurry, low-quality, or ambiguous images.

---

# Explainable AI (Grad-CAM)

Grad-CAM was used during model development to verify that the model focused on disease-affected regions rather than irrelevant image features.

Due to TensorFlow Lite's inference-only runtime, Grad-CAM is **not generated inside the deployed Flutter application**.

Example Grad-CAM visualizations are available in the `image/gradcam_examples/` directory.

---

# Advisory Engine

The project includes a lightweight knowledge base that provides practical information after disease prediction.

Each disease contains:

- Description
- Symptoms
- Causes
- Treatment
- Prevention

This transforms the system from a classifier into a practical decision-support application.

---

# Flutter Mobile Application

The final mobile application was developed using Flutter.

Features include:

- Camera capture
- Gallery selection
- Offline inference
- Confidence score
- Disease information
- Treatment suggestions
- Prevention recommendations
- Modern responsive interface

The application performs all predictions locally using TensorFlow Lite without requiring an internet connection.

---

# Development Environment

### Machine Learning Pipeline

- Python 3.10.20
- Ubuntu (WSL2)
- TensorFlow 2.21

### Mobile Application

- Flutter
- Dart
- TensorFlow Lite

---

# Installation

Clone the repository

```bash
git clone https://github.com/sahilf7/AgriLens.git
cd AgriLens
```

Install Python dependencies

```bash
pip install -r requirements.txt
```

Run the Flutter application by following the documentation inside the `app/` directory.

---

# Results

- **98.8% validation accuracy**
- Lightweight TensorFlow Lite deployment
- Offline mobile inference
- Confidence-aware predictions
- Explainable model development
- Practical agricultural advisory system

---

# Limitations

- Performance depends on image quality.
- Supports only the **38 plant disease classes** included in the training dataset.
- Images outside the supported crops or diseases may produce unreliable predictions.
- Grad-CAM is available only during model development and analysis, not during mobile inference.
- The model does not verify whether the input contains a plant leaf. Every input image receives one of the 38 supported class predictions.

---

# Future Improvements

- Leaf Classifier (To reject non-leaf images)
- Support additional crop species
- Multi-language advisory system
- Cloud synchronization
- Continuous model updates

---

# Documentation

Detailed product requirements, architecture, and technical design are available in the `docs/` directory.

Analysis and Evaluation reports are available in the `reports/` directory.

---

# License

This project is licensed under the MIT License.

---

# Acknowledgements

- New Plant Diseases Dataset (Augmented)
- TensorFlow
- TensorFlow Lite
- Flutter
- OpenCV
- Scikit-learn
