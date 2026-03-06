# Documentation

This directory contains all project documentation organized by topic.

## Structure

```
docs/
├── architecture/          # Model architecture explanations
│   ├── transunet.md      # TransUNet architecture details
│   ├── unet.md           # U-Net baseline
│   └── attention_unet.md # Attention U-Net
│
├── data/                 # Data understanding and analysis
│   ├── brats_dataset.md  # BraTS dataset overview
│   ├── preprocessing.md  # Data preprocessing steps
│   └── augmentation.md   # Data augmentation strategies
│
├── training/             # Training documentation
│   ├── setup.md         # Training setup and configuration
│   ├── hyperparameters.md # Hyperparameter tuning
│   └── best_practices.md  # Training tips and tricks
│
├── evaluation/           # Evaluation and metrics
│   ├── metrics.md       # Dice, IoU, Hausdorff
│   └── visualization.md # Result visualization
│
└── explainability/       # Interpretability methods
    ├── gradcam.md       # Grad-CAM explanation
    └── attention.md     # Attention visualization
```

## Quick Links

- [Understanding BraTS Dataset](data/brats_dataset.md)
- [TransUNet Architecture](architecture/transunet.md)
- [Training Guide](training/setup.md)
- [Evaluation Metrics](evaluation/metrics.md)
