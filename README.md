# PG-Group-3 — Multimodal Skin Lesion Classification (Skin Cancer Detection)

> F21DL – Data Mining & Machine Learning · Group Coursework · Heriot-Watt University Dubai

**Coursework submission:** A ZIP archive containing the final project code is also uploaded on Canvas Group Files section as part of the coursework submission. The GitHub repository additionally preserves the group's individual development contributions and experimental work.

## Repository Structure

The repository is organised to keep the **final consolidated code** separate from the group's individual development contributions.

- **`Final Code Files/`** - Contains the final, organised implementation of the project, including the tabular, image-based and fusion pipelines, along with the relevant outputs. This is the main folder to refer to for the final code and reported results.
- **Other root-level code folders** - Contain the individual group members' contributions, draft implementations, exploratory notebooks and experimental work developed throughout the project. These have been retained to document the group's work and development process. It's kept for reference and isn't needed to reproduce the results.

This structure keeps the final implementation clearly identifiable while preserving the contributions of all group members.

## Project Overview

This project investigates machine-learning approaches for classifying skin lesions into **six diagnostic categories** using two complementary data modalities: **clinical images** and **patient/lesion metadata**.

Using the **PAD-UFES-20** dataset, we compare models trained on clinical metadata alone, models trained on lesion images alone, and a multimodal approach that combines both.

**Key finding:** late fusion of the image and clinical models gave the best results (macro-F1 **0.749**, vs. 0.647 image-only and 0.661 clinical-only).

## Aim

To develop and evaluate machine-learning approaches for classifying skin lesions using clinical patient/lesion information and smartphone-captured lesion images.

## Motivation

Early and accurate identification of suspicious skin lesions can support clinical decision-making. Smartphone-captured clinical images are also closer to real-world image acquisition than images taken only under controlled dermoscopic conditions.

This project explores whether visual information, clinical context, or a combination of both gives the most useful information for automated skin-lesion classification.

## Research Questions

| | Question | Outcome |
|---|---|---|
| RQ1 | How effectively can classical ML models classify lesions using clinical metadata? | Partly supported: good on common classes, weak on rare malignant ones |
| RQ2 | How effectively can CNN-based models classify lesions using images? | Supported for pretrained (transfer-learning) models |
| RQ3 | Does combining clinical metadata and image features improve performance compared with either modality alone? | Supported for late fusion |

**Hypothesis:** combining image information with clinical metadata provides complementary information and improves classification performance compared with a single modality.

## Dataset

### PAD-UFES-20

A publicly available dataset linking smartphone-captured clinical images of skin lesions with patient and lesion metadata.

| Characteristic | Value |
|---|---|
| Patients | 1,373 |
| Unique lesions | 1,641 |
| Clinical images | 2,298 |
| Diagnostic classes | 6 |
| Metadata attributes | 26 |

| Class | Diagnosis | Images |
|---|---|---|
| BCC | Basal cell carcinoma | 845 |
| ACK | Actinic keratosis | 730 |
| NEV | Nevus | 244 |
| SEK | Seborrheic keratosis | 235 |
| SCC | Squamous cell carcinoma | 192 |
| MEL | Melanoma | 52 |

The metadata includes clinical variables such as age, sex, Fitzpatrick skin type, lesion location, lesion diameter and reported symptoms, plus identifiers and diagnostic information.

### Why PAD-UFES-20?

- **Real-world clinical images:** smartphone photos vary in lighting, resolution and image quality.
- **Complementary data modalities:** each image is linked to patient/lesion metadata, so modalities can be compared and combined.
- **Clinically relevant categories:** six classes covering both cancer and non-cancer lesions.
- **Research suitability:** previous work has explored CNNs, clinical metadata and image–metadata fusion on this dataset.
- **Class imbalance:** classes are unequally represented (~16:1), so class-wise evaluation is important.

## Project Approach

**Data preparation**
- Removed duplicate and conflicting images and repeated lesion rows.
- Dropped leakage columns (identifiers, biopsy status).
- Used **patient-level splits** (`StratifiedGroupKFold`) so no patient appears in both train and test.

### 1. Metadata-only classification
Clinical metadata was used to train:
- **Supervised models:** logistic regression, SVM, random forest, decision tree, gradient boosting, perceptron and Naïve Bayes.
- **Exploratory and probabilistic models:** k-means and GMM clustering, and probabilistic classifiers.

