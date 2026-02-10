# Learning Probability Density Function using GAN

---

##  Objective

The objective of this project is to learn the probability density function (PDF) of a transformed NO₂ concentration variable using a **Generative Adversarial Network (GAN)**.  
Instead of assuming a known distribution (like Gaussian), the model learns the distribution directly from data samples.

---

## Dataset

- **Dataset:** India Air Quality Data  
- **Feature used:** NO₂ concentration (x)  
- Source: https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data  

Only the NO₂ column was used for this task.

---

## Methodology

The project was completed in three stages.

---

### Step 1: Data Transformation

Each NO₂ value `x` was transformed into a new variable `z` using:

z = x + a_r * sin(b_r * x)

where:
a_r = 0.05 * (r mod 7)
b_r = 0.3 * ((r mod 5) + 1)


- `r` = roll number  
- `mod` = remainder operator  

This transformation introduces a non-linear sinusoidal variation to the data.

---

### Step 2: GAN-based PDF Learning

A **Generative Adversarial Network (GAN)** was used to learn the distribution of `z`.

A GAN consists of two networks:

#### Generator
- Takes random noise as input  
- Produces fake samples  
- Goal: mimic real z values

#### Discriminator
- Receives real and fake samples  
- Predicts whether input is real or fake  
- Goal: distinguish real from generated samples

Both networks compete during training, allowing the generator to gradually learn the true distribution.

---

### Step 3: Training Process

- Data was normalized before training  
- Mini-batch training was used  
- Binary cross-entropy loss optimized both networks  
- Training continued for multiple epochs

---

### Step 4: PDF Estimation

After training:

- Generator produced many synthetic samples  
- Histogram density estimation was used  
- This histogram approximates the learned PDF

---

## Result Graph

The histogram below compares:

- Real transformed data (z)  
- GAN-generated samples  

The GAN captures the central tendency and range of the data.

<img width="824" height="616" alt="image" src="https://github.com/user-attachments/assets/3e72512a-b09a-4641-b8e0-88f63b8b1935" />

---

## Result Table

| Component | Description |
|--------|------------|
| Transformation | Sinusoidal non-linear mapping |
| Generator | Fully connected neural network |
| Discriminator | Binary classifier network |
| Training Method | Adversarial learning |
| PDF Estimation | Histogram density |

---

## Observations

### Mode Coverage
The GAN learned the main region where data occurs but showed some concentration near the mean.

### Training Stability
Loss values oscillated, which is normal for GAN training.

### Quality of Generated Distribution
Generated samples roughly matched the real data distribution, though minor mode collapse was observed.

---

## Conclusion

- GAN successfully learned the distribution without assuming a known PDF  
- Generated samples approximate the real data distribution  
- Demonstrates data-driven density learning  
- Shows practical application of generative models

---
