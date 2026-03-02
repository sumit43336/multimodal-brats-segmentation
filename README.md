# Multimodal BraTS Segmentation

Brain tumor segmentation using the BraTS 2020 dataset with deep learning approaches.

## Project Overview

This project implements multimodal brain tumor segmentation using MRI scans from the BraTS (Brain Tumor Segmentation) 2020 challenge dataset.

## Dataset

- **BraTS 2020 Training Data**: 369 cases
- **BraTS 2020 Validation Data**: 125 cases
- **Modalities**: T1, T1ce, T2, FLAIR
- **Segmentation Labels**: Necrotic/non-enhancing tumor, peritumoral edema, enhancing tumor

## Project Structure

```
.
├── src/                     # Source code
│   ├── models/             # U-Net, Attention U-Net (2D & 3D)
│   ├── data/               # Data loaders and preprocessing
│   ├── explainability/     # Grad-CAM, attention visualization
│   └── utils/              # Helper functions
├── notebooks/              # Jupyter notebooks for exploration
├── experiments/            # Training configs and logs
│   ├── configs/           # YAML configuration files
│   └── logs/              # Training logs and tensorboard
├── scripts/               # Training and evaluation scripts
├── results/               # Output results
│   ├── figures/          # Visualizations and plots
│   └── tables/           # Performance metrics
├── dataset/              # BraTS 2020 dataset (not tracked)
├── requirements.txt      # Python dependencies
└── README.md
```

## Requirements

- Python 3.8+
- PyTorch 2.0+
- CUDA (for GPU training)
- See `requirements.txt` for full dependencies

## Results

Coming soon: Performance metrics, visualizations, and comparative analysis.

## Contributing

This is a research project. Feel free to open issues or submit pull requests.

## Features

- **2D and 3D Segmentation**: Compare slice-based vs volumetric approaches
- **Attention Mechanisms**: U-Net vs Attention U-Net architectures
- **Explainability**: Grad-CAM and attention map visualizations
- **Efficiency Analysis**: Training time, GPU memory, inference speed metrics
- **Reproducible Pipeline**: Clean code structure with configuration management

## Getting Started

### Installation

```bash
# Clone the repository
git clone https://github.com/sumit43336/multimodal-brats-segmentation.git
cd multimodal-brats-segmentation

# Install dependencies
pip install -r requirements.txt
```

### Dataset Setup

1. Download BraTS 2020 dataset from [Kaggle](https://www.kaggle.com/datasets/awsaf49/brats20-dataset-training-validation)
2. Extract to `dataset/` directory
3. Run preprocessing scripts

### Training

```bash
# Train 2D U-Net
python scripts/train_2d.py --config experiments/configs/unet2d.yaml

# Train 3D U-Net
python scripts/train_3d.py --config experiments/configs/unet3d.yaml
```

### Evaluation

```bash
# Evaluate model
python scripts/evaluate.py --checkpoint path/to/checkpoint.pth
```

## License

This project is for research and educational purposes.

## Acknowledgments

- BraTS 2020 Challenge organizers
- MICCAI community
