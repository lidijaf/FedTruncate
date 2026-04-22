# Robust Federated Learning Experiments

## 📝 Overview

This repository contains an experimental framework for studying **robust federated learning (FL)** under adversarial conditions using the Flower framework.

The project is based on and adapted from the original implementation of **loss-based client clustering for robust FL**, and extended with additional algorithms and experiments.

### Implemented Algorithms

- **FedAvg (Mean)**
- **FedCluster** (loss-based client clustering)
- **FedTruncate** (our implementation)
- Additional robust aggregation baselines:
  - Trimmed Mean
  - Median
  - Krum
  - Multi-Krum
  - Bulyan

### Project Goal

The goal of this project is to:
- implement and analyze **robust FL algorithms**
- compare their performance under:
  - clean (no attack) settings
  - adversarial attacks (e.g., label flipping, sign flipping, noise)
- evaluate robustness, convergence, and stability

---

## 🔗 Origin of the Codebase

This repository is adapted from the WAFL25-RobustFL project.

We extend this codebase with:
- new strategies (e.g., **FedTruncate**)
- modified configuration and evaluation setups
- additional experiments

---

## 🗂️ Project Structure

```
.
├── src/                # Core Flower code
│   ├── strategies/     # Server strategies (FedAvg, FedCluster, FedTruncate, etc.)
├── configs/            # YAML configuration files for experiments
├── data/               # Partitioned datasets (generated automatically)
├── outputs/            # Experiment outputs (logs, metrics, checkpoints)
├── pyproject.toml      # Dependencies (Poetry)
└── README.md
```

> `data/` and `outputs/` are generated automatically and should not be version-controlled.

---

## 🚀 Quick Start

### Prerequisites

- Python 3.10+
- Poetry

---

### 1. Install Dependencies

```
poetry install
```

---

### 2. Partition Dataset

Example (CIFAR-10, 10 clients, IID):

```
poetry run partition-dataset CIFAR10 --num_clients=10 --type=homogeneous
```

---

### 3. Select Configuration

```
export config_file_name=config_no_attack
```

---

### 4. Run Simulation

```
poetry run simulation
```

---

## ⚙️ FedTruncate (Our Contribution)

We implemented **FedTruncate**, a robust FL aggregation method based on:

1. Evaluating client updates on a trusted server dataset
2. Rejecting low-quality updates using a threshold
3. Selecting the best K clients
4. Aggregating selected models
5. Applying a rollback mechanism if the update degrades performance

### Key Implementation Detail

We use a **relative threshold**:

f_S(x_i) > f_S(x^t) * (1 + B)

This makes the method stable across training rounds.

---

## 📊 Current Status

- FedTruncate implemented and validated
- Stable configuration identified
- Ongoing experiments:
  - comparison with FedCluster and FedAvg
  - evaluation under adversarial attacks

---

## 📬 Future Work

- Integration of additional algorithms (e.g., FedGreed)
- Extensive evaluation under different attack models
- Hyperparameter sensitivity analysis
