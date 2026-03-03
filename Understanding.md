TransUNet is a state-of-the-art deep learning architecture that combines the strengths of Convolutional Neural Networks (CNNs) and Transformers for medical image segmentation. It was proposed in the paper 

Why To Use Transunet ??
Traditional medical segmentation models like U-Net (based on pure CNNs) have two major limitations:
1.	Limited Receptive Field – CNNs can only capture local features (edges, textures) but struggle to understand long-range dependencies (relationships between distant pixels)
2.	Loss of Global Context – The tumor's complete structure and its relationship with surrounding brain tissues require global understanding
TransUNet solves this by introducing Transformers – the architecture that revolutionized NLP (BERT, GPT) – into medical image segmentation


Architecture:
TransUNet follows a hybrid CNN-Transformer design:

 

 How TransUNet Works
Step 1: CNN Encoding (Local Features)
•	A ResNet-50 CNN extracts hierarchical features from input images
•	Captures low-level details: edges, textures, boundaries
•	Produces feature maps at multiple resolutions
Step 2: Transformer Encoding (Global Context)
•	Feature maps are reshaped into sequences of patches
•	12-layer Vision Transformer (ViT) processes these sequences
•	Models long-range dependencies between different image regions
•	Understands the complete tumor structure and its context
Step 3: CNN Decoding (Segmentation)
•	U-Net style decoder with skip connections
•	Upsamples features back to original resolution
•	Combines local features (from CNN) with global context (from Transformer)
•	Produces final segmentation masks




Use Of TransUnet in this project 

1. Multi-modal Input Handling
TransUNet seamlessly processes 4 MRI modalities (T1, T1ce, T2, FLAIR) as input channels
2. 3 Tumor Region Segmentation
Outputs 3 segmentation masks simultaneously:
•	Whole Tumor (labels 1+2+4)
•	Tumor Core (labels 1+4)
•	Enhancing Tumor (label 4)
3. Built-in Explainability
The Transformer's attention mechanisms provide natural explainability:
•	Visualize which image regions the model focuses on
•	Understand model decisions for clinical validation
4. 2D → 3D Extensibility
•	Start with 2D slices for efficient training
•	Extend to 3D volumes for complete volumetric segmentation


