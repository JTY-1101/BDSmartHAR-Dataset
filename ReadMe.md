# BDSmartHAR Dataset

## 1. Introduction

**BDSmartHAR** is a smartphone-based human activity recognition dataset collected under real-world daily conditions. The dataset is designed for research on smartphone-based Human Activity Recognition (HAR), especially for applications related to intelligent navigation, mobile sensing, and terminal-side activity recognition.

The complete BDSmartHAR dataset contains data from **18 subjects** and covers **11 fine-grained activity-placement classes**. This public repository provides a representative subset of BDSmartHAR, including data from **6 subjects**, for demonstrating the dataset structure, sensor format, label format, and recommended usage. Access to the complete dataset requires permission from the authors.

Unlike many conventional HAR datasets collected in controlled laboratory environments or with fixed device placements, BDSmartHAR focuses on realistic smartphone usage conditions. In daily life, users may hold the phone in hand, place it in a pocket, use it near the ear, or mount it on a bicycle or vehicle. These carrying conditions can significantly affect accelerometer and gyroscope signals, even when the user performs the same activity.

Therefore, BDSmartHAR jointly considers **human activity states** and **smartphone placement postures** as fine-grained activity-placement classes. This design better reflects practical smartphone-based HAR scenarios, where both the user's motion state and the phone's carrying condition are relevant to subsequent applications such as pedestrian dead reckoning, navigation assistance, behavior-aware localization, and context-aware mobile sensing.

## 2. Dataset Name

The dataset is named **BDSmartHAR**.

## 3. Public Subset and Complete Dataset

This repository contains a public subset of BDSmartHAR.

| Item | Description |
|---|---|
| Public subset | Data from 6 subjects |
| Complete dataset | Data from 18 subjects |
| Access to complete dataset | Requires permission from the authors |
| Data type | Smartphone inertial sensor data |
| Label type | One-hot encoded activity-placement labels |
| Application scope | Academic research only |

The public subset is intended to provide a clear description of the data organization, sensor channels, label format, and data usage. Researchers who need the complete 18-subject dataset should contact the authors and obtain authorization before use.

## 4. Main Features

BDSmartHAR has the following characteristics:

- Real-world data collection under uncontrolled daily conditions.
- Smartphone-based inertial sensing using accelerometer and gyroscope data.
- Complete dataset containing 18 subjects.
- Public subset containing 6 subjects.
- 11 fine-grained activity-placement classes.
- Multiple common smartphone placement postures.
- Windowed sensor samples with a fixed shape for deep learning models.
- Subject-level organization to support cross-user validation.
- One-hot encoded labels for multi-class classification.
- Designed to support research on HAR, mobile sensing, and intelligent navigation.

## 5. Dataset Design Motivation

The dataset was constructed based on three principles: **scene authenticity**, **category completeness**, and **sample balance**.

### 5.1 Scene Authenticity

The data were collected in daily environments rather than strictly controlled laboratory settings. This helps reflect the diversity of real smartphone usage, including natural motion patterns, different walking and running styles, and varying carrying conditions.

### 5.2 Category Completeness

The dataset covers common static, dynamic, and transportation-related activities. It also distinguishes several smartphone placement postures under the same activity, forming fine-grained activity-placement classes.

### 5.3 Sample Balance

The data collection process was designed to keep the sample duration and sample quantity of different activity classes relatively balanced, reducing severe category imbalance during model training.

## 6. Subjects

The complete BDSmartHAR dataset contains data from **18 subjects**:

- subject01
- subject02
- subject03
- subject04
- subject05
- subject06
- subject07
- subject08
- subject09
- subject10
- subject11
- subject12
- subject13
- subject14
- subject15
- subject16
- subject17
- subject18

The public repository provides a representative subset of **6 subjects**:

- subject01
- subject02
- subject03
- subject04
- subject05
- subject06

Each subject has a separate folder. The subject-level folder structure is intended to support subject-independent evaluation, such as cross-user validation.

