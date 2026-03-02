# Project Structure

## Directory Organization

```
multimodal-brats-segmentation/
│
├── src/                          # Source code modules
│   ├── models/                   # Model architectures
│   │   ├── unet2d.py            # 2D U-Net implementation
│   │   ├── unet3d.py            # 3D U-Net implementation
│   │   ├── attention_unet2d.py  # 2D Attention U-Net
│   │   └── attention_unet3d.py  # 3D Attention U-Net
│   │
│   ├── data/                     # Data handling
│   │   ├── dataset.py           # PyTorch Dataset classes
│   │   ├── transforms.py        # Data augmentation
│   │   └── preprocessing.py     # Preprocessing utilities
│   │
│   ├── explainability/          # Interpretability methods
│   │   ├── gradcam.py          # Grad-CAM implementation
│   │   └── attention_viz.py    # Attention visualization
│   │
│   └── utils/                   # Utility functions
│       ├── metrics.py          # Evaluation metrics (Dice, IoU)
│       ├── losses.py           # Loss functions
│       └── visualization.py    # Plotting utilities
│
├── notebooks/                   # Jupyter notebooks
│   ├── 01_data_exploration.ipynb
│   ├── 02_preprocessing.ipynb
│   ├── 03_model_comparison.ipynb
│   └── 04_explainability.ipynb
│
├── scripts/                     # Executable scripts
│   ├── train_2d.py             # Train 2D models
│   ├── train_3d.py             # Train 3D models
│   ├── evaluate.py             # Model evaluation
│   ├── preprocess.py           # Data preprocessing
│   └── visualize.py            # Generate visualizations
│
├── experiments/                 # Experiment management
│   ├── configs/                # YAML configuration files
│   │   ├── unet2d.yaml
│   │   ├── attention_unet2d.yaml
│   │   ├── unet3d.yaml
│   │   └── attention_unet3d.yaml
│   └── logs/                   # Training logs (tensorboard)
│
├── folds/                      # Cross-validation splits
│   ├── fold_1_train.csv
│   ├── fold_1_val.csv
│   ├── fold_2_train.csv
│   ├── fold_2_val.csv
│   ├── fold_3_train.csv
│   ├── fold_3_val.csv
│   ├── fold_4_train.csv
│   └── fold_4_val.csv
│
├── results/                    # Experimental results
│   ├── figures/               # Plots and visualizations
│   └── tables/                # Performance metrics
│
├── dataset/                    # BraTS 2020 data (not tracked)
│   └── BraiTs2020/
│       ├── BraTS2020_TrainingData/
│       └── BraTS2020_ValidationData/
│
├── .gitignore                 # Git ignore rules
├── requirements.txt           # Python dependencies
├── PROJECT_PLAN.md           # Detailed project roadmap
├── STRUCTURE.md              # This file
└── README.md                 # Project overview
```

## Key Components

### Models (`src/models/`)
- 2D and 3D U-Net architectures
- Attention mechanisms for improved segmentation
- Modular design for easy experimentation

### Data Pipeline (`src/data/`)
- Custom PyTorch Dataset for BraTS data
- 2D slice extraction and 3D patch sampling
- Data augmentation and normalization

### Explainability (`src/explainability/`)
- Grad-CAM for convolutional layers
- Attention weight visualization
- Multi-modal analysis tools

### Experiments (`experiments/`)
- YAML-based configuration management
- Reproducible experiment tracking
- TensorBoard logging integration

### Cross-Validation (`folds/`)
- Pre-computed 4-fold cross-validation splits
- Ensures reproducibility across experiments
- Balanced train/validation distributions

## Workflow

1. **Data Preparation**: Run `scripts/preprocess.py` to prepare BraTS data
2. **Training**: Use `scripts/train_2d.py` or `scripts/train_3d.py` with config files
3. **Evaluation**: Run `scripts/evaluate.py` to compute metrics
4. **Analysis**: Use notebooks for exploration and visualization
5. **Results**: Check `results/` for figures and performance tables

## Notes

- Dataset files are excluded from version control (see `.gitignore`)
- Model checkpoints are saved in `experiments/logs/`
- All experiments use the same fold splits for fair comparison
