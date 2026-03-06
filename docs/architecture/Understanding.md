# TransUNet: Transformers for Medical Image Segmentation

## Overview

TransUNet is a state-of-the-art deep learning architecture that combines the strengths of **Convolutional Neural Networks (CNNs)** and **Transformers** for medical image segmentation. It bridges the gap between local feature extraction and global context understanding.

---

## Why Use TransUNet?

### Limitations of Traditional U-Net

Traditional medical segmentation models like U-Net (based on pure CNNs) have two major limitations:

1. **Limited Receptive Field**
   - CNNs can only capture local features (edges, textures)
   - Struggle to understand long-range dependencies
   - Cannot model relationships between distant pixels effectively

2. **Loss of Global Context**
   - Tumor's complete structure requires holistic understanding
   - Relationship with surrounding brain tissues needs global awareness
   - Pure CNNs lack the ability to capture these global patterns

### TransUNet Solution

TransUNet solves these problems by introducing **Transformers** – the architecture that revolutionized NLP (BERT, GPT) – into medical image segmentation.

```
Traditional U-Net:  CNN → CNN → CNN (Local features only)
TransUNet:         CNN → Transformer → CNN (Local + Global context)
```

---

## Architecture

TransUNet follows a **hybrid CNN-Transformer design**:

```
┌─────────────────────────────────────────────────────────────┐
│                        TransUNet Architecture                │
└─────────────────────────────────────────────────────────────┘

Input Image (H×W×C)
      ↓
┌─────────────────┐
│  CNN Encoder    │  ← ResNet-50 backbone
│  (Local Features)│  ← Extracts hierarchical features
└────────┬────────┘
         │ Feature Maps
         ↓
┌─────────────────┐
│ Patch Embedding │  ← Reshape to sequence of patches
└────────┬────────┘
         │ Patch Sequence
         ↓
┌─────────────────┐
│  Transformer    │  ← 12-layer Vision Transformer (ViT)
│ (Global Context)│  ← Self-attention mechanism
└────────┬────────┘
         │ Encoded Features
         ↓
┌─────────────────┐
│  CNN Decoder    │  ← U-Net style decoder
│ (Upsampling)    │  ← Skip connections from encoder
└────────┬────────┘
         ↓
Segmentation Mask (H×W×Classes)
```

---

## How TransUNet Works

### Step 1: CNN Encoding (Local Features)

```
Input → Conv Blocks → Feature Maps
        (ResNet-50)    (Multiple scales)
```

- **ResNet-50 CNN** extracts hierarchical features from input images
- Captures low-level details: edges, textures, boundaries
- Produces feature maps at multiple resolutions (1/2, 1/4, 1/8, 1/16)

**Feature Hierarchy:**
```
Level 1: 64 channels  → Basic edges and textures
Level 2: 256 channels → Simple patterns
Level 3: 512 channels → Complex structures
Level 4: 1024 channels → High-level features
```

### Step 2: Transformer Encoding (Global Context)

```
Feature Maps → Patches → Self-Attention → Global Features
   (H×W×C)      (N×D)      (12 layers)      (N×D)
```

- Feature maps are reshaped into **sequences of patches**
- **12-layer Vision Transformer (ViT)** processes these sequences
- Models long-range dependencies between different image regions
- Understands the complete tumor structure and its context

**Self-Attention Mechanism:**
```
For each patch:
  Q (Query)  = What am I looking for?
  K (Key)    = What information do I have?
  V (Value)  = What information should I pass?
  
Attention(Q,K,V) = softmax(QK^T/√d)V
```

### Step 3: CNN Decoding (Segmentation)

```
Encoded Features → Upsample → Skip Connections → Output Mask
   (Transformer)     (×2,×4)    (from encoder)     (H×W×C)
```

- **U-Net style decoder** with skip connections
- Upsamples features back to original resolution
- Combines local features (from CNN) with global context (from Transformer)
- Produces final segmentation masks

**Decoder Architecture:**
```
Layer 1: 512 channels → Upsample ×2 + Skip Connection
Layer 2: 256 channels → Upsample ×2 + Skip Connection
Layer 3: 128 channels → Upsample ×2 + Skip Connection
Layer 4: 64 channels  → Upsample ×2 + Skip Connection
Output:  Classes      → Final segmentation
```

---

