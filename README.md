# Adaptive Bacterial Antibiotic Resistance Prediction Using Meta-Learning

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

This repository contains the implementation and experiments for few-shot prediction of antimicrobial resistance (AMR) genes using meta-learning. The project explores how models can rapidly adapt to previously unseen antibiotic resistance mechanisms using only a handful of labeled sequences.

## Overview

Antimicrobial resistance is a major global health concern, and many AMR gene families are rare or newly emerging. Traditional supervised models fail when only a few examples exist. This project investigates meta-learning frameworks that can generalize from N-way K-shot tasks and adapt quickly to previously unseen AMR classes.

### Key Features

- Unified k-mer Token-CNN encoder compatible with multiple meta-learning paradigms, including metric-based, optimization-based, context-based, and Bayesian methods.
- Enhanced few-shot performance with group-level AMR labels, achieving ~91% accuracy in 3-way 3-shot classification using MetaOptNet-Ridge.
- Strong cross-database transferability, with 95–96% accuracy when adapting from MEGARes to CARD and NDARO in 5-shot settings.
- Deterministic vs. Bayesian comparison, showing that Bayesian MetaOptNet provides superior calibration, reliable uncertainty estimates, and near-zero high-confidence error.
- Comprehensive encoder evaluation, demonstrating that Token-CNN and CNN–BiLSTM offer the best trade-off between accuracy and uncertainty calibration compared to Transformer-based models.

## Repository Structure
```
.
├── dataset/
│   ├── CARD/
│   ├── ndaro/
│   └── megares_fasta_processed.csv
│
├── experiments/
│   ├── experiment1/
│   ├── experiment2/
|   ├── experiment3/
|   └── experiment4/
│
├── meta-learning-models/
│   ├── ablations/
│   └── final/
│
├── results/
│   └── model-checkpoints/
│       ├── bayesian_metaoptnet_checkpoint.pt
│       └── metaoptnet_checkpoint.pt
│
├── LICENSE
└── README.md
```

### Folder Descriptions

#### `dataset/`
Contains datasets, processed FASTA files, k-mer token indices, and harmonized metadata used for experiments.

#### `meta-learning-models/ablations/`
Jupyter notebooks implementing various architectures and meta-learning methods that were archived due to relatively lower performance:
- **Token-CNN encoder**: k-mer-based convolutional encoder
- **CNN–BiLSTM encoder**: Hybrid architecture for sequence modeling
- **Transformer encoder**: Attention-based sequence representation
- **Meta-learning methods**: MetaOptNet, ProtoNet, Bayesian variants, and more

#### `meta-learning-models/final/`
Jupyter notebooks implementing MetaOptNet and Bayesian MetaOptNet algorithms(trained and tested on MegaRes dataset

#### `experiments/`
Jupyter notebooks containing:
- Episodic few-shot training
- Cross-database testing
- Emergence (hold-out class) simulations
- Uncertainty & calibration evaluations
- t-SNE & motif attribution analyses

#### `results/model-checkpoints/`
Pretrained model checkpoints saved during experiments for reproducibility and transfer learning.

## Key Results

| Experiment | Accuracy | Setup |
|------------|----------|-------|
| **MetaOptNet-Ridge on training dataset** | ~91% | 3-way 3-shot tasks |
| **Cross-dataset transfer (testing on unseen datasets)** | 95–96% | 5-shot (MEGARes → CARD/NDARO) |
| **Bayesian variant** | High confidence with zero high-confidence errors | Uncertainty-aware predictions |

### Additional Findings

- Token-CNN embeddings show strong clustering across databases
- K-mer attribution successfully identifies biologically meaningful motifs
- Effective generalization to emerging resistance classes with minimal examples


## Contributors

- **Neha Nair** - [@nehanpnair](https://github.com/nehanpnair)
- **Niharika Saha** - [@Niharika-Saha](https://github.com/Niharika-Saha)
- **Padarthi Neha Sai** - [@pnehasai](https://github.com/pnehasai)
- **Priyanka S** - [@pris25123](https://github.com/pris25123)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
