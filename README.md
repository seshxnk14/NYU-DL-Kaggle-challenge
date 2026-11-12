# NYU-DL-Kaggle-challenge
# CIFAR-10 Classification with Wide ResNet-28

## Project Overview

This project develops a custom Wide Residual Network for CIFAR-10 image classification under a five-million-trainable-parameter constraint.

Our final model achieved **88.80% accuracy on the Kaggle public leaderboard** using a single residual CNN.

## Final Results

| Metric | Result |
|---|---|
| Architecture | Custom preactivation Wide ResNet-28 |
| Trainable parameters | 4,923,705 |
| Training images | 50,000 labeled |
| Competition test images | 2,000 unlabeled |
| Local validation accuracy | 96.98% |
| Kaggle public leaderboard accuracy | 88.80% |
| Training epochs | 240 |

The local validation result was obtained using a separate model trained on 45,000 images and evaluated on 5,000 held-out images. The Kaggle result was obtained using the final model trained on all 50,000 labeled images.

## Methodology

The final training procedure combines:

- CIFAR-10 AutoAugment
- MixUp and CutMix
- Sharpness-Aware Minimization (SAM)
- Exponential Moving Average (EMA) weights
- SGD with momentum and cosine learning-rate decay
- Horizontal-flip test-time augmentation

## Repository Contents

- `notebooks/` — Final training, validation, and prediction notebook
- `report/` — Project methodology and experimental findings
- `results/` — Final Kaggle submission CSV
- `requirements.txt` — Python dependencies

## Running the Notebook

1. Download the competition dataset from Kaggle.
2. Install the dependencies listed in `requirements.txt`.
3. Open `notebooks/CIFAR10_WRN28_Final.ipynb` in JupyterLab or Google Colab.
4. Configure the dataset and checkpoint paths in the first code cell.
5. Select one of the three execution modes.

### Execution Modes

**`validate`** — Trains on 45,000 images and evaluates on 5,000 held-out images.

**`full`** — Trains the final model from scratch on all 50,000 labeled images.

**`predict`** — Loads an existing full-data checkpoint and generates predictions for the 2,000 competition test images.

The notebook's default prediction configuration requires the saved full-data checkpoint. If the checkpoint is unavailable, use `full` mode to retrain the model.

## Evaluation

The competition test labels are hidden. Therefore, test accuracy cannot be calculated locally. The notebook generates a submission CSV containing `id,label`, which Kaggle evaluates against its hidden labels.

Our best reported public leaderboard accuracy was **88.80%**.

## Reproducibility

The project uses random seed 2026 for the final development experiment. Training configuration and optimizer state are stored in model checkpoints.

GPU availability, software versions, and nondeterministic operations may affect exact reproduction.

## References

See the project report for the experimental comparisons, architectural design decisions, and academic references.