## Use of TransUNet in This Project

### 1. Multi-modal Input Handling

TransUNet seamlessly processes **4 MRI modalities** as input channels:

```
Input Shape: (H, W, 4)
├── Channel 0: T1    (anatomical structure)
├── Channel 1: T1ce  (contrast-enhanced)
├── Channel 2: T2    (edema detection)
└── Channel 3: FLAIR (fluid detection)
```

### 2. Multi-class Tumor Segmentation

Outputs **3 segmentation masks** simultaneously:

| Region | Label | Description |
|--------|-------|-------------|
| **Whole Tumor (WT)** | 1+2+4 | Complete tumor region including all sub-regions |
| **Tumor Core (TC)** | 1+4 | Non-enhancing tumor core + enhancing tumor |
| **Enhancing Tumor (ET)** | 4 | Active/enhancing tumor region |

```
Output Shape: (H, W, 3)
├── Mask 0: Whole Tumor (WT)
├── Mask 1: Tumor Core (TC)
└── Mask 2: Enhancing Tumor (ET)
```

### 3. Built-in Explainability

The Transformer's **attention mechanisms** provide natural explainability:

```
Attention Weights Visualization:
┌─────────────┐     ┌─────────────┐
│ Input Slice │ --> │ Attention   │
│   (MRI)     │     │    Map      │
└─────────────┘     └─────────────┘
                           ↓
                    Which regions does
                    the model focus on?
```

**Benefits:**
- Visualize which image regions the model focuses on
- Understand model decisions for clinical validation
- Identify potential biases or failure modes
- Build trust with medical practitioners

### 4. 2D → 3D Extensibility

**Progressive Development Strategy:**

```
Phase 1: 2D TransUNet
├── Train on individual slices
├── Fast iteration and debugging
└── Efficient GPU memory usage

Phase 2: 2.5D TransUNet
├── Use multi-slice input (e.g., 3 consecutive slices)
├── Capture some 3D context
└── Moderate computational cost

Phase 3: 3D TransUNet
├── Full volumetric segmentation
├── Complete spatial context
└── Higher computational requirements
```

**Advantages:**
- Start with 2D slices for efficient training
- Extend to 3D volumes for complete volumetric segmentation
- Flexible architecture for different computational budgets

---

## Key Advantages for BraTS Challenge

### 1. Superior Performance
- Combines local and global feature learning
- Better boundary detection and tumor delineation
- Handles complex tumor morphologies

### 2. Multi-modal Fusion
- Effectively integrates information from 4 MRI sequences
- Learns complementary features across modalities
- Robust to missing modalities (if needed)

### 3. Interpretability
- Attention maps show model reasoning
- Clinically relevant explanations
- Facilitates model debugging and improvement

### 4. Scalability
- Efficient training with 2D slices
- Extensible to 3D for deployment
- Adaptable to different image sizes

---

## Implementation Pipeline

```
┌──────────────────────────────────────────────────────────┐
│                   Training Pipeline                       │
└──────────────────────────────────────────────────────────┘

1. Data Loading
   └── Load 4 modalities (T1, T1ce, T2, FLAIR)
   └── Load ground truth segmentation

2. Preprocessing
   └── Normalize intensities
   └── Extract 2D slices
   └── Data augmentation (rotation, flip, elastic)

3. Model Training
   └── Forward pass through TransUNet
   └── Compute loss (Dice + Cross-Entropy)
   └── Backpropagation and optimization

4. Validation
   └── Compute Dice scores (WT, TC, ET)
   └── Generate attention visualizations
   └── Save best checkpoint

5. Testing
   └── Inference on test set
   └── Post-processing (CRF, morphological ops)
   └── Generate submission files
```

---

## Comparison: U-Net vs TransUNet

| Aspect | U-Net | TransUNet |
|--------|-------|-----------|
| **Architecture** | Pure CNN | Hybrid CNN-Transformer |
| **Receptive Field** | Limited (local) | Global (entire image) |
| **Feature Learning** | Hierarchical convolutions | Convolutions + Self-attention |
| **Context Modeling** | Local neighborhoods | Long-range dependencies |
| **Explainability** | Grad-CAM only | Attention maps + Grad-CAM |
| **Computational Cost** | Lower | Higher (but manageable) |
| **Performance** | Good baseline | State-of-the-art |

---
