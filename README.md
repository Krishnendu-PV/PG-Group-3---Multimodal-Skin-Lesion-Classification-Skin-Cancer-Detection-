# PG-Group-3---Multimodal-Skin-Lesion-Classification-Skin-Cancer-Detection-

## Project Overview

This project investigates machine-learning approaches for classifying
skin lesions into six diagnostic categories using two complementary data
modalities: clinical images and patient/lesion metadata.

Using the **PAD-UFES-20** dataset, we aim to compare models trained on
clinical metadata alone, models trained on lesion images alone, and a
multimodal approach that combines information from both.

The project is being carried out as part of the **F21DL -- Data Mining &
Machine Learning** coursework.

## Aim

To develop and evaluate machine-learning approaches for classifying skin
lesions using clinical patient/lesion information and
smartphone-captured lesion images.

## Motivation

Early and accurate identification of suspicious skin lesions can support
clinical decision-making. Smartphone-captured clinical images also
reflect a more realistic image-acquisition setting than images obtained
exclusively under controlled dermoscopic conditions.

This project explores whether visual information, clinical context, or a
combination of both provides the most useful information for automated
skin-lesion classification.

## Research Questions

1.  How effectively can classical machine-learning models classify
    lesions using clinical metadata?
2.  How effectively can CNN-based models classify lesions using images?
3.  Does combining clinical metadata and image features improve
    classification performance compared with either modality
    independently?

**Hypothesis:** Combining image information with clinical metadata may
provide complementary information and improve classification performance
compared with using a single modality.

## Dataset

### PAD-UFES-20

The project uses the publicly available **PAD-UFES-20** dataset, which
links smartphone-captured clinical images of skin lesions with
associated patient and lesion metadata.

  Dataset characteristic     Description
  ------------------------ -------------
  Patients                         1,373
  Unique lesions                   1,641
  Clinical images                  2,298
  Diagnostic classes                   6
  Metadata attributes                 26

The six diagnostic categories are:

-   **ACK** -- Actinic keratosis
-   **BCC** -- Basal cell carcinoma
-   **MEL** -- Melanoma
-   **NEV** -- Nevus
-   **SCC** -- Squamous cell carcinoma
-   **SEK** -- Seborrheic keratosis

The metadata includes clinical variables such as age, sex, Fitzpatrick
skin type, lesion location, lesion diameter and reported symptoms. The
dataset also contains identifiers and diagnostic information.

### Why PAD-UFES-20?

-   **Real-world clinical images:** Smartphone-captured images include
    variation in lighting, resolution and image quality.
-   **Complementary data modalities:** Clinical images are associated
    with patient/lesion metadata, enabling comparisons across
    modalities.
-   **Clinically relevant categories:** The dataset includes six
    diagnostic classes, covering both cancer and non-cancer lesion
    categories.
-   **Research suitability:** Previous work has explored CNN-based
    classification, clinical metadata and image--metadata fusion using
    PAD-UFES-20.
-   **Class imbalance:** The diagnostic categories are not equally
    represented, making class-wise evaluation important.

## Project Approach

The project is organised around three experiments:

### 1. Metadata-only classification

Clinical metadata will be prepared and used to train machine-learning
models. This experiment will investigate how effectively patient and
lesion characteristics can distinguish between the diagnostic
categories. At least three machine-learning algorithms will be implemented 
and compared using appropriate classification metrics.

### 2. Image-only classification

Skin-lesion images will be preprocessed and used to train CNN-based
image-classification models. Neural-network models will be implemented and 
fine-tuned, with their performance assessed and compared against other 
approaches to investigate the diagnostic information that can be learned 
from visual appearance.

### 3. Image + metadata classification

Image-derived features and clinical metadata features will be combined
in a multimodal model. Its performance will be compared with the
metadata-only and image-only experiments to investigate whether
combining the two modalities provides additional predictive value.

## Evaluation

Model performance will be assessed using:

-   **Accuracy** -- overall proportion of correct predictions.
-   **Precision** -- how often predictions for a class are correct.
-   **Recall** -- how effectively the model identifies samples belonging
    to a class.
-   **F1-score** -- the balance between precision and recall.

Because the dataset is class-imbalanced, evaluation will consider
class-wise performance in addition to overall accuracy.

## Dataset Sources and References

-   **Original PAD-UFES-20 dataset paper:**\
    https://www.sciencedirect.com/science/article/pii/S235234092031115X
-   **Dataset on Kaggle:**\
    https://www.kaggle.com/datasets/mahdavi1202/skin-cancer/data

## Project Status

This repository is under development. Dataset exploration and the
modelling experiments are being carried out as part of the coursework.

Implementation details, preprocessing steps, model architectures,
training configurations, experimental results and conclusions will be
added to this README as the project progresses.
