# BraTS 2020 Dataset for Brain Tumor Segmentation

## Dataset Overview

The **Brain Tumor Segmentation (BraTS) 2020** challenge dataset is a multi-institutional collection of pre-operative multi-modal MRI scans focused on brain tumors, specifically gliomas.

| **Attribute** | **Value** |
|---------------|-----------|
| **Total Patients** | 369 |
| **High Grade Glioma (HGG)** | 293 patients (79.4%) |
| **Low Grade Glioma (LGG)** | 76 patients (20.6%) |
| **Patients with Survival Data** | 236 patients |
| **Total NIfTI Files** | 1,845 files |
| **Total Dataset Size** | ~28 GB |
| **Image Dimensions** | 240 × 240 × 155 voxels |
| **Voxel Resolution** | 1.0 mm × 1.0 mm × 1.0 mm (isotropic) |

---

## **Download Links**

| Source | Link | Access |
|--------|------|--------|
| **Official CBICA Portal** | [https://www.med.upenn.edu/cbica/brats2020/data.html](https://www.med.upenn.edu/cbica/brats2020/data.html) | Registration Required |
| **Kaggle** | [https://www.kaggle.com/datasets/awsaf49/brats20-dataset-training-validation](https://www.kaggle.com/datasets/awsaf49/brats20-dataset-training-validation) | Free (Kaggle account) |
| **Zenodo** | [https://zenodo.org/records/3718904](https://zenodo.org/records/3718904) | Direct Download |

---

## **Dataset Structure**

After downloading and extracting, the dataset should be organized as follows:

MICCAI_BraTS2020_TrainingData/
├── BraTS20_Training_001/
│ ├── BraTS20_Training_001_flair.nii
│ ├── BraTS20_Training_001_t1.nii
│ ├── BraTS20_Training_001_t1ce.nii
│ ├── BraTS20_Training_001_t2.nii
│ └── BraTS20_Training_001_seg.nii
├── BraTS20_Training_002/
│ └── ...
├── ...
└── BraTS20_Training_369/
└── ...


---

## **MRI Modalities**

For each patient, 4 multimodal MRI scans are provided:

| Modality | File Pattern | Description | Clinical Role |
|----------|--------------|-------------|---------------|
| **T1** | `*_t1.nii` | Native T1-weighted | Anatomical structure |
| **T1ce** | `*_t1ce.nii` | T1-weighted contrast-enhanced | Highlights active tumor |
| **T2** | `*_t2.nii` | T2-weighted | Identifies edema |
| **FLAIR** | `*_flair.nii` | Fluid-attenuated inversion recovery | Best for peritumoral edema |

**Image Properties:**
- **Dimensions:** 240 × 240 × 155 voxels (height × width × depth)
- **Voxel Spacing:** 1.0 mm × 1.0 mm × 1.0 mm
- **Data Type:** float32 (after loading)

---

## **Segmentation Labels (Ground Truth)**

Each patient includes a segmentation mask file (`*_seg.nii`) with the following label encoding:

| Label | Region | Description |
|-------|--------|-------------|
| **0** | Background | Healthy brain tissue, skull, empty space |
| **1** | Necrosis | Necrotic (dead) tumor core |
| **2** | Edema | Peritumoral edema (swelling around tumor) |
| **4** | Enhancing | Active, contrast-enhancing tumor tissue |

> **Note:** Label 3 is not used in BraTS 2020.

---

## **Derived Tumor Regions for Segmentation**

For our segmentation task, we combine the original labels into **3 clinically meaningful regions**:

| Region | Formula | Labels Included | Clinical Significance |
|--------|---------|-----------------|----------------------|
| **Whole Tumor (WT)** | 1 + 2 + 4 | Necrosis + Edema + Enhancing | Complete tumor extent |
| **Tumor Core (TC)** | 1 + 4 | Necrosis + Enhancing | Solid tumor core |
| **Enhancing Tumor (ET)** | 4 | Enhancing only | Active, proliferating tumor |

**Visual Representation:**

┌─────────────────────────────────────┐
│ Whole Tumor (1+2+4) │
│ ┌─────────────────────────────┐ │
│ │ Tumor Core (1+4) │ │
│ │ ┌─────────────────────┐ │ │
│ │ │ Enhancing (4) │ │ │
│ │ └─────────────────────┘ │ │
│ └─────────────────────────────┘ │
└─────────────────────────────────────┘


---

## **Label Distribution Example (Patient 001)**
Patient: BraTS20_Training_001
Total voxels: 8,928,000 (240×240×155)

Label Distribution:
├── Label 0 (Background): 8,716,021 voxels (97.6%)
├── Label 1 (Necrosis): 15,443 voxels (0.17%)
├── Label 2 (Edema): 168,794 voxels (1.89%)
└── Label 4 (Enhancing): 27,742 voxels (0.31%)

Derived Regions:
├── Whole Tumor (1+2+4): 211,979 voxels (2.37%)
├── Tumor Core (1+4): 43,185 voxels (0.48%)
└── Enhancing Tumor (4): 27,742 voxels (0.31%)

## Clinical Data (Survival Information)
Along with imaging data, we have clinical information for 236 patients (out of 369):

Field	                    Description	                       Example
Age	                      Patient age at diagnosis	         60.46 years
Survival_days	Days        survived after diagnosis	         289 days
Extent_of_Resection	      Surgical resection extent	         GTR, STR, or NA

Sample Clinical Data:
Brats20ID,Age,Survival_days,Extent_of_Resection
BraTS20_Training_001,60.463,289,GTR
BraTS20_Training_002,52.263,616,GTR
BraTS20_Training_003,54.301,464,GTR
...

Extent of Resection Codes:

GTR: Gross Total Resection (complete removal)

STR: Subtotal Resection (partial removal)

NA: Not Available

 Metadata Files
The dataset includes two CSV files for patient mapping and clinical data:
1. name_mapping.csv
Maps BraTS 2020 IDs to previous challenge years and TCGA IDs:

Grade,BraTS_2017_subject_ID,BraTS_2018_subject_ID,TCGA_TCIA_subject_ID,BraTS_2019_subject_ID,BraTS_2020_subject_ID
HGG,Brats17_CBICA_AAB_1,Brats18_CBICA_AAB_1,NA,BraTS19_CBICA_AAB_1,BraTS20_Training_001
...

2. survival_info.csv
Contains clinical data for 236 patients:
Brats20ID,Age,Survival_days,Extent_of_Resection
BraTS20_Training_001,60.463,289,GTR
...

Data Verification Results
Check             	              Status                      	Notes
Total Patients	                  ✅ 369 verified	              All folders present
NIfTI Files	                      ✅ 1,845 files               	5 per patient
File Format	                      ✅ .nii (uncompressed)	      Easy to load
Image Dimensions	                ✅ 240×240×155	              Consistent across patients
Voxel Resolution	                ✅ 1mm isotropic	            Standardized
Segmentation Labels	              ✅ 0,1,2,4 present	          Correct encoding
Multi-modal Complete             	✅ All 4 modalities	          No missing files
Clinical Data	                    ⚠️ 236/369 patients	        Partial availability

Usage Example in Python:
import nibabel as nib
import numpy as np
import os

class BraTS2020Dataset:
    """Simple loader for BraTS 2020 dataset"""
    
    def __init__(self, data_root):
        self.data_root = data_root
        self.patients = [d for d in os.listdir(data_root) 
                        if d.startswith('BraTS20_Training_')]
        self.patients.sort()
        print(f"Found {len(self.patients)} patients")
    
    def load_patient(self, patient_id):
        """Load all modalities for a patient"""
        patient_path = os.path.join(self.data_root, patient_id)
        
        modalities = {}
        for mod in ['flair', 't1', 't1ce', 't2', 'seg']:
            file_path = os.path.join(patient_path, f"{patient_id}_{mod}.nii")
            img = nib.load(file_path)
            modalities[mod] = img.get_fdata()
        
        return modalities
    
    def get_tumor_regions(self, seg):
        """Extract the three tumor regions from segmentation"""
        whole_tumor = ((seg == 1) | (seg == 2) | (seg == 4)).astype(np.float32)
        tumor_core = ((seg == 1) | (seg == 4)).astype(np.float32)
        enhancing = (seg == 4).astype(np.float32)
        
        return {
            'whole_tumor': whole_tumor,
            'tumor_core': tumor_core,
            'enhancing': enhancing
        }

# Usage
dataset = BraTS2020Dataset("path/to/MICCAI_BraTS2020_TrainingData")
patient_data = dataset.load_patient("BraTS20_Training_001")
regions = dataset.get_tumor_regions(patient_data['seg'])

print(f"T1 shape: {patient_data['t1'].shape}")
print(f"Whole tumor voxels: {np.sum(regions['whole_tumor'])}")

Dataset Splits (K-Fold)
For reproducible experiments, we provide 5-fold cross-validation splits:
experiments/folds/
├── fold_1_train.csv  (295 patients)
├── fold_1_val.csv    (74 patients)
├── fold_2_train.csv
├── fold_2_val.csv
├── fold_3_train.csv
├── fold_3_val.csv
├── fold_4_train.csv
├── fold_4_val.csv
└── fold_5_train.csv
└── fold_5_val.csv

Split Strategy:

Stratified by tumor grade (HGG/LGG)

Random seed: 42 for reproducibility

80% training, 20% validation per fold

Citation
If you use this dataset in your research, please cite:
@article{menze2015multimodal,
  title={The multimodal brain tumor image segmentation benchmark (BRATS)},
  author={Menze, Bjoern H and Jakab, Andras and Bauer, Stefan and Kalpathy-Cramer, Jayashree and Farahani, Keyvan and Kirby, Justin and Burren, Yuliya and Porz, Nicole and Slotboom, Johannes and Wiest, Roland and others},
  journal={IEEE transactions on medical imaging},
  volume={34},
  number={10},
  pages={1993--2024},
  year={2015},
  publisher={IEEE}
}

@article{bakas2017advancing,
  title={Advancing the cancer genome atlas glioma MRI collections with expert segmentation labels and radiomic features},
  author={Bakas, Spyridon and Akbari, Hamed and Sotiras, Aristeidis and Bilello, Michel and Rozycki, Martin and Kirby, Justin S and Freymann, John B and Farahani, Keyvan and Davatzikos, Christos},
  journal={Scientific data},
  volume={4},
  number={1},
  pages={1--13},
  year={2017},
  publisher={Nature Publishing Group}
}

Important Notes
Data Privacy: All patient data is fully anonymized

File Format: Files are .nii (uncompressed NIfTI), not .nii.gz

Survival Data: Only 236 patients have complete clinical data

Missing Labels: Label 3 is intentionally unused

Preprocessing: Images are already co-registered and skull-stripped

## Related Resources
BraTS 2020 Challenge Website

BraTS 2020 Paper

Medical Segmentation Decathlon

NIfTI File Format Specification

## Summary
Aspect	                 Details
Total Patients	         369
Modalities	             T1, T1ce, T2, FLAIR
Segmentation Labels	     0 (BG), 1 (Necrosis), 2 (Edema), 4 (Enhancing)
Output Regions	         Whole Tumor, Tumor Core, Enhancing Tumor
Image Dimensions	       240×240×155
Voxel Resolution	       1mm³ isotropic
File Format              NIfTI (.nii)
Clinical Data	           236 patients with survival info
