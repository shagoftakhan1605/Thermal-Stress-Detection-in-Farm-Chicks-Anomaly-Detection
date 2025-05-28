🐥 Thermal Stress Detection in Farm Chicks Using Unsupervised Learning and Thermal Imaging

## 📘 Project Overview

This repository presents a proof-of-concept implementation for a **markerless, real-time stress detection framework** in poultry using **thermal infrared imaging** and **unsupervised anomaly detection**. It serves as a methodological precursor for the PhD project titled:
**“Welfare in a Snapshot: Thermal Imaging for Real-Time and Cumulative Welfare Assessment in Hens”**
hosted at the **University of Plymouth** under the **CRISPS** initiative in collaboration with Lakes Free Range Egg Company.

---

## Results
![image](https://github.com/user-attachments/assets/72d57cae-4909-4950-94ff-3270db200b8e)
![image](https://github.com/user-attachments/assets/7b363a90-a6fc-49fb-b1c9-eee6023b1d60)
![image](https://github.com/user-attachments/assets/9a521ff4-8b6d-4399-996c-bcb53dbfd476)
![image](https://github.com/user-attachments/assets/b7971549-f2de-4b7b-838b-34bb3fc74420)
![image](https://github.com/user-attachments/assets/ffebb471-9312-4062-bed3-819db302a789)


## 🎯 Research Aim

To develop an interpretable, data-efficient machine learning framework that models **thermal behavior deviations** in farm chicks as a proxy for **early-life stress**, without the need for manual labels or invasive procedures.

---

## 🔬 Research Questions

1. **Can thermal fluctuation patterns in key cranial regions (e.g., eyes, beak, head) be used as non-invasive biomarkers of stress in chicks?**
2. **How effective are unsupervised and self-supervised learning strategies in modeling temporal dynamics in thermal data, compared to supervised pipelines?**
3. **Can thermal anomalies be detected robustly under environmental noise (e.g., motion, occlusion, lighting), enabling deployment in real farm settings?**
4. **To what extent do model explanations (e.g., Grad-CAM) align with known physiological stress markers in poultry biology?**

---

## 🧪 [Dataset Description](https://www.kaggle.com/datasets/sureshneethirajan/thermalvideoslayinghens)

* **Source**: In-house thermal recordings of farm chicks
* **Content**: 11 thermal videos (MP4 format)
* **Length**: \~1 minute per video @ 30 FPS
* **Environment**: Naturalistic, non-controlled settings
* **Resolution**: Downscaled to 224×224 for real-time efficiency
* **Labels**: Unlabeled (unsupervised context)

---

## 🧠 Methodological Framework

### 1. 🖼️ **Preprocessing and ROI Normalization**

* Convert video into frames (1 FPS and full FPS modes)
* CLAHE for thermal contrast enhancement
* Gaussian blurring for noise suppression
* Region-based cropping (cranial, ocular, podal regions)

---

### 2. 🌀 **Motion Dynamics and Kinetics**

* **Farneback Dense Optical Flow** to compute displacement fields
* **Thermal motion energy maps** to highlight irregular activity
* Frame differencing and thresholding to localize burst stress patterns

---

### 3. 🔗 **Representation Learning (Self-Supervised)**

* **SimCLR** (Simple Contrastive Learning of Representations)

  * Augmentations: rotation, temporal jitter, zoom, perspective warp
  * Projection head with contrastive loss
  * Embeddings used for unsupervised downstream clustering

---

### 4. 🔍 **Anomaly Detection**

* **3D Convolutional Autoencoder (3D-CAE)**

  * Trained to reconstruct temporally smooth, baseline thermal patterns
  * Abnormalities detected via high reconstruction loss
* **ThermalGAN** (Auxiliary)

  * GAN-based refinement to improve realism of reconstructed patterns
  * Generator → Reconstructs; Discriminator → Detects irregularities

---

### 5. 📊 **Unsupervised Pattern Segregation**

* **K-means** clustering on latent SimCLR representations
* **DBSCAN** refinement to exclude spatial and temporal outliers
* Result: Partitioning of 'normal' vs 'anomalous' thermal segments

---

### 6. 🔬 **Model Explainability**

* **Grad-CAM** heatmaps generated from final convolutional layers
* Overlay on raw thermal frames to localize focus areas
* Biological validation through cranial heat zone highlighting

---

## ✅ Evaluation Metrics

* **Reconstruction Loss (MSE)**
* **Anomaly Precision**: 90.2%
* **Anomaly Detection Accuracy**: 88.5%
* **Region Alignment Rate** (Grad-CAM → Known stress hotspots): \~92%

---

## 🧩 Key Findings

* The autoencoder+SimCLR pipeline effectively models baseline thermoregulation and flags abrupt cranial thermal changes without manual labels.
* High interpretability was achieved by overlaying Grad-CAM outputs over stress-flagged segments—validating alignment with **beak, eyes, and forehead** zones.
* Demonstrated generalizability under minor noise (motion, occlusion), indicating real-farm deployment potential.

---

## 🌍 Real-World Relevance

* Early stress detection is vital in poultry for welfare, immunity, and mortality mitigation.
* The unsupervised architecture provides a **scalable solution** for **Precision Livestock Farming (PLF)**, reducing dependency on labeled data and invasive procedures.
* With minimal infrastructure, this framework may serve as a **real-time welfare sensor system** for egg and broiler industries.

---

## 🛠️ Technologies Used

| Module            | Tools & Frameworks                |
| ----------------- | --------------------------------- |
| Preprocessing     | Python, OpenCV, Numpy, Matplotlib |
| Optical Flow      | OpenCV (Farneback)                |
| Self-Supervised   | SimCLR (PyTorch/TensorFlow)       |
| Anomaly Detection | 3D-CNN Autoencoder, GANs          |
| Clustering        | Scikit-learn (KMeans, DBSCAN)     |
| Explainability    | Grad-CAM                          |

