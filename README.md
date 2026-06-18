# **Retinal Segmentation \- UNet \- PyTorch**

This project implements a PyTorch-based U-Net architecture for the semantic segmentation of blood vessels in medical retinal images (retina scans).

## **Project Overview**

Accurate segmentation of retinal blood vessels is crucial for the automated diagnosis of eye diseases. In this project, various configurations of a U-Net model (2-block and 3-block architectures) were implemented and trained from scratch.

Additionally, the project features custom Early Stopping and Model Checkpointing for optimized training, replicating the convenience of Keras callbacks entirely in raw PyTorch.

## **Architectures**

Two variations of the U-Net architecture were evaluated:

* **2-Block U-Net:** A shallower architecture requiring fewer parameters and faster training time.  
* **3-Block U-Net:** A deeper architecture with a higher capacity to extract more complex features.

## **Experiment & Results (Ablation Study)**

To evaluate the impact of data preprocessing steps, the models were trained under two different scenarios:

1. **With ImageNet Normalization** (Standard color correction)  
2. **Without Normalization** (Raw, natural RGB values)

### **Performance Metrics (Test Dataset)**

| Model Architecture | Preprocessing | Dice Score | IoU (Intersection over Union) |
| :---- | :---- | :---- | :---- |
| U-Net (2 Blocks) | Normalized | 0.7041 | 0.5434 |
| U-Net (3 Blocks) | Normalized | 0.7047 | 0.5440 |
| U-Net (2 Blocks) | **Unnormalized (Raw)** | **0.7079** | **0.5478** |
| U-Net (3 Blocks) | Unnormalized (Raw) | 0.7041 | 0.5433 |

### **Observations**

Interestingly, the **unnormalized 2-block model** demonstrated the best overall performance. Standard ImageNet normalization aggressively shifted the image colors into a harsh red spectrum. Because retinal images inherently possess a unique, organic color distribution, retaining the original RGB values actually helped the network effectively segment the fine blood vessels without the need for artificial color correction.

### **Visual Results**

**Normalized**  
<img width="1370" height="1190" alt="normalized" src="https://github.com/user-attachments/assets/5e43b509-cc1f-40ed-8a60-9298f0a016ac" />


**Unnormalized**   
<img width="1370" height="1190" alt="unnormalized" src="https://github.com/user-attachments/assets/a9124ee5-3606-405c-a62e-f900ea026206" />


## **Training Setup**

* **Framework:** PyTorch  
* **Optimizer:** Adam (Learning Rate: 1e-4)  
* **Callbacks:** Custom Early Stopping (Patience: 15\) & Model Checkpoint (Saves best val\_dice)  
* **Metrics:** Dice Score, IoU
