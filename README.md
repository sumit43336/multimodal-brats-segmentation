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
├── Code/                    # Analysis and model notebooks
├── dataset/                 # BraTS 2020 dataset
│   └── BraiTs2020/
│       ├── BraTS2020_TrainingData/
│       └── BraTS2020_ValidationData/
└── README.md
```

## Requirements

- Python 3.x
- PyTorch
- nibabel
- numpy
- pandas
- matplotlib
- scikit-learn

## Getting Started

1. Clone the repository
2. Download the BraTS 2020 dataset
3. Run the preprocessing notebooks in the `Code/` directory
4. Train the segmentation model

## License

This project is for research and educational purposes.

## Acknowledgments

- BraTS 2020 Challenge organizers
- MICCAI community
