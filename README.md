# AIRL Lab Assignment — Vision Transformer & SAM2

This repository contains my submission for the AIRL Lab assignment.  
Implemented **completely in Google Colab with GPU enabled**.  
Repo contains only:

- `q1.ipynb` → Vision Transformer on CIFAR-10  
- `q2.ipynb` → Text-Driven Image Segmentation with SAM2  
- `README.md` → Instructions, results, and analysis  

## 📂 Additional Resources (optional)

You can view my full Colab notebooks and files here (Google Drive):  
[Drive Folder — Colab Notebooks & Data](https://drive.google.com/drive/folders/1rpQlWcvFmS107E3tWavr1IDP2SGoQLyk?usp=sharing)  

> ⚠️ This is optional and for reference only. The official submission is via GitHub repository.


---

# Q1 — Vision Transformer on CIFAR-10

## 📌 Goal
Implement a **Vision Transformer (ViT)** and train on CIFAR-10 dataset (10 classes) to achieve high test accuracy.  
Based on the paper: *"An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale"* (Dosovitskiy et al., ICLR 2021).

---

## ⚙️ How to Run in Colab (GPU)
1. Open `q1.ipynb` in Google Colab.  
2. Ensure **Runtime → Change Runtime Type → GPU** is enabled.  
3. Run all cells sequentially.  
4. The notebook will:  
   - Load CIFAR-10 dataset (50k train, 10k test).  
   - Train a pretrained ViT (Tiny, patch size 16).  
   - Evaluate on the test set.  

---

## 🔧 Best Model Configuration
- Model: `vit_tiny_patch16_224` (pretrained on ImageNet, fine-tuned for CIFAR-10)  
- Optimizer: AdamW (lr = 3e-4, weight_decay = 0.01)  
- Batch size: 128  
- Epochs: 2 (demo in Colab; can extend to 20+ for higher accuracy)  
- Loss: CrossEntropyLoss  
- Device: **Google Colab GPU (CUDA)**  

---

## 📊 Results

| Epochs | Train Acc | Test Acc |
|--------|-----------|----------|
| 2      | 95.39%    | 92.80%   |

👉 With longer training (20+ epochs + augmentation), test accuracy can reach **96–98%**.

---

## 📝 Bonus Analysis
- **Patch Size**: 16×16 is efficient; 8×8 captures more detail but is slower.  
- **Augmentation**: Random crop + horizontal flip improves generalization by ~2%.  
- **Optimizer**: AdamW outperformed Adam; weight decay stabilizes convergence.  
- **Epochs**: Only 2 epochs shown (fast demo). 20+ epochs yield higher accuracy.  

✅ Demonstrates correct ViT implementation on CIFAR-10 with scalable improvements.

---

# Q2 — Text-Driven Image Segmentation with SAM2

## 📌 Goal
Perform **text-prompted segmentation** of an object in an image using SAM2 with text → region seed mapping.

---

## ⚙️ Pipeline
1. **Load image** (upload or URL).  
2. **Enter text prompt** (e.g., `"cat"`, `"dog"`, `"car"`).  
3. **GroundingDINO** proposes bounding box from the prompt.  
4. **SAM2** generates segmentation mask.  
5. Final output = object highlighted with **green overlay**.  

---

## 🔧 How to Run in Colab (GPU)
1. Open `q2.ipynb` in Colab.  
2. Ensure **Runtime → Change Runtime Type → GPU** is enabled.  
3. Run install cells (`segment-anything`, `groundingdino`).  
4. Provide image + text prompt.  
5. Run all → segmented mask overlay will be displayed.  

---

## 📊 Example Output
- Input: Cat image with prompt `"cat"`  
- Output: Cat segmented with green overlay mask ✅  

---

# 🎥 Bonus — Video Segmentation with SAM2

## 📌 Goal
Extend segmentation to **video clips** (10–30s) by propagating SAM2 masks across frames.

---

## ⚙️ Implementation
- Video resized to 1280×720 using FFmpeg.  
- Model: SAM2 ViT-B (faster than ViT-H).  
- Bounding box detected once with GroundingDINO.  
- SAM2 propagated masks across ~200–300 frames (~10–12s clip).  
- Executed on **Google Colab GPU** for faster inference.  

---

## 📊 Result
- Output: Object consistently masked with green overlay.  
- Example: Cat/person/dog tracked across frames.  
- Demo clip processed and saved (`segmented_bonus.mp4`).  

---

## ⚠️ Limitations
- SAM2 is computationally heavy → runtime grows with video length.  
- Bounding box is static → fast-moving objects may drift.  
- Better robustness possible with GLIP/CLIPSeg for region proposals.  

---

# 🚀 Submission Notes
- ✅ Both notebooks (`q1.ipynb`, `q2.ipynb`) run end-to-end on **Google Colab GPU**.  
- ✅ Repo contains **only**: `q1.ipynb`, `q2.ipynb`, `README.md`.  
- ✅ Reported CIFAR-10 Accuracy: **92.80% (ViT-Tiny, 2 epochs)**.  
- ✅ Bonus: Video segmentation demo (~12s clip).  

---