Access to the remaining subject data requires authorization from the authors.

## 7. Sensors

The dataset uses smartphone inertial sensors:

- Accelerometer
- Gyroscope

The sampling frequency is **50 Hz**.

Each data sample contains six sensor channels:

| Channel Index | Sensor Channel |
|---|---|
| 0 | acc_x |
| 1 | acc_y |
| 2 | acc_z |
| 3 | gyro_x |
| 4 | gyro_y |
| 5 | gyro_z |

The accelerometer channels record three-axis acceleration measurements, and the gyroscope channels record three-axis angular velocity measurements.

## 8. Activity-Placement Classes

BDSmartHAR contains **11 fine-grained activity-placement classes**:

| Label Index | Class Name | Description |
|---|---|---|
| 0 | Stand (Hand) | Standing while holding the smartphone in hand |
| 1 | Stand (Phone) | Standing while placing the smartphone near the ear or in a phone-use posture |
| 2 | Stand (Pocket) | Standing with the smartphone in pocket |
| 3 | Walk (Hand) | Walking while holding the smartphone in hand |
| 4 | Walk (Phone) | Walking while placing the smartphone near the ear or in a phone-use posture |
| 5 | Walk (Pocket) | Walking with the smartphone in pocket |
| 6 | Run (Hand) | Running while holding the smartphone in hand |
| 7 | Run (Pocket) | Running with the smartphone in pocket |
| 8 | Cycle (Mount) | Cycling with the smartphone mounted |
| 9 | Cycle (Pocket) | Cycling with the smartphone in pocket |
| 10 | Vehicle (Mount) | Riding in a vehicle with the smartphone mounted |

The labels are stored in one-hot encoding format. Each label vector has 11 dimensions, corresponding to the 11 activity-placement classes listed above.

## 9. Dataset Structure

The public subset is provided as `dataset.zip`. After extraction, the folder structure is organized by subject as follows:

- dataset/
  - subject01/
    - data.npy
    - label.npy
  - subject02/
    - data.npy
    - label.npy
  - subject03/
    - data.npy
    - label.npy
  - subject04/
    - data.npy
    - label.npy
  - subject05/
    - data.npy
    - label.npy
  - subject06/
    - data.npy
    - label.npy
  - README.md

Each subject folder contains two files:

| File Name | Description |
|---|---|
| data.npy | Windowed sensor samples of the corresponding subject |
| label.npy | One-hot encoded activity-placement labels of the corresponding subject |

The complete BDSmartHAR dataset contains 18 subject folders. Researchers who need access to the complete dataset should contact the authors and obtain authorization before use.

## 10. Data Format

For each subject folder:

| File | Shape | Description |
|---|---|---|
| data.npy | (N, 128, 6) | Windowed smartphone inertial sensor samples |
| label.npy | (N, 11) | One-hot encoded activity-placement labels |

where:

| Dimension | Meaning |
|---|---|
| N | Number of samples for the corresponding subject |
| 128 | Window length |
| 6 | Number of sensor channels |
| 11 | Number of activity-placement classes |

Each sample in `data.npy` contains 128 consecutive time steps and six sensor channels. Each label in `label.npy` is represented as an 11-dimensional one-hot vector.

## 11. Window Segmentation

The original continuous sensor recordings were segmented using a sliding-window strategy.

The window length is **128 sampling points**. At a sampling frequency of 50 Hz, this corresponds to approximately **2.56 seconds**.

The provided dataset files have already been segmented into fixed-length samples with the shape **(128, 6)**.

## 12. Recommended Evaluation Protocol

To evaluate cross-user generalization, we recommend using a subject-level validation protocol.

In the associated study, the 18 subjects were divided into six mutually exclusive folds. In each round:

- one fold was used as the test set;
- the remaining five folds were used as the training set;
- no subject appeared in both the training set and the test set.

This subject-level protocol is recommended because random sample-level splitting may cause subject leakage, leading to overly optimistic results.

