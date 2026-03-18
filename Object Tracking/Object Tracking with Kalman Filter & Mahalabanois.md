> A Kalman filter tracker is a recursive algorithm that estimates the state (position, velocity) of a moving object by combining noisy sensor measurements with a linear motion model, producing an optimal, smooth, and accurate tracking path. It is widely used in robotics, computer vision, and autonomous driving to predict object trajectories.

The Kalman filter used in the vision system lives here →https://gitlab.stoutagtech.dev/cultivator/cultivator-vision/-/blob/main/tracker/kalman.cpp

Our Kalman Filter

---

- `measurementNoiseCov (R)`: uncertainty of detector measurements `z=[x_meas, y_meas]`.
    
    Smaller `R` => trust detections more; larger `R` => trust model more.
    
- `processNoiseCov (Q)`: uncertainty in motion model/state evolution `x_k = A x_{k-1} + w`.
    
    Here it reflects how much unmodeled motion you expect in `x`, `y`, and especially `vy`.
    
- `errorCovPre (P')`: predicted state uncertainty before correction each step.
    
- `errorCovPost (P)`: corrected state uncertainty after incorporating measurement.
    
- `transitionMatrix (A)`: motion model. In your case:
    
    - `x` constant,
    - `y` advances by `vy*dt`,
    - `vy` constant.
- `measurementMatrix (H)`: maps state to measurement. With default init `eye(2,3)`, it means you measure `x` and `y` directly from state `[x,y,vy]`.
    
- `gain (K)`: Kalman gain computed each update from `P', H, R`; determines blend between prediction and measurement.
    
    Higher when `R` is small or `P'` is large; lower when `R` is large or `P'` is small.
    

---

# **Mahalanobis Distance and Kalman Filtering for Plant Track Association**

In the plant tracking system, **Kalman filtering** and **Mahalanobis distance** are used together to associate new detections with existing plant tracks. This allows the system to robustly match plants between frames even when detections are noisy or partially missing.

---

# **Overview**

The tracking pipeline typically follows this process:

1. **Predict plant positions using a Kalman filter**
2. **Receive new detections from the vision system**
3. **Compute Mahalanobis distance between predictions and detections**
4. **Reject unlikely matches (gating)**
5. **Assign detections to tracks**

This approach allows the tracker to account for **uncertainty in both motion prediction and measurement noise**.

---

# **Kalman Filter Role**

Each plant track maintains a Kalman filter state that describes its estimated position and motion.

A common state vector is:

```
x = [x, y, vx, vy]
```

Where:

- x, y = plant position in image space
- vx, vy = estimated velocity

Every frame the filter performs two steps.

---

## **1. Prediction Step**

The filter predicts where the plant should appear in the next frame.

```
x_pred = F * x
P_pred = F * P * Fᵀ + Q
```

Where:

- x_pred = predicted state
- P_pred = predicted covariance (uncertainty)
- F = motion model
- Q = process noise

The covariance matrix P_pred describes how uncertain the prediction is.

Examples:

|**Situation**|**Covariance**|
|---|---|
|Stable track|Small uncertainty|
|New or noisy track|Larger uncertainty|

This uncertainty is critical for the next step.

---

# **Detection Input**

The vision model produces plant detections each frame, for example:

```
detections = [
  (100, 448),
  (500, 430),
  (105, 452)
]
```

The system must determine which detection corresponds to each predicted track.

This is called **data association**.

---

# **Why Euclidean Distance is Not Enough**

A naive approach would use Euclidean distance:

```
distance = sqrt((x1 - x2)^2 + (y1 - y2)^2)
```

However, this ignores uncertainty.

Example:

|**Case**|**Prediction Uncertainty**|**Detection Offset**|**Interpretation**|
|---|---|---|---|
|Stable track|small|5 px|suspicious|
|Uncertain track|large|5 px|acceptable|

Euclidean distance treats both cases equally, which leads to incorrect associations.

---

# **Mahalanobis Distance**

Mahalanobis distance solves this by normalizing distance using the predicted uncertainty.

Formula:

```
d² = (z - ẑ)ᵀ S⁻¹ (z - ẑ)
```

Where:

- z = detection measurement
- ẑ = predicted measurement
- S = innovation covariance

The innovation covariance is:

```
S = H P Hᵀ + R
```

Where:

- P = predicted covariance
- H = measurement model
- R = measurement noise

Mahalanobis distance essentially measures:

> “How many standard deviations away a detection is from the prediction.”

---

# **Geometric Interpretation**

Instead of a circular distance threshold, the prediction produces an **uncertainty ellipse**.

```
      predicted position
             o

        uncertainty ellipse
        _____________
       /             \\
      |               |
       \\_____________/
```

Mahalanobis distance measures how far the detection lies within this probability ellipse.

---

# **Track Association Process**

## **1. Predict Track Positions**

The Kalman filter predicts where each plant should appear.

Example:

```
Track 1 prediction → (100, 450)
Track 2 prediction → (510, 440)
```

---

## **2. Compute Mahalanobis Distance Matrix**

Distances are computed between each track and detection.

Example:

```
                detection1 detection2 detection3
track1              0.8        14.2        0.5
track2             12.4         0.9       11.8
```

---

## **3. Gating**

Matches that exceed a threshold are rejected.

Example threshold:

```
d² < 9
```

This roughly corresponds to a **3-sigma confidence region**.

---

## **4. Assignment**

Remaining matches are assigned using an optimization method such as:

- Hungarian algorithm
- Greedy matching

Example result:

```
track1 → detection3
track2 → detection2
```

---

# **Benefits for Plant Tracking**

This method improves robustness in several situations.

### **Close Plants**

Mahalanobis distance helps separate nearby plants using uncertainty.

### **Detection Noise**

Jitter in bounding boxes is handled naturally.

### **Camera Motion**

Predicted motion helps maintain track continuity.

### **Missing Detections**

Tracks can persist even if a detection is temporarily lost.

---

# **Typical Implementation Pattern**

Conceptually the distance calculation looks like:

```
y = detection - H * x_pred

S = H * P_pred * Hᵀ + R

d² = yᵀ * S⁻¹ * y
```

Then:

```
if d² < threshold:
    valid_match
```

---

# **Key Intuition**

Mahalanobis distance measures:

> distance in units of expected uncertainty.

Examples:

|**Error**|**Uncertainty**|**Result**|
|---|---|---|
|3 px|very small|large Mahalanobis distance|
|3 px|large|small Mahalanobis distance|

This makes the tracker behave probabilistically rather than using fixed thresholds.

---

# **Useful References**

### **Mahalanobis Distance**

[https://en.wikipedia.org/wiki/Mahalanobis_distance](https://en.wikipedia.org/wiki/Mahalanobis_distance)

### **Kalman Filter**

[https://en.wikipedia.org/wiki/Kalman_filter](https://en.wikipedia.org/wiki/Kalman_filter)

### **Stone Soup Tracking Library (excellent tutorials)**

[https://stonesoup.readthedocs.io](https://stonesoup.readthedocs.io)

### **Multi-object tracking overview**

[https://arxiv.org/abs/1602.00763](https://arxiv.org/abs/1602.00763)

---

If you’d like, I can also make a **second Notion section explaining common debugging techniques for Mahalanobis gating in vision trackers**, which is extremely useful for systems like your **plant row tracking pipeline**.