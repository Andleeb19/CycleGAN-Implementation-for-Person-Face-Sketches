# CycleGAN-Implementation-for-Person-Face-Sketches
# Face-to-Sketch Translation Using CycleGAN

This repository contains the implementation of a Cycle-Consistent Generative Adversarial Network (CycleGAN) for **bidirectional image-to-image translation** between facial photographs and sketches. The project includes model training, evaluation, and a web-based interface for real-time image conversion using a trained model.

## 🧠 Project Overview

- **Task**: Image-to-image translation using CycleGAN
- **Dataset**: Person Face Sketches
- **Objective**: 
  - Translate a face photo to its sketch.
  - Translate a face sketch to a photorealistic image.
- **UI**: A simple web-based interface using Gradio for real-time conversion.

---

## 🗂️ Dataset
https://www.kaggle.com/datasets/almightyj/person-face-sketches
We used the **Person Face Sketches** dataset containing 679 paired face images and sketches. The dataset is divided as follows:

- **Training**: 70%
- **Validation**: 10%
- **Testing**: 20%

All images were resized to `256x256` and normalized to `[-1, 1]`.

---

## 🏗️ Model Architecture

### Generators (G<sub>A→B</sub>, G<sub>B→A</sub>)
- Encoder: 3 downsampling convolution layers
- Transformer: 6 residual blocks
- Decoder: 2 upsampling transposed convolutions
- Output: Tanh activated output image

### Discriminators (D<sub>A</sub>, D<sub>B</sub>)
- PatchGAN (70×70) architecture
- 4 convolutional layers with LeakyReLU
- Output: Patch-based decision map

---

## 🔧 Training Details

- **Framework**: PyTorch
- **Optimizer**: Adam (β₁ = 0.5, β₂ = 0.999)
- **Learning Rate**: 0.0002 with linear decay after 100 epochs
- **Epochs**: 10
- **Batch Size**: 4
- **Replay Buffer**: Used for training stability
- **Checkpoints**: Model weights saved after every epoch

---

## 📈 Loss Functions

- **Adversarial Loss**
- **Cycle Consistency Loss** (λ<sub>cyc</sub> = 10.0)
- **Identity Loss** (λ<sub>id</sub> = 5.0)

Total Loss:  
L_total = L_GAN + λ_cyc * L_cyc + λ_id * L_id

yaml
Copy
Edit

---

## 🧪 Evaluation

### Metrics
| Direction         | FID ↓ | SSIM ↑ | PSNR ↑ |
|------------------|-------|--------|--------|
| Photo → Sketch    | 68.32 | 0.71   | 19.45  |
| Sketch → Photo    | 72.45 | 0.68   | 18.73  |

### Observations
- Best results on frontal faces with neutral expressions.
- Performance drops on profile views or extreme expressions.

---

## 🌐 Web Interface (Gradio)

We built a simple user interface using [Gradio](https://gradio.app) that allows:

- Uploading photos or sketches
- Using webcam input
- Switching between photo-to-sketch and sketch-to-photo modes
- Real-time image translation and result download

You can run it directly on **Google Colab**.

---

## 🚀 How to Run

### Training (Colab Recommended)
```bash
# Clone repo
git clone https://github.com/yourusername/CycleGAN-Face-Sketch.git
cd CycleGAN-Face-Sketch
