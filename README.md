# mae-vae-diffusion-rag-from-scratch

Four generative models from scratch, unified in one web application.

---

## The Four Projects

| Part | Topic | What It Does | Dataset |
| :--- | :--- | :--- | :--- |
| **A** | **Masked Autoencoder (MAE)** | Pretrains an asymmetric ViT encoder–decoder on 64×64 satellite tiles with 75% random patch masking (loss on masked patches only), then trains a linear classifier on only 16 labelled images per class (160 total). | [EuroSAT RGB](https://huggingface.co/datasets/blanchon/EuroSAT_RGB) (10 land-cover classes) |
| **B** | **Variational Autoencoder (VAE)** | Learns a 16-D latent space over 28×28 grayscale handwritten Urdu characters using a convolutional encoder–decoder, reparameterisation trick, and negative ELBO (BCE + closed-form KL). Supports reconstruction, random sampling, and latent interpolation. | [UHaT](https://zenodo.org/records/3670611) (40 character classes) |
| **C** | **Diffusion (DDPM)** | Class-conditioned Denoising Diffusion Probabilistic Model (`T = 1000` linear noise schedule, `diffusers.UNet2DModel` from random init) that generates handwritten Urdu characters from pure noise given a character label. | [UHaT](https://zenodo.org/records/3670611) (40 character classes) |
| **D** | **Retrieval-Augmented Generation (RAG)** | Chunks 40.2k PubMed abstracts (≤150 words, 30-word overlap), builds a mean-pooled L2-normalised embedding index (`all-MiniLM-L6-v2`), retrieves top-k abstracts, and generates cited answers with `Qwen/Qwen2.5-1.5B-Instruct`. Evaluates retrieval (`Hit@k`, `Recall@k`, `MRR@10`) and generation (`ROUGE-L`, citation precision, human eval). | [BioASQ mini](https://huggingface.co/datasets/enelpol/rag-mini-bioasq) (707 test questions) |

> **Medical Content Notice (Part D):** Answers are generated from PubMed research abstracts for learning purposes only. *For educational use only. Not medical advice.*

---

## Repository Structure

```text
.
├── starter/             # Given data loaders and visualization helpers 
│   ├── eurosat.py       # EuroSAT RGB loader, few-label indices, patchify/unpatchify
│   ├── uhat.py          # UHaT character loader (28x28 white-on-black)
│   ├── bioasq.py        # BioASQ corpus and question-answer-passages loaders
│   ├── viz.py           # Image grid saving utility
│   └── check_starter.py # Sanity check script for all three datasets
├── part_a_mae/          # Part A: MAE model, pretraining, reconstructions, few-label classifier
├── part_b_vae/          # Part B: VAE model, training, reconstructions, samples, interpolation
├── part_c_diffusion/    # Part C: DDPM noise schedule, training, sampling
├── part_d_rag/          # Part D: chunking, embedding index, search, metrics, generation, eval
├── results/             # Figures, tables, rag_answers.jsonl, human_eval.csv, analysis.md, samples.md
├── app/                 # Unified web front end with 4 tabs (MAE, VAE, Diffusion, RAG)
└── README.md            # Setup, run instructions, correctness checks, and weight links
```

---

## How to Run

### 1. Environment Setup

```bash
pip install torch transformers datasets diffusers rouge-score matplotlib pillow
```

### 2. Datasets

- **EuroSAT** and **BioASQ** download automatically from Hugging Face on first run.
- **UHaT**: Download `data.zip` from [Zenodo](https://zenodo.org/records/3670611) (or [Kaggle](https://www.kaggle.com/datasets/hazrat/uhat-urdu-handwritten-text-dataset)) and unzip it into `starter/data/uhat/`.

### 3. Verify Starter Code (Task 0)

Run from inside `starter/`:

```bash
cd starter
python check_starter.py
```

This prints dataset shapes/counts and saves `starter/results/eurosat_examples.png` and `starter/results/uhat_examples.png`.

### 4. Training, Evaluation & Web App

*(Update the exact commands below as each module is implemented.)*

- **Part A (MAE):** `python -m part_a_mae...`
- **Part B (VAE):** `python -m part_b_vae...`
- **Part C (Diffusion):** `python -m part_c_diffusion...`
- **Part D (RAG):** `python -m part_d_rag...`
- **Web App:** Launch from `app/` once all four models are trained.

---

## Trained Weights

*(Do not commit weights to GitHub. Upload to Hugging Face or Google Drive and link them here.)*

- **Part A (MAE):** TBD
- **Part B (VAE):** TBD
- **Part C (DDPM):** TBD
- **Part D (Chunk Index):** TBD

---

## Correctness Checks & App Screenshots

*(To be populated with outputs from Section 3.6 correctness checks and screenshots of all four app tabs.)*

Four generative models from scratch, unified in one web application (Assignment 04 — Generative AI, Fall 2026).

---

## The Four Projects

| Part | Topic | What It Does | Dataset |
| :--- | :--- | :--- | :--- |
| **A** | **Masked Autoencoder (MAE)** | Pretrains an asymmetric ViT encoder–decoder on 64×64 satellite tiles with 75% random patch masking (loss on masked patches only), then trains a linear classifier on only 16 labelled images per class (160 total). | [EuroSAT RGB](https://huggingface.co/datasets/blanchon/EuroSAT_RGB) (10 land-cover classes) |
| **B** | **Variational Autoencoder (VAE)** | Learns a 16-D latent space over 28×28 grayscale handwritten Urdu characters using a convolutional encoder–decoder, reparameterisation trick, and negative ELBO (BCE + closed-form KL). Supports reconstruction, random sampling, and latent interpolation. | [UHaT](https://zenodo.org/records/3670611) (40 character classes) |
| **C** | **Diffusion (DDPM)** | Class-conditioned Denoising Diffusion Probabilistic Model (`T = 1000` linear noise schedule, `diffusers.UNet2DModel` from random init) that generates handwritten Urdu characters from pure noise given a character label. | [UHaT](https://zenodo.org/records/3670611) (40 character classes) |
| **D** | **Retrieval-Augmented Generation (RAG)** | Chunks 40.2k PubMed abstracts (≤150 words, 30-word overlap), builds a mean-pooled L2-normalised embedding index (`all-MiniLM-L6-v2`), retrieves top-k abstracts, and generates cited answers with `Qwen/Qwen2.5-1.5B-Instruct`. Evaluates retrieval (`Hit@k`, `Recall@k`, `MRR@10`) and generation (`ROUGE-L`, citation precision, human eval). | [BioASQ mini](https://huggingface.co/datasets/enelpol/rag-mini-bioasq) (707 test questions) |

> **Medical Content Notice (Part D):** Answers are generated from PubMed research abstracts for learning purposes only. *For educational use only. Not medical advice.*

---

## Repository Structure

```text
.
├── starter/             # Given data loaders and visualization helpers (unchanged)
│   ├── eurosat.py       # EuroSAT RGB loader, few-label indices, patchify/unpatchify
│   ├── uhat.py          # UHaT character loader (28x28 white-on-black)
│   ├── bioasq.py        # BioASQ corpus and question-answer-passages loaders
│   ├── viz.py           # Image grid saving utility
│   └── check_starter.py # Sanity check script for all three datasets
├── part_a_mae/          # Part A: MAE model, pretraining, reconstructions, few-label classifier
├── part_b_vae/          # Part B: VAE model, training, reconstructions, samples, interpolation
├── part_c_diffusion/    # Part C: DDPM noise schedule, training, sampling
├── part_d_rag/          # Part D: chunking, embedding index, search, metrics, generation, eval
├── results/             # Figures, tables, rag_answers.jsonl, human_eval.csv, analysis.md, samples.md
├── app/                 # Unified web front end with 4 tabs (MAE, VAE, Diffusion, RAG)
└── README.md            # Setup, run instructions, correctness checks, and weight links
```

---

## How to Run

### 1. Environment Setup

```bash
pip install torch transformers datasets diffusers rouge-score matplotlib pillow
```

### 2. Datasets

- **EuroSAT** and **BioASQ** download automatically from Hugging Face on first run.
- **UHaT**: Download `data.zip` from [Zenodo](https://zenodo.org/records/3670611) (or [Kaggle](https://www.kaggle.com/datasets/hazrat/uhat-urdu-handwritten-text-dataset)) and unzip it into `starter/data/uhat/`.

### 3. Verify Starter Code (Task 0)

Run from inside `starter/`:

```bash
cd starter
python check_starter.py
```

This prints dataset shapes/counts and saves `starter/results/eurosat_examples.png` and `starter/results/uhat_examples.png`.

### 4. Training, Evaluation & Web App

*(Update the exact commands below as each module is implemented.)*

- **Part A (MAE):** `python -m part_a_mae...`
- **Part B (VAE):** `python -m part_b_vae...`
- **Part C (Diffusion):** `python -m part_c_diffusion...`
- **Part D (RAG):** `python -m part_d_rag...`
- **Web App:** Launch from `app/` once all four models are trained.

---

## Trained Weights

*(Do not commit weights to GitHub. Upload to Hugging Face or Google Drive and link them here.)*

- **Part A (MAE):** TBD
- **Part B (VAE):** TBD
- **Part C (DDPM):** TBD
- **Part D (Chunk Index):** TBD

---

## Correctness Checks & App Screenshots

*(To be populated with outputs from Section 3.6 correctness checks and screenshots of all four app tabs.)*
