# CMI Detect Behavior with Sensor Data

A wrist-worn sensor classification problem focused on building a model that distinguishes body-focused repetitive behavior like motions from non-BFRB gestures using time-series signals collected from a wrist-worn device, including IMU, thermopile, and time-of-flight sensors.

The project is intended as an end-to-end study in multimodal machine learning under realistic constraints. The core challenge is to learn robust behavioral patterns from noisy sequential data while handling sensor-specific structure, subject variation, and missing signals that appear in the evaluation setting.

Aims to develop a predictive model capable of distinguishing (1) BFRB-like gestures from non-BFRB-like gestures and (2) the specific type of BFRB-like gesture.

## Project Context

This project uses the dataset released through the Child Mind Institute's **CMI - Detect Behavior with Sensor Data** challenge, which focuses on detecting body-focused repetitive behaviors from wrist-worn sensor data.

Although the data was originally distributed through a Kaggle competition, this repository is structured as an independent machine learning project rather than a competition entry. The goal is to study how multimodal wearable signals, including motion, temperature, and proximity data, can be used to distinguish BFRB-like gestures from similar everyday movements.

The broader motivation comes from the Child Mind Institute's **Healthy Brain Network**, an open science initiative that shares de-identified behavioral and mental health related data to support research in child and adolescent psychiatry.

> **Resources:** [Data Dictionary](data-dictionary.md)

