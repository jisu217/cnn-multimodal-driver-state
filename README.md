# A study on driver state recognition using CNN-based multimodal multi-input learning

> A lightweight, on-device-ready driver state recognition system using facial images, body posture images, and sound spectrograms as triple-input multimodal data.

--- 

## 목차 (Table of Contents)
1. [Paper](#1.Paper)
2. [모델 아키텍처 (Model Architecture)](#2-모델-아키텍처)
3. [데이터셋 (Dataset)](#3-데이터셋)
4. [주요 결과 (Results)](#4-주요-결과)
5. [팀원 및 역할 (Team & Roles)](#5-팀원-및-역할)
6. [학술 발표 (Publication)](#6-학술-발표)

--- 

## 1. Paper

**"A study on driver state recognition using CNN-based multimodal multi-input learning"**  
Sooah Shin, Jisu Kang, Sooah Kim, Hwanseo Yeo, Dongyeon Lee, Jeongjyun Lee, Gijun Han, **Jinho Han***  
*Korean Journal of Artificial Intelligence*, 2025  
📎 DOI: [10.24225/kjai.2022.9.1.1](http://dx.doi.org/10.24225/kjai.2022.9.1.1)

---

## 2. Overview

Accurately detecting a driver's state is critical for road safety. This project proposes a **multimodal CNN** that takes **three simultaneous inputs** — driver face image, driver posture image, and sound spectrogram — to classify six driver states with **99.9% accuracy**.

Key design goals:
- ✅ Simple CNN structure suitable for **on-device AI** (e.g., mobile phones)
- ✅ Uses only a **camera + microphone** — no specialized sensors required
- ✅ Outperforms single/dual-input baselines and competes with ResNet50 & Xception

---

## 3. Classification Labels

| Label | State | Visual Cue | Audio Cue |
|-------|-------|-----------|-----------|
| `c0` | Normal | Eyes forward | Quiet ambient sound |
| `c1` | Faint | Head dropped on wheel | Cracking sound |
| `c2` | Drowsy | Eyes closed / yawning | Yawning sound |
| `c3` | Surprise | Eyes/mouth wide open | Horn sound |
| `c4` | Anger | Looks sideways, agitated | Horn + angry voice |
| `c5` | Anxiety | Tense expression | Light horn + exclamation |

---

## 4. Model Architecture

The proposed **Multi-Input CNN** is based on a modified AlexNet structure:

```
Input 1 (Face)    Input 2 (Posture)    Input 3 (Sound Spectrogram)
     │                   │                          │
[Conv1 + Pool]     [Conv1 + Pool]           [Conv1 + Pool]
[Conv2 + Pool]     [Conv2 + Pool]           [Conv2 + Pool]
     └─────────────────Concatenate──────────────────┘
                         │
                    [Conv3] → [Conv4] → [Conv5] → [Pool]
                         │
                 [FC 4096] → [FC 4096] → [FC 6]
                         │
                      Softmax
                   (6 classes output)
```

**Input size:** 227×227×3 per image  
**Total layers:** 8 (2 conv per input branch → concat → 3 conv → 3 FC)

---

## 5. Experimental Results

### Single Input vs. Dual Input vs. Triple Input

| Model | Input | Accuracy |
|-------|-------|----------|
| ResNet50 | Driver face | 81.0% |
| ResNet50 | Driver state | 85.7% |
| Xception | Driver face | 87.8% |
| Xception | Driver state | 76.8% |
| Our CNN | Driver face | 80.7% |
| Our CNN | Driver state | 68.6% |
| Our CNN | Dual (face + state) | 75.8% |
| **Our CNN** | **Triple (face + state + sound)** | **99.9%** |

> 💡 Adding sound spectrogram data as the third modality resolved the overfitting observed in dual-input training and boosted accuracy to **99.9%**.

---

## 6. Dataset

| Split | Samples | Details |
|-------|---------|---------|
| Total | 18,900 | 6 classes × 3 inputs × 1,050 samples |
| Train | 12,600 | 6 × 3 × 700 |
| Test | 6,300 | 6 × 3 × 350 |

- **Driver face images** — facial expression crops
- **Driver state images** — upper body posture images
- **Sound spectrograms** — ~2-second audio clips converted using Adobe Audition

---

## 7. Training Configuration

| Parameter | Value |
|-----------|-------|
| Learning rate | 0.001 |
| Epochs | 200 |
| Number of classes | 6 |
| Image size | 227 × 227 × 3 |

---

## 8. Comparison with Prior Work

| Authors | Classes | Data | Multimodal | Accuracy |
|---------|---------|------|-----------|----------|
| **Ours** | **6** | **Image + Sound** | **✅** | **99.9%** |
| Kim et al. (2024) | 2 | Face image | ❌ | 99.84% |
| Das et al. (2024) | 2 | Image + IoT | ✅ | 98.8% |
| Madni et al. (2024) | 2 | Eye movement | ❌ | 99.0% |
| Amin et al. (2023) | 3 | Image + ECG/HR | ✅ | 96.6% |
| Qin et al. (2022) | 10 | Image (HOG) | ❌ | 99.87% |

---

## 9. Future Work

- Integration of non-contact biosignals (EEG, ECG, EOG) as additional modalities
- Deployment and optimization for real on-device AI environments
- Extension to more diverse and real-world driving scenarios

---

## 10. Citation

```bibtex
@article{shin2025driver,
  title   = {A study on driver state recognition using CNN-based multimodal multi-input learning},
  author  = {Shin, Sooah and Kang, Jisu and Kim, Sooah and Yeo, Hwanseo and Lee, Dongyeon and Lee, Jeongjyun and Han, Gijun and Han, Jinho},
  journal = {Korean Journal of Artificial Intelligence},
  year    = {2025},
  doi     = {10.24225/kjai.2022.9.1.1}
}
```

---

## 11. Contact

**Corresponding Author:** Prof. Jinho Han  
Department of Liberal Arts, Korean Bible University, Republic of Korea  
📧 hjinob@bible.ac.kr

---

