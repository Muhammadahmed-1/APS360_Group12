# Satellite-to-Map Image Translation (APS360 Project)

## Overview
This project implements a **conditional Generative Adversarial Network (cGAN)** to translate satellite images into Google Maps–style renderings. The model uses a **U-Net generator** and a **70×70 PatchGAN discriminator**, trained on paired satellite–map datasets. The goal is to automate map generation with high fidelity in road layouts and building structures.

<img width="1277" height="685" alt="image" src="https://github.com/user-attachments/assets/106f8c11-9049-4480-9506-34856e4d2ebb" />

## Data Processing
- Dataset: **Pix2Pix paired dataset (NYC)** + additional manually collected global city data.  
- Preprocessing: resizing, normalization, augmentation (jitter, rotation, blur, flips).  
- Splits: **80/10/10** (train/validation/test).  
---
## Model Architecture
- **Generator**: U-Net (8-layer encoder–decoder with skip connections).  
- **Discriminator**: 70×70 PatchGAN for patch-level realism.  
- **Losses**:  
  - Generator: BCE adversarial loss + L1 loss (λ=100) + perceptual VGG-16 loss.  
  - Discriminator: BCE loss.  
- Training: Adam optimizer, lr=0.0002, batch size=1.  
---
## Hyperparameter Tuning 
<img width="1128" height="746" alt="image" src="https://github.com/user-attachments/assets/c4224814-17d9-4047-b466-18a21e1b7d4a" />

## Results
**Quantitative (Validation Set):**
- L1 Loss: **0.0647**  
- PSNR: **25.68 dB**  
- SSIM: **0.6895**
**Test Set:**  
- L1 Loss: **0.0639**  
- PSNR: **25.86 dB**  
- SSIM: **0.6958**
**Qualitative:**  
<img width="1122" height="619" alt="image" src="https://github.com/user-attachments/assets/4bae1ff4-f913-4037-b6b4-c2a08a6f84bc" />
<img width="1159" height="618" alt="image" src="https://github.com/user-attachments/assets/227529fc-384e-4e42-ac28-4113947e3832" />
- Clear reproduction of road layouts and building boundaries in NYC samples.  
- Struggles with fine details in water regions and in unseen global city data.  

---
