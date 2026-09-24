- Category: Prototype
- Link: https://arxiv.org/pdf/2505.21216v1
##  Contributions
- [[ESP-CSI]]
- Localization
## Summary
### Abstract
- With ESP32 IoT [[ESP-CSI|CSI]], Automatic Gain Control ([[AGC]]), and multi-task 3D localization model.
- Utilizes Sensor-in-Sample ([[SiS]]) to enhance robustness. 
- Cost-effective and scalable solution.
- LMSE = 0.2629 meters (3D space)
### Introduction
- GPS denied environment is crucial for UAVs' full potential.
- Autonomous inspection, RT surveillance, etc. that requires cm level accuracy.
- Significant challenge. Many sensors are developed to help with indoor positioning.
- Other methods:
	- Ultra-Wide Band: Accurate but complexity and deployment challenges.
	- Optical (CV): Accurate but expensive and LoS.
	- Bluetooth: Cost-effective but lacks accuracy.
- [[CSI]] as promising solution for accuracy, cost,  and robustness.
- Most researches are 2D [[CSI]] localization, not 3D.
- Gap: no 3D localization for UAV indoor applications.
- CSI uses Amplitude and Phase which are highly affected by environmental factors.
- Real uses may result in incomplete sensor data or limited samples, challenge to system performance.
- CiUAV: low-cost with ESP32-S3 without additional onboard equipment.
- Dynamic [[AGC]] to mitigate CSI signal distortions. Outlier processing method to optimize representation.
- [[MTL|Multi-task]] joint 3D localization model to adapt limited training data.
- Sensor-in-Sample ([[SiS]]) that optimizes sensor quantity and datasets size. Allows accuracy despite limitations.
### Related Works
- ####  [[WiFi Positioning|WiFi-Based Indoor Positioning]]
- ####  [[CSI Based Passive Sniffing]]
- ####  [[MTL|Multi-Task Learning]]

### Methodology
![[Pasted image 20260921225335.png|639]]
#### 1. Data Acquisition
- ICMP echo request from sensors, UAV replies with CSI information.
- Non-intrusive approach.
- Multiple CSI sensors, collect CSI data then transfer to host via UDP.
- UAV uses ARUCO and ToF for position.
- Position data is used as label.
- PID controller used to target data point.
- CSI data collected.
#### 2. Dynamic [[AGC]] compensation
- AGC automatically adjusts signal gain for stability.
- AGC causes distortion, dynamic AGC adjusts.
- ESP32-S3 allows real-time AGC.
#### 3. Model training
- SiS: Multi-task 3D Localization model
- Optimizes sensor configurations and training data usage.
- Input _X_: CSI Amplitude only for every sensor every subcarrier.
- Labels _Y_: 3D coordinates.
- Feature extractor extracts features _H_ from input data _X_. Meaningful patterns and structural information.
- _H_ mapped to _Y'_ predicted positions.
- Loss function reduces training sample while maximizing position accuracy.
##### Loss
- To minimize number of sensors, sparsity regularization term.
- Regularization term penalizes sensor weight to reduce redundant deployment. 
- Sample weight vector reguralization to prioritize high-value samples.
- Total Loss = Lprediction + Lsensor + (C)Lsample where C is the regularization coefficient.
- Total loss balances positioning, accuracy, sensor sparsity.
#### 4. 3D localization
- UAV uses onboard camera to detect ARUCO markers.
- ToF sensor to measure altitude.
- CSI data and 3D coordinate transmitted via wireless transmission.
### Experiments
#### Setup
- Three CSI sensors on 2.5 m ceiling. Within 5 m x 5 m room.
- Wireless router to establish area network communication link.
- Three CSI sensors connected to router. One-touch network configuration.
- Indoor UAV connected through WiFi to the router.
- Host computer used as data storage and computation. Same router.
- UDP 2.4 GHz in the same lan.
- Controls via Tello API.
#### Dataset
- CSI sensor 50 Hz sampling rate.
- 121 grid points.
- Height 0.6 - 2 m.
- At each point and height, 500 frames.
- 3 time periods.
- **77,000** samples **33,000** test set.
#### Input CSI data
- N=10,000 samples.
- S=3 sensors.
- f=50 subcarriers.
- 
### Conclusion
- [[AGC]] greatly reduces [[CSI]] noise.
- [[SiS]] optimizes sensor configurations.
- Localization error of 0.2629 meters.
### References
- 