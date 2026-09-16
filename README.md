# EN3150 Assignment 03 — Resource-Constrained CNN for Edge Image Classification

## 📌 Assignment Overview

This project was completed as part of **EN3150 – Pattern Recognition** at the **University of Moratuwa**.

The assignment focuses on developing and evaluating convolutional neural networks for **two-digit handwritten image classification** under resource constraints.

The task is formulated as a **100-class classification problem**, where each class represents a two-digit number from `00` to `99`.

The project evaluates:

- A standard custom CNN
- A resource-constrained lightweight CNN
- MobileNetV2 using transfer learning
- EfficientNet-B0 using transfer learning

The models are compared based on:

- Classification accuracy
- Number of trainable parameters
- Model size
- Computational/resource requirements
- Precision
- Recall
- Confusion matrices

---

## 👥 Group Members

| Name | Registration Number |
|---|---|
| Dilhara D.S. | 230147L |
| DISSANAYAKE G.R.G.K. | 230159B |
| MENDIS T.A.S.D. | 230409T |
| MARASINGHA M.D.S. | 230398F |

---

## 🎯 Problem Description

The dataset consists of images containing handwritten two-digit numbers.

Each image contains two handwritten digits. The two digits are combined to create a single class label:

**Class Label = 10 × label1 + label2**

Therefore, the classification problem contains **100 classes**:

`00, 01, 02, ..., 98, 99`

The maximum image resolution used in the assignment is **64 × 64 pixels**.

---

## 📂 Dataset

### MNIST 2-Digit Dataset

The dataset contains handwritten images representing two-digit numbers.

### Dataset Characteristics

- **Image Type:** Grayscale
- **Maximum Resolution:** 64 × 64
- **Number of Classes:** 100
- **Classes:** 00–99

### Dataset Preparation

The preprocessing pipeline consists of:

1. Loading dataset metadata
2. Constructing the two-digit class label
3. Locating the corresponding image
4. Resizing images to 64 × 64
5. Converting images to tensors
6. Normalizing image values

---

## 📊 Dataset Split

A stratified dataset split was used:

| Dataset | Percentage |
|---|---:|
| Training | 70% |
| Validation | 15% |
| Testing | 15% |

Stratification was used to maintain the class distribution across the training, validation and testing sets.

---

# 🧠 Model Architectures

## Model A — Standard Custom CNN

A conventional CNN architecture was implemented as the baseline custom model.

### Performance

| Metric | Value |
|---|---:|
| Trainable Parameters | 560,612 |
| Test Accuracy | 94.35% |
| Model Size | 2.1431 MB |

The model uses standard convolutional layers to extract spatial features from the handwritten digit images.

The extracted features are then passed through fully connected layers for classification into 100 classes.

---

## Model B — Resource-Constrained CNN

A lightweight CNN was developed specifically to satisfy the resource constraint:

**Trainable Parameters < 100,000**

The model uses **depthwise-separable convolutions** to significantly reduce the number of parameters and computational operations.

### Architecture

Input  
↓  
Depthwise-Separable Convolution: 1 → 16  
↓  
Max Pooling  
↓  
Depthwise-Separable Convolution: 16 → 32  
↓  
Max Pooling  
↓  
Depthwise-Separable Convolution: 32 → 64  
↓  
Max Pooling  
↓  
Adaptive Average Pooling  
↓  
Fully Connected: 64 → 100  
↓  
Output

### Performance

| Metric | Value |
|---|---:|
| Trainable Parameters | 9,741 |
| Test Accuracy | 64.97% |
| Model Size | 0.0466 MB |

The model satisfies the parameter constraint:

**9,741 < 100,000**

---

# ⚡ Depthwise-Separable Convolution

Depthwise-separable convolution separates a standard convolution into two operations:

**Depthwise Convolution + Pointwise Convolution**

Instead of performing a full convolution across all input and output channels, the depthwise operation processes each input channel separately.

The pointwise convolution then combines the resulting feature maps using `1 × 1` convolutions.

This substantially reduces:

- Number of trainable parameters
- Number of multiply-accumulate operations
- Memory requirements
- Computational complexity

This makes depthwise-separable convolutions suitable for:

- Edge devices
- Embedded systems
- Mobile devices
- Wearable devices
- Resource-constrained applications

---

# 🚀 Transfer Learning Models

Two state-of-the-art CNN architectures were also evaluated using transfer learning.

## MobileNetV2

MobileNetV2 was selected because it is designed for efficient image classification with relatively low computational requirements.

### Test Accuracy

**96.79%**

---

## EfficientNet-B0

EfficientNet-B0 was evaluated as another transfer-learning-based model.

### Test Accuracy

**97.47%**

EfficientNet-B0 achieved the highest test accuracy among the evaluated models.

---

# 📈 Experimental Results

| Model | Test Accuracy | Trainable Parameters | Model Size |
|---|---:|---:|---:|
| Standard Custom CNN | 94.35% | 560,612 | 2.1431 MB |
| Resource-Constrained CNN | 64.97% | 9,741 | 0.0466 MB |
| MobileNetV2 | 96.79% | — | — |
| EfficientNet-B0 | 97.47% | — | — |

---

# 🔍 Model Comparison

## Standard Custom CNN

The standard custom CNN provides a strong baseline for the classification task.

- **Parameters:** 560,612
- **Accuracy:** 94.35%
- **Model Size:** 2.1431 MB

## Resource-Constrained CNN

The lightweight CNN dramatically reduces the model size and parameter count.

- **Parameters:** 9,741
- **Accuracy:** 64.97%
- **Model Size:** 0.0466 MB

This demonstrates the trade-off between resource usage and classification performance.

## MobileNetV2

