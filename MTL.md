## Introduction
- 
## Notes
- Leverages shared features across related tasks to improve generalization and performance in NLP & Computer Vision.
- Parameter Sharing: tasks share a common feature extraction layer.
- Soft Parameter Sharing: links independent models through task-spesific constraints.
- Mitigates overfitting and improve information utilization.
- Recently has incorporated dynamic mechanisms, adjusting task processing using contextual information to capture inter-task relationships to improve robustness.
## MTL for UAV Localization
- Traditional single-task models focus on position prediction overlooking multi-dimensional factors like signal propagation and noise.
- Intertask competition in MTL can cause bottlenecks, espescially in correlated & complex environments.
- Dynamic MTL framework that co-optimizes multiple tasks and utilizes CSI's multi-dimensional characteristics is essential.  
## References
- [[CiUAV]]