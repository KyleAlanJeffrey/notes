
### Kalman Filter
A Kalman Filter in a tracker is used to estimate the state of a moving object (like position, velocity, etc.) over time, even when the measurements are noisy or incomplete. It does this by predicting the next state based on a motion model and correcting that prediction using sensor observations.

Key Functions of a Kalman Filter in Tracking:
	1.	Prediction:
	•	Uses the current state and a motion model (e.g., constant velocity) to estimate where the object will be in the next time step.
	•	Also predicts the uncertainty of that estimate.
	2.	Update (Correction):
	•	When a new measurement is received (e.g., from a camera, radar, or sensor), it corrects the prediction by weighing both the prediction and the new measurement.
	•	The result is a better estimate with reduced uncertainty.

Why It’s Useful in Tracking:
	•	Smooths noisy sensor data.
	•	Fills in missing measurements (e.g., when detection is lost).
	•	Estimates hidden variables like velocity or acceleration.
	•	Improves robustness against temporary sensor glitches.

Example:

If you’re tracking a robot with a GPS that updates every second but occasionally drops out or jitters, a Kalman Filter helps keep a smooth and realistic estimate of where the robot actually is and where it’s heading.