- **Accuracy:** 96.79%

MobileNetV2 provides strong classification performance while being designed for efficient deployment.

## EfficientNet-B0

- **Accuracy:** 97.47%

EfficientNet-B0 achieved the highest classification accuracy among the evaluated models.

---

# 📏 Evaluation Metrics

The models were evaluated using several classification metrics.

## Accuracy

Accuracy measures the proportion of correctly classified samples.

**Accuracy = Correct Predictions / Total Predictions**

## Precision

Precision measures how many samples predicted as a particular class actually belong to that class.

**Precision = True Positives / (True Positives + False Positives)**

## Recall

Recall measures how many samples belonging to a class were correctly identified.

**Recall = True Positives / (True Positives + False Negatives)**

## Confusion Matrix

Confusion matrices were used to analyze the classification behavior of the models across the 100 classes.

They help identify:

- Frequently confused classes
- Correct classifications
- Misclassification patterns
- Class-specific performance

---

# 📉 Training Analysis

The training and validation performance was monitored throughout training.

For the resource-constrained CNN, some instability was observed during later stages of training.

Possible improvements include:

- Learning-rate tuning
- Additional regularization
- Improved data augmentation
- Hyperparameter optimization
- Alternative lightweight architectures

---

# 💻 Technologies Used

- Python
- PyTorch
- NumPy
- Pandas
- Matplotlib
- Scikit-learn
- Pillow

---

# 📁 Suggested Repository Structure

    EN3150-Assignment-03/
    │
    ├── README.md
    │
    ├── notebooks/
    │   └── EN3150_Assignment_03.ipynb
    │
    ├── data/
    │   └── dataset/
    │
    ├── models/
    │   ├── custom_cnn.py
    │   ├── lightweight_cnn.py
    │   ├── mobilenetv2.py
    │   └── efficientnet.py
    │
    ├── results/
    │   ├── figures/
    │   ├── confusion_matrices/
    │   └── model_comparison/
    │
    └── requirements.txt

---

# ⚙️ Installation

Clone the repository:

    git clone <YOUR_GITHUB_REPOSITORY_URL>
    cd EN3150-Assignment-03

Create a virtual environment:

    python -m venv venv

### Windows

    venv\Scripts\activate

### Linux / macOS

    source venv/bin/activate

Install the required libraries:

    pip install torch torchvision numpy pandas matplotlib scikit-learn pillow

---

# ▶️ Running the Project

Open the Jupyter Notebook:

    jupyter notebook

Then open:

    notebooks/EN3150_Assignment_03.ipynb

The notebook contains the complete workflow:

    Dataset Loading
          ↓
    Preprocessing
          ↓
    Train / Validation / Test Split
          ↓
    Model Training
          ↓
    Validation
          ↓
    Testing
          ↓
    Performance Evaluation
          ↓
    Model Comparison

---

# 🧪 Experimental Workflow

    MNIST 2-Digit Dataset
             │
             ▼
      Data Preprocessing
             │
             ▼
      Stratified Data Split
             │
       ┌─────┼─────────────┐
       │     │             │
       ▼     ▼             ▼
     Model A Model B  Transfer Learning
     Custom   Lightweight       │
      CNN       CNN       ┌─────┴─────┐
       │         │        ▼           ▼
       │         │   MobileNetV2  EfficientNet-B0
       │         │        │           │
       └─────────┴────────┴───────────┘
                  │
                  ▼
           Model Evaluation
                  │
                  ▼
        Accuracy / Precision
        Recall / Confusion Matrix
                  │
                  ▼
           Model Comparison

---

# 📌 Key Observations

## 1. Resource Efficiency

The lightweight CNN reduced the number of trainable parameters from:

**560,612 → 9,741**

This represents a substantial reduction in model complexity.

## 2. Model Size

The lightweight CNN occupies only:

**0.0466 MB**

compared with:

**2.1431 MB**

for the standard custom CNN.

## 3. Accuracy vs. Resource Usage

The experiments demonstrate a trade-off between model complexity and classification performance:

    Lower Resource Usage
            ↓
       Smaller Model
            ↓
      Fewer Parameters
            ↓
    Lower Computational Cost
            ↕
    Potential Reduction
        in Accuracy

## 4. Transfer Learning

The transfer-learning models achieved high classification accuracy:

    MobileNetV2      → 96.79%
    EfficientNet-B0  → 97.47%

---

# 🎯 Main Takeaway

The assignment demonstrates that CNN architecture design involves a trade-off between **classification performance and computational/resource requirements**.

    Classification Accuracy
             ▲
             │
             │       EfficientNet-B0
             │          97.47%
             │
             │       MobileNetV2
             │          96.79%
             │
             │       Custom CNN
             │          94.35%
             │
             │
             │
             │   Lightweight CNN
             │       64.97%
             │
             └──────────────────────────►
                  Resource Usage

The resource-constrained CNN demonstrates how depthwise-separable convolutions can produce a compact model while satisfying strict parameter constraints.

---

# 📚 References

1. Murphy, K. P. — *Probabilistic Machine Learning: An Introduction*, 2022.

2. Fukushima, K. — *Cognitron: A Self-Organizing Multilayered Neural Network*, 1975.

3. Hubel, D. H. & Wiesel, T. N. — *Receptive Fields and Functional Architecture of Monkey Striate Cortex*, 1962.

4. LeCun, Y., Bottou, L., Bengio, Y. & Haffner, P. — *Gradient-Based Learning Applied to Document Recognition*, 1998.

---

# 🎓 Academic Project

This repository contains work completed for:

**EN3150 – Pattern Recognition**  
**Faculty of Engineering**  
**University of Moratuwa**

This is a university coursework project.
