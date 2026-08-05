# GAN Coursework — Synthetic & Real-World Data Generation

**Main Notebook:** `Final_Code_GAN_Padhu.ipynb`

This project explores Generative Adversarial Networks across synthetic, image, network-traffic and sketch data. The work starts with a GAN built from scratch and then moves into three practical GAN applications.

---

## Experiments

| Part    | Experiment                | Dataset                            | Implementation                |
| ------- | ------------------------- | ---------------------------------- | ----------------------------- |
| **1**   | 2D distribution learning  | Sine wave + noisy parametric curve | PyTorch MLP GAN               |
| **2.1** | Retinal image generation  | OCTMNIST                           | TensorFlow/Keras DCGAN & cGAN |
| **2.2** | Synthetic network traffic | CICIDS 2017                        | TensorFlow/Keras Dense GAN    |
| **2.3** | Sketch generation         | QuickDraw                          | PyTorch DCGAN                 |

Part 1 also investigates architectural changes by comparing a **2-layer ReLU generator** with a deeper **4-layer ELU generator** on the same target distribution.

For QuickDraw, the main birthday-cake experiment is extended to **cat** and **house** sketches. The CICIDS experiment is similarly extended from Wednesday traffic to the complete set of daily files.

---

## Evaluation

Different evaluation methods are used depending on the data:

* **Images:** generated sample grids, training curves and FID
* **Network traffic:** PCA/t-SNE visualisation and distribution moment gaps
* **2D experiments:** real/generated distribution plots and adversarial loss behaviour

### Main Results

| Experiment                                |              Result |
| ----------------------------------------- | ------------------: |
| Sine GAN — discriminator / generator loss |   ≈ **1.38 / 0.70** |
| OCTMNIST — FID ↓                          |           **39.23** |
| CICIDS Wednesday — mean / std gap ↓       | **0.1576 / 0.2067** |
| CICIDS All Days — mean / std gap ↓        | **0.1300 / 0.1483** |
| QuickDraw House — FID ↓                   |           **26.44** |
| QuickDraw Cake — FID ↓                    |           **34.29** |
| QuickDraw Cat — FID ↓                     |           **38.79** |

---

## Setup

```bash
python -m venv venv
```

Activate the environment:

```bash
# Linux / macOS
source venv/bin/activate

# Windows
venv\Scripts\activate
```

Install the required packages:

```bash
pip install -r requirements.txt
```

Then open `Final_Code_GAN_Padhu.ipynb` and execute the notebook from top to bottom.

The initial setup cell can also install missing dependencies automatically.

---

## Data & Reproducibility

**OCTMNIST** is retrieved through `medmnist`, **CICIDS 2017** through `kagglehub`, and **QuickDraw** sketches are downloaded from Google Cloud Storage.

For CICIDS, the notebook automatically identifies and combines the eight daily CSV files for the full-dataset extension.

Experiments use fixed seeds:

* PyTorch / NumPy: `2025`
* TensorFlow: `2026`
* Image resolution: `32 × 32`

Figures and other runtime outputs are written to the automatically created `results/` directory.

---

### CICIDS Label Clarification

Although the coursework brief refers to DDoS traffic, the Wednesday CICIDS 2017 data contains **DoS attacks** such as Hulk, GoldenEye, slowloris and Slowhttptest. Therefore, the Wednesday experiment is treated as **BENIGN vs DoS**.

DDoS samples occur in the Friday data and are incorporated when the analysis is extended to all available days.

---

The notebook contains the complete modelling workflow, training process, generated samples, visualisations and quantitative evaluation used for the coursework.
