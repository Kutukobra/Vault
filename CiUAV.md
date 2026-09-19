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
- Multi-task joint 3D localization model to adapt limited training data.
- Sensor-in-Sample ([[SiS]]) that optimizes sensor quantity and datasets size. Allows accuracy despite limitations.
### Conclusion
- [[AGC]] greatly reduces [[CSI]] noise.
- [[SiS]] optimizes sensor configurations.
- Localization error of 0.2629 meters.

### Related Works
- [[WiFi Sensing|WiFi-Based Indoor Positioning]]
- [[CSI Based Passive Sniffing]]
- [[MTL|Multi-Task Learning]]