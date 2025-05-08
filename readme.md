# MESA: Matching Everything by Segmenting Anything

This repository reproduces and evaluates the core contributions of the CVPR 2024 paper:  
**"MESA: Matching Everything by Segmenting Anything"** by Zhang & Zhao.

## 📌 Overview

MESA proposes a novel two-stage framework for pixel-level image matching by:
- Segmenting images using the **Segment Anything Model (SAM)**.
- Constructing a **Multi-Relational Graph (MRG)** over the segmented regions.
- Applying **Area Markov Random Fields (AMRF)** and **Graph Cut** for robust region-level matching.
- Learning deep similarity metrics using a **Siamese Network**.

This project re-implements the pipeline using a subset of the **MegaDepth** dataset, verifying the paper's functional correctness and qualitative performance.

---

## 🔧 Pipeline Components

1. **Segmentation using SAM**  
   Semantic regions extracted using Meta AI’s SAM model.

2. **Multi-Relational Graph (MRG)**  
   Graph built with inclusion and adjacency edges using IoU and depth similarity.

3. **Area Markov Random Field (AMRF)**  
   Probabilistic model over MRG with spatial and contextual smoothness.

4. **Graph Cut Optimization**  
   Label inference via Graph Cut for region consistency.

5. **Siamese Network**  
   Learns embeddings for region similarity scoring using contrastive loss.

6. **Area-to-Point Matching (A2PM)**  
   Two versions:
   - Without MESA: SIFT + Brute Force.
   - With MESA: Region-aware ORB filtering + Graph reasoning.

---

## 📂 Dataset

- **MegaDepth Subset**  
  - RGB resolution: 1600×1200  
  - Aligned depth maps in HDF5 format  
  - [MegaDepth Kaggle Link](https://www.kaggle.com/datasets/kashiwaba/megadepth-v1-p2)

---

## ⚙️ Preprocessing

- Convert RGB using OpenCV
- Extract depth from `.h5` using `h5py`
- Siamese pairs loaded via a `pairs.txt` file
- Resize to 400×296, grayscale conversion, normalization

---

## 🧪 Training Details

| Parameter              | Value        |
|------------------------|--------------|
| Batch Size             | 8            |
| Learning Rate          | 0.001        |
| Epochs                 | 30           |
| Embedding Dim          | 128          |
| Dropout                | 0.5          |
| Contrastive Loss Margin| 1.0          |

---

## 📊 Evaluation Metrics

- **AMP@τ**: Area Matching Precision @ IoU threshold  
- **AreaNum**: Average number of segmented regions  
- **ROC-AUC**: Siamese verification performance

---

## 🖥️ Environment

- **Platform**: Kaggle GPU Notebooks  
- **GPU**: Tesla P100 (16 GB VRAM)  
- **Python**: 3.11  
- **Libraries**: PyTorch, torchvision, OpenCV, NetworkX, h5py

---

## 📷 Results

- Successful replication of MESA pipeline
- Visual outputs include SAM masks, MRG graphs, region matches, and Siamese heatmaps
- Graph-based matching showed qualitative improvement over naive keypoint methods

---

## 🙏 Acknowledgements

- Original paper: Zhang & Zhao, CVPR 2024  
- Segment Anything Model (Meta AI)  
- MegaDepth Dataset  
- Guided by Dr. Rachit Chhaya

---

## 📚 References

1. Zhang, Y., & Zhao, X. (2024). MESA: Matching Everything by Segmenting Anything. *CVPR 2024*.

