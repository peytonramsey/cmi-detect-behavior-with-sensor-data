# Data Dictionary

## train & test .csv

| Column | Description |
|---|---|
| row_id | Unique identifier for each row in the dataset. |
| sequence_id | An ID for the batch of sensor data. Each sequence includes one Transition, one Pause, and one Gesture. |
| sequence_type | If the gesture is a target or non-target type. Train only. |
| sequence_counter | A counter of the row within each sequence. |
| subject | A unique ID for the subject who provided the data.
| gesture | The target column. Description of sequence Gesture. Train only.
| orientation | Description of the subject's orientation during the sequence. Train only.
| behavior | A description of the subject's behavior during the current phase of the sequence.
| acc_[x/y/z] | Measure linear acceleration along three axes in meters per second squared from the IMU sensor.
| rot_[w/x/y/z] | Orientation data which combines information from the IMU's gyroscope, accelerometer, and magnetometer to describe the device's orientation in 3D space.
| thm_[1-5] | There are five thermopile sensors on the watch which record temperature in degrees Celsius. Note that the index/number for each corresponds to the index in the photo on the Overview tab.
| tof_[1-5]_v[0-63] | There are five time-of-flight sensors on the watch that measure distance. In the dataset, the 0th pixel for the first time-of-flight sensor can be found with column name tof_1_v0, whereas the final pixel in the grid can be found under column tof_1_v63. This data is collected row-wise, where the first pixel could be considered in the top-left of the grid, with the second to its right, ultimately wrapping so the final value is in the bottom right (see image above). The particular time-of-flight sensor is denoted by the number at the start of the column name (e.g., 1_v0 is the first pixel for the first time-of-flight sensor while 5_v0 is the first pixel for the fifth time-of-flight sensor). If there is no sensor response (e.g., if there is no nearby object causing a signal reflection), a -1 is present in this field. Units are uncalibrated sensor values in the range 0-254. Each sensor contains 64 pixels arranged in an 8x8 grid, visualized in the figure below.

## train & test demographics.csv

These tabular files contain demographic and physical characteristics of the participants.

| Column | Description |
|---|---|
| subject | A unique ID for the subject who provided the data. |
| adult_child | Indicates whether the participant is a child (0) or an adult (1). Adults are defined as individuals aged 18 years or older. |
| age | Participant's age in years at time of data collection. |
| sex | Participants sex assigned at birth, 0= female, 1 = male. |
| handedness | Dominant hand used by the participant, 0 = left-handed, 1 = right-handed. |
| height_cm | Height of the participant in centimeters. |
| shoulder_to_wrist_cm | Distance from shoulder to wrist in centimeters. |
| elbow_to_wrist_cm | Distance from elbow to wrist in centimeters. |

