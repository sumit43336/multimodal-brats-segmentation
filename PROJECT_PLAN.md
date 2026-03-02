# Project Plan: Explainable AI for Medical Image Segmentation (2D -> 3D)

## Overview
We will build a publishable, resume-grade project using the BraTS 2020 training+validation dataset (Kaggle mirror) with a focused, reproducible pipeline. The core study compares:
- 2D vs 3D segmentation
- U-Net vs Attention U-Net
- Explainability analysis (Grad-CAM / attention maps)
- Efficiency trade-offs (time, memory, inference speed)

Primary goal: A clean experimental study with strong baselines, ablations, and interpretable results.

## Dataset
- BraTS 2020 training+validation (Kaggle mirror): https://www.kaggle.com/datasets/awsaf49/brats20-dataset-training-validation
- Task: Brain tumor segmentation
- Modalities: T1, T1c, T2, FLAIR

## Models
- 2D U-Net
- 2D Attention U-Net
- 3D U-Net (patch-based)
- 3D Attention U-Net (lightweight variant if needed)

## Evaluation
- Dice score (primary)
- IoU / Jaccard
- Precision / Recall
- Hausdorff (optional)
- Efficiency: train time, GPU memory, inference latency

## Explainability
- Grad-CAM for 2D models
- Attention map visualization for Attention U-Net
- Slice-level explanations aggregated to 3D volume

## Publishable Contributions (Planned)
1. Empirical comparison of 2D vs 3D segmentation under the same training regime.
2. Impact of attention mechanisms on segmentation accuracy and interpretability.
3. Explainability analysis comparing where models focus across modalities.
4. Efficiency trade-off study for practical deployment.

## Roadmap (4 Weeks)

### Week 1: Setup + Data Pipeline
- Download BraTS 2020 Kaggle dataset
- Preprocess volumes into standardized sizes
- Create 2D slice loader + 3D patch loader
- Set train/val/test splits
- Baseline 2D U-Net training

### Week 2: 2D Models + Baselines
- Train 2D U-Net and 2D Attention U-Net
- Log metrics + save checkpoints
- Initial explainability outputs (Grad-CAM)

### Week 3: 3D Models
- Train 3D U-Net and lightweight 3D Attention U-Net
- Compare 2D vs 3D performance
- Measure GPU usage + training speed

### Week 4: Analysis + Paper Draft
- Compile ablation table (2D/3D x attention/no-attention)
- Explainability figures + qualitative analysis
- Write paper draft: intro, related work, method, results
- Finalize resume bullet points

## Deliverables
- Reproducible training pipeline (PyTorch)
- Results table and plots
- Explainability visualizations
- Draft research paper

## Resume Bullet Draft
- Built and evaluated 2D vs 3D U-Net segmentation on BraTS MRI volumes with attention and explainability, achieving strong Dice scores and interpretable outputs.
- Designed an end-to-end medical imaging pipeline with reproducible preprocessing, training, and evaluation across multiple baselines.
- Conducted efficiency and robustness analyses to inform real-world deployment trade-offs.