A typical subject-level six-fold split for the complete dataset may follow this structure:

| Fold | Test Subjects |
|---|---|
| Fold 1 | subject01, subject02, subject03 |
| Fold 2 | subject04, subject05, subject06 |
| Fold 3 | subject07, subject08, subject09 |
| Fold 4 | subject10, subject11, subject12 |
| Fold 5 | subject13, subject14, subject15 |
| Fold 6 | subject16, subject17, subject18 |

Users may also define their own subject-level folds, but the subject partition should be clearly reported in any publication using this dataset.

## 13. Important Notes on Evaluation

When using BDSmartHAR, please avoid mixing samples from the same subject into both training and testing sets unless your purpose is explicitly within-subject evaluation.

For cross-user HAR research, subject-independent evaluation is strongly recommended.

Recommended practice:

- Use subject-level splits for training and testing.
- Report the subject partition protocol clearly.
- Report mean and standard deviation when using cross-validation.
- Avoid sample-level random splitting if the goal is cross-user generalization.

## 14. Potential Applications

BDSmartHAR may be used for research on:

- smartphone-based human activity recognition;
- sensor-based activity classification;
- cross-user HAR model evaluation;
- feature learning for inertial sensor data;
- activity-placement recognition;
- mobile sensing;
- intelligent navigation;
- pedestrian dead reckoning assistance;
- terminal-side HAR deployment;
- lightweight deep learning models for mobile devices;
- context-aware smartphone sensing.

## 15. Limitations

The current version of BDSmartHAR has the following limitations:

- The complete dataset contains 18 subjects, which is still limited in scale.
- The public repository only provides a representative subset of 6 subjects.
- The dataset focuses on 11 predefined activity-placement classes.
- The dataset contains smartphone inertial sensor data only.
- Environmental and device diversity may still be further expanded.
- The dataset is designed primarily for academic research and may require further validation before being used in practical systems.

Future versions may include more subjects, more device types, more navigation-related activities, and additional sensor modalities.

## 16. Usage and Authorization

The public subset of BDSmartHAR is provided for academic research and dataset-format demonstration purposes.

Use of the complete BDSmartHAR dataset requires prior permission from the authors. Researchers who intend to use the complete dataset should contact the authors and describe their research purpose before access is granted.

Unauthorized redistribution, commercial use, or use beyond the approved research scope is not permitted.

To request permission, please contact:

| Contact | Email |
|---|---|
| Tingyuan Jiang | jiangtingyuan24@mails.ucas.ac.cn |

When requesting permission, please include the following information:

- your name;
- your affiliation;
- your email address;
- your intended research purpose;
- whether the dataset will be used in a publication;
- whether the dataset will be used for benchmarking or model development;
- whether any derived data, trained models, or analysis results will be redistributed.

Use of the complete dataset is allowed only after approval from the dataset authors.

## 17. Redistribution Policy

The complete dataset may not be redistributed without written permission from the authors.

Users are not allowed to:

- upload the complete dataset to other public repositories;
- share the complete dataset with unauthorized third parties;
- use the dataset for commercial purposes without approval;
- modify and redistribute the dataset as a new dataset;
- remove or alter the dataset documentation, authorship information, or usage requirements.

## 18. Acknowledgment

This dataset was constructed as part of research on smartphone-based human activity recognition and intelligent navigation.

The authors thank all participants involved in the data collection process.

## 19. Disclaimer

The dataset is provided for academic research purposes only. The authors make no warranties regarding the completeness, accuracy, or suitability of the dataset for any specific application.

Users are responsible for ensuring that their use of the dataset complies with applicable laws, institutional rules, and ethical requirements.

## 20. Contact

For questions about the dataset, permission requests, or citation updates, please contact:

| Contact | Email |
|---|---|
| Tingyuan Jiang | jiangtingyuan24@mails.ucas.ac.cn |
| Liang Wang | wangliang@aircas.ac.cn |