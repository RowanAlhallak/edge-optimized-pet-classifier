# Edge-Optimized Image Classification for Mobile Deployment

## Project Objective
This project engineers a lightweight, mobile-ready multiclass computer vision model designed to classify fine-grained biological traits (37 distinct cat and dog breeds from the Oxford-IIIT Pet Dataset) entirely on-device. The goal is to maximize classification accuracy while minimizing memory footprint, computational overhead, and CPU inference latency for offline edge environments.

**Read the full Technical Whitepaper:** 
[edge-optimized-pet-classifier.pdf](https://github.com/user-attachments/files/34613747/edge-optimized-pet-classifier.pdf)


## Tech Stack
* **Framework:** PyTorch, Torchvision, PyTorch Mobile (TorchScript)
* **Language:** Python
* **Data Visualization:** Matplotlib, Scikit-Learn
* **Environment:** Google Colab (GPU Acceleration for training)

## Methodology & Architecture
* **Model:** MobileNetV2 (Pre-trained on ImageNet).
* **Dataset:** Oxford-IIIT Pet Dataset (37 classes). 
* **Training Pipeline:** Implemented a two-phase transfer learning strategy:
  1. **Phase 1 (Feature Extraction):** Froze base layers and trained the classification head for 5 epochs to stabilize weights.
  2. **Phase 2 (Fine-Tuning):** Unfroze the entire network and trained with a reduced learning rate (1e-4) utilizing a `ReduceLROnPlateau` scheduler.
* **Mobile Optimization:** Serialized and optimized the final model using `optimize_for_mobile` to fuse layers and prepare the `.ptl` file for mobile CPU execution.

## Key Results & Edge Metrics
The two-phase fine-tuning approach successfully achieved an **89% overall test accuracy** across 10,000 images, proving capable of distinguishing biologically similar breeds. 

Crucially, the model is highly optimized for offline smartphone deployment:
* **Mobile Model File Size:** 8.57 MB
* **Total Parameters:** 2,271,269
* **Average CPU Inference Latency:** 32.96 ms per image
* **Throughput:** ~30.3 Frames Per Second (FPS)

### Training & Validation Curves
<img width="1390" height="490" alt="LearningCurves" src="https://github.com/user-attachments/assets/47148919-5bc6-4915-b14e-36f760e9fee9" />


### Class-Specific Confusion Matrix
<img width="939" height="816" alt="ConfusionMatrix" src="https://github.com/user-attachments/assets/6d9e1ee9-46c1-4cd9-98f7-f3ec9e8d664d" />


## How to Run the Code
1. Clone this repository:
   ```bash
   git clone [https://github.com/RowanAlhallak/edge-optimized-pet-classifier.git](https://github.com/RowanAlhallak/edge-optimized-pet-classifier.git)
