# FineFACE: Fair Facial Attribute Classification Leveraging Fine-grained Features

## Overview

Published research highlights the presence of demographic bias in automated facial attribute classification algorithms, particularly impacting women and individuals with darker skin tones. Existing bias mitigation techniques typically require demographic annotations and often obtain a trade-off between fairness and accuracy, i.e., Pareto inefficiency. Facial attributes, whether common ones like gender or others such as "chubby" or "high cheekbones", exhibit high interclass similarity and intraclass variation across demographics leading to unequal accuracy. This necessitates the use of local and subtle cues using fine-grained analysis for differentiation.  This paper proposes a novel approach to fair facial attribute classification by framing it as a fine-grained classification problem. Our approach effectively integrates both low-level local features (like edges and color) and high-level semantic features (like shapes and structures) through cross-layer mutual attention learning. Here, shallow to deep CNN layers function as experts, offering category predictions and attention regions.

## FineFACE network architecture
![image](https://github.com/user-attachments/assets/6b11d3d4-c876-411e-b89d-33bffe5a7545)

This figure illustrates this method by introducing three experts e1, e2, e3, on a 5-stage backbone CNN (e.g., ResNet50). The workflow of each expert and the concatenation of experts are depicted in different colors. Each expert receives feature maps from a specific layer as input and generates a categorical prediction along with an attention region, which is used for data augmentation by other experts. This architecture is trained in multiple steps within each iteration. We start by training the deepest expert (e3), followed by the shallower experts. Finally, in the last step, we train the concatenation of experts to enhance overall performance.

## Requirements

-Python
-PyTorch

## Datasets

1. Download the FairFace, UTKFace, LFWA+ and CelebA datasets and organize the structure as follows:

- dataset folder
  - train
    - class_001
      - 1.jpg
      - 2.jpg
      - ...
    - class_002
      - 1.jpg
      - 2.jpg
      - ...
  - test
    - class_001
      - 1.jpg
      - 2.jpg
      - ...
    - class_002
      - 1.jpg
      - 2.jpg
      - ...
2. Modify the path to the dataset folders.

## Training

To train the model, run the following file.

```
python train_FairFace_gender_ResNet50.py

```

## Acknowledgement

This work is supported by National Science Foundation (NSF) award no. 2129173. The code is inspired by [Dichao-Liu](https://github.com/Dichao-Liu/CMAL), [Du et al](https://github.com/PRIS-CV/PMG-Progressive-Multi-Granularity-Training) and many thanks to them.

## Citation

If you fine our work useful, please cite our paper
```
@inproceedings{fine-icpr,
  title=FineFACE: Fair Facial Attribute Classification Leveraging Fine-grained Features},
  author={Ayesha Manzoor and Ajita Rattani},
  booktitle    = {{The International Conference on Pattern Recognition (ICPR)}},
  publisher    = {{IAPR}},
  year         = {2024}
}
```

   
   
