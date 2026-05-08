# CIFAR-10 Image Classification: Custom CNN vs Transfer Learning

## Index

1. [Project Overview](#project-overview)
2. [Project Motivation](#project-motivation)
3. [Dataset](#dataset)
4. [Repository Structure](#repository-structure)
5. [Methodology](#methodology)
   - [Custom CNN](#custom-cnn)
   - [Transfer Learning](#transfer-learning)
6. [Models Compared](#models-compared)
7. [Evaluation Metrics](#evaluation-metrics)
8. [Results Summary](#results-summary)
9. [Key Findings](#key-findings)
10. [Challenges and Lessons Learned](#challenges-and-lessons-learned)
11. [How to Run the Project](#how-to-run-the-project)
12. [Requirements](#requirements)
13. [Project Deliverables](#project-deliverables)
14. [Future Improvements](#future-improvements)
15. [Team Members](#team-members)
16. [Credits](#credits)
17. [License](#license)

---

## Project Overview

This project applies **Convolutional Neural Networks (CNNs)** and **transfer learning** to classify images from the **CIFAR-10 dataset**.

The project compares two main approaches:

1. Building a **custom CNN from scratch**
2. Using **pretrained transfer learning models**

The final goal was to understand how far a custom CNN could go through architecture experimentation, regularisation, data augmentation, and learning-rate tuning, and then compare that performance against pretrained models such as **EfficientNetB0**, **DenseNet121**, and **MobileNet / MobileNetV3**.

---

## Project Motivation

The motivation behind this project was to understand how deep learning models learn visual features from image data.

Specifically, we wanted to investigate:

- How a CNN learns from small 32×32 colour images
- How architecture changes affect performance
- How overfitting appears in learning curves
- How data augmentation improves generalisation
- How transfer learning compares with training a CNN from scratch
- Which model performs best on CIFAR-10 classification

This project helped us practise the full computer vision workflow:

- preprocessing
- modelling
- experimentation
- evaluation
- interpretation
- presentation of results

---

## Dataset

The project uses the **CIFAR-10 dataset**.

CIFAR-10 contains:

- **50,000 training images**
- **10,000 test images**
- **32×32 pixel RGB images**
- **10 image classes**

The target classes are:

| Class ID | Class Name |
|---:|---|
| 0 | airplane |
| 1 | automobile |
| 2 | bird |
| 3 | cat |
| 4 | deer |
| 5 | dog |
| 6 | frog |
| 7 | horse |
| 8 | ship |
| 9 | truck |

CIFAR-10 is a useful dataset for image classification practice because it is small enough to train quickly, but challenging enough to show real model limitations, especially between visually similar classes.

---

## Repository Structure

```text
cifar10-cnn-transfer-learning/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── notebooks/
│   ├── 01_custom_cnn_experiments.ipynb
│   ├── 02_efficientnetb0_transfer_learning.ipynb
│   ├── 03_densenet121_transfer_learning.ipynb
│   └── 04_mobilenet_transfer_learning.ipynb
│
├── src/
│   └── helper_functions.py
│
├── results/
│   ├── metrics_summary.csv
│   ├── classification_reports/
│   └── model_comparisons/
│
├── figures/
│   ├── learning_curves/
│   ├── confusion_matrices/
│   ├── comparison_plots/
│   └── architecture_diagrams/
│
├── presentation/
│   └── CIFAR10_CNN_Transfer_Learning_Presentation.pptx
│
└── models/
    └── README.md
```

> Note: Large trained model files such as `.keras` or `.h5` are not intended to be pushed directly to GitHub unless file size limits allow it. They should be stored externally or documented in the `models/README.md` file.

---

## Methodology

### Custom CNN

The first part of the project focused on building a CNN from scratch.

The custom CNN workflow included:

- Loading the CIFAR-10 dataset
- Visualising sample images and labels
- Normalising image pixel values by dividing by `255`
- Encoding labels
- Splitting training data into training and validation sets
- Building a baseline CNN
- Training and evaluating the baseline model
- Analysing learning curves
- Iteratively improving the architecture
- Applying regularisation
- Applying data augmentation
- Selecting the best custom CNN for comparison with transfer learning models

The custom CNN experiments included:

- Increasing the number of filters
- Adding extra convolutional layers
- Testing `GlobalAveragePooling2D`
- Adding Dropout
- Testing different learning-rate behaviour
- Using `EarlyStopping`
- Using `ModelCheckpoint`
- Using `ReduceLROnPlateau`
- Applying data augmentation

The final custom CNN acted as the project baseline for comparison with transfer learning models.

---

### Transfer Learning

The second part of the project used pretrained models.

Transfer learning was applied because pretrained CNNs already contain useful visual knowledge learned from large-scale image datasets.

The transfer learning workflow included:

- Loading pretrained model architectures
- Removing the original top classification layer
- Adding a new CIFAR-10 classification head
- Resizing CIFAR-10 images where required
- Applying the correct preprocessing function for each pretrained model
- Training the new classification head
- Fine-tuning selected layers of the pretrained model
- Evaluating each model on the test set

The transfer learning models explored were:

- **EfficientNetB0**
- **DenseNet121**
- **MobileNet / MobileNetV3**

---

## Models Compared

| Model | Approach | Description |
|---|---|---|
| Custom CNN | Built from scratch | Learns all visual features directly from CIFAR-10 |
| EfficientNetB0 | Transfer learning | Uses ImageNet pretrained weights and fine-tuning |
| DenseNet121 | Transfer learning | Uses dense connections to improve feature reuse |
| MobileNet / MobileNetV3 | Transfer learning | Lightweight architecture designed for efficiency |

---

## Evaluation Metrics

The models were evaluated using:

- Accuracy
- Precision
- Recall
- F1-score
- Classification report
- Confusion matrix
- Learning curves for accuracy and loss

The confusion matrix was especially important because it showed which classes were most frequently confused by each model.

Accuracy alone gives a useful overall score, but it does not explain where the model is making mistakes. For that reason, we also inspected class-level behaviour using classification reports and confusion matrices.

---

## Results Summary

The final model comparison on test data was approximately:

| Model | F1-score |
|---|---:|
| Custom CNN | 0.73 |
| EfficientNetB0 | 0.88 |
| MobileNetV3 | 0.92 |
| DenseNet121 | 0.95 |

Overall, transfer learning models outperformed the custom CNN.

The custom CNN provided a strong learning baseline, while the pretrained models showed the advantage of starting from reusable visual features learned from larger datasets.

---

## Key Findings

### Custom CNN

- The custom CNN achieved reasonable performance but had to learn all features from scratch.
- Data augmentation helped improve robustness.
- Dropout helped reduce overfitting.
- Learning curves were essential for deciding the next experiment.
- The model still struggled with visually similar classes.
- The final custom CNN became a useful benchmark for evaluating transfer learning models.

### EfficientNetB0

- EfficientNetB0 performed better than the custom CNN.
- The pretrained ImageNet weights gave the model a stronger starting point.
- Fine-tuning improved performance compared with using only a frozen base.
- Conservative fine-tuning was used to avoid damaging pretrained weights.
- Main remaining errors were concentrated in visually similar classes.

### DenseNet121

- DenseNet121 achieved the strongest result among the tested models.
- Dense connections helped improve feature reuse across layers.
- Fine-tuning improved the model after the frozen setup reached its limit.
- Regularisation and careful fine-tuning were important due to overfitting risk.

### MobileNet / MobileNetV3

- MobileNet models provided a strong balance between performance and efficiency.
- These models are lightweight compared with larger transfer learning architectures.
- MobileNetV3 achieved strong results while keeping computational cost lower.

---

## Challenges and Lessons Learned

### Main Challenges

- CIFAR-10 images are very small, only 32×32 pixels.
- Some classes are visually similar, such as:
  - cat and dog
  - automobile and truck
  - airplane and ship
  - bird and deer
- Some models showed signs of overfitting.
- Colab runtime and memory constraints affected experimentation.
- Larger image resizing improved transfer learning possibilities but increased memory usage.
- Fine-tuning pretrained models required careful learning-rate control.
- Running many experiments required clear model naming and saved outputs to avoid losing progress.

### Main Lessons

- Accuracy alone is not enough; confusion matrices reveal deeper class-level behaviour.
- Learning curves are essential for diagnosing underfitting and overfitting.
- Data augmentation can improve generalisation, but it must be applied carefully.
- Transfer learning can significantly outperform a custom CNN when pretrained features are useful.
- Fine-tuning should usually be done with a low learning rate.
- For very low-resolution datasets, less conservative fine-tuning may sometimes be worth testing.
- Saving checkpoints and final models is critical when working in Colab.
- Clear experiment tracking makes it easier to explain results later.

---

## How to Run the Project

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/cifar10-cnn-transfer-learning.git
cd cifar10-cnn-transfer-learning
```

### 2. Create a virtual environment

Using `venv`:

```bash
python -m venv venv
```

Activate it:

```bash
# macOS / Linux
source venv/bin/activate
```

```bash
# Windows
venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Open Jupyter Notebook

```bash
jupyter notebook
```

Then open the notebooks inside the `notebooks/` folder.

Recommended order:

```text
01_custom_cnn_experiments.ipynb
02_efficientnetb0_transfer_learning.ipynb
03_densenet121_transfer_learning.ipynb
04_mobilenet_transfer_learning.ipynb
```

---

## Requirements

Main Python libraries used:

```text
tensorflow
numpy
pandas
matplotlib
seaborn
scikit-learn
jupyter
```

A typical `requirements.txt` file should include:

```text
tensorflow
numpy
pandas
matplotlib
seaborn
scikit-learn
jupyter
```

---

## Project Deliverables

This repository includes:

- Custom CNN experimentation notebook
- EfficientNetB0 transfer learning notebook
- DenseNet121 transfer learning notebook
- MobileNet / MobileNetV3 transfer learning notebook
- Learning curves
- Confusion matrices
- Classification reports
- Model comparison tables
- Final presentation slides

---

## Future Improvements

Possible future work includes:

- Testing larger input sizes for transfer learning, such as `128×128`
- Applying stronger but controlled data augmentation
- Fine-tuning more layers in EfficientNetB0
- Comparing fixed low learning rates such as `1e-5` and `1e-4`
- Testing additional pretrained architectures
- Using Grad-CAM or similar explainability methods
- Creating a Streamlit demo for model predictions
- Improving code modularity with reusable Python scripts
- Saving and loading models through external storage when model files are too large for GitHub

---

## Team Members

Add the GitHub usernames of the three team members below:

| Role | GitHub Username |
|---|---|
| Nicole Segura | [@nicolesegura121](https://github.com/nicolesegura121) |
| Satishbabu Rajagopal | [@satishbabu06](https://github.com/satishbabu06) |
| Vítor Ferraz | [@vitorferraz19](https://github.com/vitorferraz19) |

---

## Credits

This project was completed as part of a deep learning computer vision assignment focused on CNNs and transfer learning.

The project uses:

- CIFAR-10 dataset
- TensorFlow / Keras
- Scikit-learn
- Matplotlib
- Seaborn
- Pretrained Keras Applications models

---

## License

This project is intended for educational purposes.

If you want to make the repository open source, add a licence such as MIT, Apache 2.0, or GPL.

A common option is the MIT License.

You can choose a licence using:

```text
https://choosealicense.com/
```