# VOCALIS v3.0: Lightweight Neural Adapter for Synthetic-to-Natural Speaker Embedding Adaptation

## 📖 Overview
Zero-shot speech synthesis is widely used, but speaker embeddings extracted from synthetic speech often do not align well with those from natural recordings. This mismatch occurs because pretrained speaker encoders are tuned heavily on natural speech. 

**VOCALIS** is a lightweight, purely embedding-space residual adapter network designed to bridge this synthetic-to-natural domain gap. It learns to map synthetic speaker embeddings toward their natural counterparts without modifying the pretrained encoder or any downstream systems.

### Key Highlights
- **Parameter-efficient:** The adapter is small (~462,000 parameters).
- **Fast Training:** Trains typically in 2-3 minutes on ordinary CPU hardware.
- **High Performance:** Increases cosine similarity between synthetic and natural embeddings from 0.0081 (baseline) to 0.3239.
- **Robust Generalization:** Generalizes to unseen TTS systems (e.g., gTTS), improving cosine similarity from 0.0507 to 0.3165 despite never being trained on it.
- **Evaluation:** Outperforms classical linear adaptation methods like Mean-shift and Deep CORAL.

## 📂 Repository Structure
```text
vocalis_3.0/
├── data/               # Contains the dataset and extracted embeddings
├── models/             # Saved model checkpoints and weights
├── notebooks/          
│   ├── original/       # Exploratory and initial notebooks (VOCALIS.ipynb)
│   └── updated/        # Final finalized pipeline (vocalis_v3.ipynb)
├── paper/              # The VOCALIS research paper and supplementary documents
├── piper/              # Piper-TTS standalone Windows binaries for synthetic data generation
├── reference/          # Reference papers (Zero-Shot TTS, WavLM, StyleTTS, etc.)
├── requirements.txt    # Python dependencies for the project
└── results/            
    ├── figures/        # Generated plots and evaluation charts
    └── metrics/        # Evaluation results and metrics
```

## ⚙️ Requirements & Installation

**Prerequisites:** Python 3.10+ (Recommended)

1. Clone the repository and navigate to the project root directory.
2. Create and activate a virtual environment (recommended):
   ```bash
   python -m venv venv
   # On Windows
   venv\Scripts\activate
   ```
3. Install the dependencies:
   ```bash
   pip install -r requirements.txt
   ```
   *Note: This project is configured for CPU-only environments.*

**Important Setup Notes:**
- **webrtcvad-wheels**: If using Resemblyzer, make sure `webrtcvad-wheels` is installed before it (this is configured in the requirements).
- **Piper TTS**: The `piper` standalone Windows binary is included in the `piper/` directory. Do not pip-install `piper-tts` due to missing Windows wheels for `piper-phonemize`.

## 🚀 Usage

The entire pipeline—from dataset loading to embedding extraction, training, and evaluation—is contained within the Jupyter Notebooks.

1. Launch Jupyter Notebook or open the project in VS Code.
2. Navigate to `notebooks/updated/vocalis_v3.ipynb`.
3. Run the cells sequentially to:
   - Extract ECAPA-TDNN embeddings for both natural (VCTK) and synthetic (Piper) audio.
   - Train the VOCALIS adapter network on the disjoint training split (28 speakers).
   - Evaluate performance (Cosine Similarity, Euclidean Distance, MSE) on the held-out test split (6 speakers).
   - Test cross-synthesis generalization using gTTS.

## 📊 Results Summary

| Method | Mean Cosine Similarity |
|--------|------------------------|
| No Adaptation (Baseline) | 0.0081 |
| Deep CORAL | 0.1747 |
| Mean-Shift | 0.2051 |
| **VOCALIS (Proposed)** | **0.3239** |

VOCALIS successfully aligns the synthetic speaker embeddings with the natural embeddings much better than existing linear transformations. The improvement holds up across different random seeds and varying sizes of training data.

## 📝 Citation

If you use this work in your research, please refer to the provided paper in the `paper/` directory:

```text
Balaji Ganesh Tammireddy and Puruhutika Rao Tata.
"VOCALIS: A Lightweight Neural Adapter for Synthetic-to-Natural Speaker Embedding Adaptation."
```

## 🤝 Authors
- **Balaji Ganesh Tammireddy** (VIT-AP University)
- **Puruhutika Rao Tata** (VIT-AP University)
