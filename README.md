# Brain Tumor Segmentation with TransUNet

Segmenting brain tumors from MRI scans using deep learning (BraTS 2020 dataset).

## 🚀 Quick Start

**New here? Read this first:** [SIMPLE_GUIDE.md](SIMPLE_GUIDE.md)

It tells you exactly where to put your work - no confusion!

## Dataset

- **BraTS 2020 Training Data**: 369 cases
- **BraTS 2020 Validation Data**: 125 cases
- **Modalities**: T1, T1ce, T2, FLAIR
- **Segmentation Labels**: Necrotic/non-enhancing tumor, peritumoral edema, enhancing tumor

## 📁 Simple Structure

```
notebooks/     ← Do your work here (Data, Model, Training)
docs/          ← Write what you learned (DATA.md, MODELS.md, TRAINING.md)
src/           ← Clean code goes here (when ready)
dataset/       ← Put BraTS data here
results/       ← Save your plots here
```

**That's it!** Start in `notebooks/`, document in `docs/`.

Read [SIMPLE_GUIDE.md](SIMPLE_GUIDE.md) for details.

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

## 📖 Documentation

- **[SIMPLE_GUIDE.md](SIMPLE_GUIDE.md)** ← START HERE! Where to put everything
- **[docs/DATA.md](docs/DATA.md)** - What you learned about the data
- **[docs/MODELS.md](docs/MODELS.md)** - How your models work
- **[docs/TRAINING.md](docs/TRAINING.md)** - Training experiments and results
- **[PROJECT_PLAN.md](PROJECT_PLAN.md)** - Overall project plan

## Getting Started

### Installation

```bash
git clone https://github.com/sumit43336/multimodal-brats-segmentation.git
cd multimodal-brats-segmentation
pip install -r requirements.txt
```

### Your Workflow

1. **Explore Data** → Open `notebooks/Data.ipynb`
2. **Build Model** → Open `notebooks/Model.ipynb`
3. **Train** → Open `notebooks/Training.ipynb`
4. **Document** → Write in `docs/DATA.md`, `docs/MODELS.md`, `docs/TRAINING.md`

That's it!

## License

This project is for research and educational purposes.

## Acknowledgments

- BraTS 2020 Challenge organizers
- MICCAI community
