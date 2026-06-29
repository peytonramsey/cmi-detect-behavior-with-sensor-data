# Data Dictionary

Quaternion: A four-value representation of 3D rotation used by IMU sensors to track how the wrist device is oriented during movement

Columns like **rot_w**, **rot_x**, **rot_y**, and **rot_z** help capture whether the hand is turning, tilting, or facing a different direction, which can matter for distinguishing one gesture from another

## train.csv

| Column | Description |
|---|---|
| sequence_id | Unique identifier for each gesture sequence. |
| gesture | Target label for the sequence, the gesture to predict. |
| behavior_phase | Stage of the sequence, such as transition, pause, or gesture. |
| acc_x | X-axis accelerometer reading from the IMU. |
| acc_y | Y-axis accelerometer reading from the IMU. |
| acc_z | Z-axis accelerometer reading from the IMU. |
| rot_w | Rotation related IMU measurement, quaternion w component. |
| rot_x | Rotation related IMU measurement, quaternion x component. |
| rot_y | Rotation related IMU measurement, quaternion y component. |
| rot_z | Rotation related IMU measurement, quaternion z component. |
| tmp1 to tmpN | Thermopile sensor readings capturing heat patterns near the wrist device. |
| tof1 to tofN | Time-of-flight sensor readings capturing proximity or distance patterns. |

## test.csv

| Column | Description |
|---|---|
| sequence_id | Unique identifier for each gesture sequence. |
| behavior_phase | Stage of the sequence, such as transition, pause, or gesture. |
| acc_x | X-axis accelerometer reading from the IMU. |
| acc_y | Y-axis accelerometer reading from the IMU. |
| acc_z | Z-axis accelerometer reading from the IMU. |
| rot_w | Rotation related IMU measurement, quaternion w component. |
| rot_x | Rotation related IMU measurement, quaternion x component. |
| rot_y | Rotation related IMU measurement, quaternion y component. |
| rot_z | Rotation related IMU measurement, quaternion z component. |
| tmp1 to tmpN | Thermopile sensor readings capturing heat patterns near the wrist device. |
| tof1 to tofN | Time-of-flight sensor readings capturing proximity or distance patterns. |

## train_demographics.csv

| Column | Description |
|---|---|
| participant_id | Unique identifier for each participant. |
| demographic fields | Participant-level metadata such as age, sex, handedness, or related attributes, exact columns should be confirmed from the file. |

## test_demographics.csv

| Column | Description |
|---|---|
| participant_id | Unique identifier for each participant. |
| demographic fields | Participant-level metadata for test participants, exact columns should be confirmed from the file. |

## sample_submission.csv

| Column | Description |
|---|---|
| sequence_id | Unique identifier for each test sequence. |
| gesture | Predicted gesture label for the sequence. |