# CMI Detect Behavior with Sensor Data

A wrist-worn sensor classification problem focused on building a model that distinguishes body-focused repetitive behavior like motions from non-BFRB gestures using time-series signals collected from a wrist-worn device, including IMU, thermopile, and time-of-flight sensors.

The project is intended as an end-to-end study in multimodal machine learning under realistic constraints. The core challenge is to learn robust behavioral patterns from noisy sequential data while handling sensor-specific structure, subject variation, and missing signals that appear in the evaluation setting.

Aims to develop a predictive model capable of distinguishing (1) BFRB-like gestures from non-BFRB-like gestures and (2) the specific type of BFRB-like gesture.

## Project Context

This project uses the dataset released through the Child Mind Institute's **CMI - Detect Behavior with Sensor Data** challenge, which focuses on detecting body-focused repetitive behaviors from wrist-worn sensor data.

Although the data was originally distributed through a Kaggle competition, this repository is structured as an independent machine learning project rather than a competition entry. The goal is to study how multimodal wearable signals, including motion, temperature, and proximity data, can be used to distinguish BFRB-like gestures from similar everyday movements.

The broader motivation comes from the Child Mind Institute's **Healthy Brain Network**, an open science initiative that shares de-identified behavioral and mental health related data to support research in child and adolescent psychiatry.

## Repository Structure

- `eda-01.qmd`: Exploratory analysis of sensor distributions, sequence structure, missing sensor patterns, and class balance across BFRB and non-BFRB gestures.
- `feature-engineering.qmd`: Construction of engineered statistical features (32 IMU, 6 thermopile, 5 ToF) from raw sensor sequences, including zero-fill handling for IMU-only sequences.
- `modeling_baseline.qmd`: Baseline model training (Random Forest, XGBoost) with subject-aware cross-validation and sensor-ablation experiments.
- `model_comparison.qmd`: Comparison of engineered-feature tree models against raw-sequence deep learning models (1D-CNN, LSTM, GRU), missing-modality handling strategies, ensembling, post-processing, and interpretability analysis (feature importance, SHAP).
- `data-dictionary.md`: Column-level documentation for the sensor, demographic, and label data.

## Key Results

The best-performing model is an XGBoost classifier on engineered statistical features, reaching a macro F1 of 0.5241 on full-sensor sequences, ahead of a 1D-CNN trained on raw IMU time-series (macro F1 0.4414) and recurrent models (GRU 0.3414, LSTM 0.2796) [file:8]. Hand-crafted statistical aggregations (e.g., acceleration standard deviation, thermopile mean) capture most of the discriminative signal in the raw sensor trace, and deep sequence models did not clearly surpass the tree-based baseline at the scale evaluated here.

For sequences missing thermopile and time-of-flight sensors (IMU-only), training separate models per modality condition performed marginally better than a single unified model with zero-filled missing channels (macro F1 0.5894 vs. 0.5830 overall), though the gap is small and the IMU-only subset (96 sequences) is too limited for a fully confident ranking. Ensembling the tree model with deep sequence models (majority vote) did not outperform the tree model alone (0.5646 vs. 0.5807), and post-processing and probability calibration likewise did not improve macro F1 on this 18-class problem.

Interpretability analysis shows thermopile features (thm_g1, thm_mean) rank among the top predictors alongside IMU statistics, and SHAP analysis confirms thermopile contributes a larger share of prediction signal for BFRB gestures (24.8%) than non-BFRB gestures (21.1%), consistent with the intuition that BFRB gestures involve sustained skin or hair contact with the wrist sensor.

## Validation Approach

All models are evaluated using subject-aware GroupKFold cross-validation, where folds are split by `subject` rather than by row or sequence. This prevents data leakage that would occur if the same participant's movement patterns appeared in both training and validation folds, which would otherwise inflate performance estimates given that individual gesture styles are strongly subject-specific.

Macro F1 is used as the primary metric across all 18 gesture classes to avoid overweighting frequent classes, given the class imbalance between the 12 BFRB and 6 non-BFRB gesture types documented in the data dictionary.

## Limitations

- **Small IMU-only subset:** only 96 of 8,151 sequences lack thermopile/ToF sensors, so macro F1 estimates on this subset are high-variance and should be treated as indicative rather than conclusive.
- **Fold count mismatch:** tree-based models were evaluated on 5 GroupKFold splits, while deep learning models were evaluated on 3 folds due to training time constraints, so direct score comparisons carry some uncertainty.
- **Fold-to-fold variance in deep learning models:** the 1D-CNN's macro F1 ranged from 0.3857 to 0.4848 across folds on the same input, indicating the reported means should be read alongside this spread rather than as a single precise value.
- **Ensembling and post-processing did not improve results:** majority-vote ensembling and confidence-threshold post-processing both underperformed the best single model, which is reported here as a genuine negative finding rather than an implementation gap.
- **Calibration is structurally inert for this metric:** temperature scaling, Platt scaling, and isotonic regression all preserve argmax class assignments, so none can change macro F1 by construction; calibration would only matter for probability-based downstream metrics not used in this project.

> **Resources:** [Data Dictionary](data-dictionary.md)