Imbalance strategies compared: class weighting and SMOTE-NC.

### 2. Image-only classification
- **Models:** a custom CNN, plus ImageNet-pretrained **ResNet50** and **EfficientNetB0** (frozen and fine-tuned), in TensorFlow/Keras.
- **Preprocessing:** images resized to 224×224 and augmented.
- **Imbalance handling:** class weighting, oversampling and focal loss were compared.

### 3. Image + metadata classification
- **Late fusion:** a weighted average of the image and clinical model probabilities (image weight 0.4, chosen by cross-validation).
- **Intermediate fusion:** a single network that combines image and tabular features.

Both were compared against the single-modality models on the same patient split.

## Evaluation

Model performance was assessed using:

- **Accuracy:** overall proportion of correct predictions.
- **Precision:** how often predictions for a class are correct.
- **Recall:** how effectively the model identifies samples of a class.
- **F1-score:** the balance between precision and recall.

Because the dataset is class-imbalanced, **macro-F1** was the main metric, and class-wise performance was examined alongside overall accuracy. Balanced accuracy, MCC and ROC-AUC were also reported.

Models were selected by cross-validation and evaluated once on a held-out test fold. A patient-level bootstrap was used to test significance.

## Results (held-out test set, 468 images)

| Model | Accuracy | Macro-F1 | ROC-AUC |
|---|---|---|---|
| Clinical only (Logistic Regression) | 0.752 | 0.661 | 0.919 |
| Image only (EfficientNetB0) | 0.722 | 0.647 | 0.907 |
| **Late fusion** | **0.803** | **0.749** | **0.945** |
| Intermediate fusion | 0.667 | 0.651 | 0.916 |

- Late fusion's gain over the image-only model is statistically significant.
- **SCC** remains the hardest class (often confused with BCC), and melanoma results rest on very few test cases, so the models are **not ready for clinical use**.

Full methodology, results and discussion are in the project report.


## Dataset Sources and References

- Original PAD-UFES-20 dataset paper: https://www.sciencedirect.com/science/article/pii/S235234092031115X
- Dataset on Kaggle: https://www.kaggle.com/datasets/mahdavi1202/skin-cancer/data

## Dataset Download and Setup

The PAD-UFES-20 dataset is publicly available for download:

- [Download PAD-UFES-20 from Kaggle](https://www.kaggle.com/datasets/mahdavi1202/skin-cancer/data)

**Note:** The complete dataset has not been uploaded to this repository due to its large size. Users must download and extract the dataset before running the notebooks.

After downloading, place the dataset in the corresponding data directory expected by the notebooks in each of the following folders:

- `Final Code Files/Tabular_src-code/` – For tabular/clinical metadata experiments.
- `Final Code Files/Image_EDA_and_Training/` – For image-based experiments.
- `Final Code Files/fusion/` – For multimodal fusion experiments, which require both images and clinical metadata.

Ensure that the dataset directory and file paths match those specified in the respective notebooks or configuration files.

## How to Run

1. Clone the repository and download the PAD-UFES-20 dataset using the link provided above.
2. Extract the dataset and place the required files in the corresponding directories, as described in the Dataset Download and Setup section.
3. Install the required dependencies:

   `pandas numpy scikit-learn imbalanced-learn tensorflow opencv-python matplotlib seaborn`

4. Navigate to `Final Code Files/` and run the notebooks in the relevant subfolder:

   - **Tabular (`Tabular_src-code/`):** Run the clinical metadata EDA and preprocessing notebooks, followed by the tabular modelling experiments.
   - **Image (`Image_EDA_and_Training/`):** Run the image EDA notebook, followed by image preprocessing and training.
   - **Fusion (`fusion/`):** Run the multimodal fusion notebooks after preparing the image and clinical data.

Refer to the individual notebooks for any additional execution instructions or data-path configuration.

## Outputs and Model Artefacts

- **Tabular:** Experiment outputs are available in the `Output/` folder.
- **Image-based and multimodal:** The notebooks save their outputs and trained model artefacts in the respective artifacts folders within their project directories. These files are not included in the GitHub repository due to their size. 
- The image and fusion notebooks contain the code required to train the models and generate the corresponding artefacts.


## Team — Dubai PG Group 3

Krishnendu Palotu Veetil · Rekha Rajan · Husna Ahmed · Hasna Mohammad Sayed Ahmed · Saima Zohra
