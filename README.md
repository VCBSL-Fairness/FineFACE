# FineFACE: Fair Facial Attribute Classification Leveraging Fine-grained Features

## Table of Contents
- [Overview](https://github.com/VCBSL-Fairness/FineFACE?tab=readme-ov-file#overview)
- [FineFACE network architecture](https://github.com/VCBSL-Fairness/FineFACE?tab=readme-ov-file#fineface-network-architecture)
- [Approach](https://github.com/VCBSL-Fairness/FineFACE/blob/main/README.md#approach)
- [Environment](https://github.com/VCBSL-Fairness/FineFACE?tab=readme-ov-file#environment)
- [Datasets](https://github.com/VCBSL-Fairness/FineFACE?tab=readme-ov-file#datasets)
- [Training](https://github.com/VCBSL-Fairness/FineFACE?tab=readme-ov-file#training)
- [Acknowledgement](https://github.com/VCBSL-Fairness/FineFACE?tab=readme-ov-file#acknowledgement)
- [Citation](https://github.com/VCBSL-Fairness/FineFACE?tab=readme-ov-file#citation)

## Overview

Published research highlights the presence of demographic bias in automated facial attribute classification algorithms, particularly impacting women and individuals with darker skin tones. Existing bias mitigation techniques typically require demographic annotations and often obtain a trade-off between fairness and accuracy, i.e., Pareto inefficiency. Facial attributes, whether common ones like gender or others such as "chubby" or "high cheekbones", exhibit high interclass similarity and intraclass variation across demographics leading to unequal accuracy. This necessitates the use of local and subtle cues using fine-grained analysis for differentiation.  This paper proposes a novel approach to fair facial attribute classification by framing it as a fine-grained classification problem. Our approach effectively integrates both low-level local features (like edges and color) and high-level semantic features (like shapes and structures) through cross-layer mutual attention learning. Here, shallow to deep CNN layers function as experts, offering category predictions and attention regions.

## FineFACE network architecture
![image](https://github.com/user-attachments/assets/6b11d3d4-c876-411e-b89d-33bffe5a7545)

This figure illustrates this method by introducing three experts e1, e2, e3, on a 5-stage backbone CNN (e.g., ResNet50). The workflow of each expert and the concatenation of experts are depicted in different colors. Each expert receives feature maps from a specific layer as input and generates a categorical prediction along with an attention region, which is used for data augmentation by other experts. This architecture is trained in multiple steps within each iteration. We start by training the deepest expert (e3), followed by the shallower experts. Finally, in the last step, we train the concatenation of experts to enhance overall performance.

## Approach

Enhancing feature representation for each demographic subgroup is crucial in improving fairness without compromising overall performance. Traditional facial attribute classifiers rely predominantly on high-level discriminative and semantically meaningful information often obtained from the final layers of the deep convolutional neural network(CNN). However, the lower layers of the deep learning model capture (low-level) essential features and patterns in faces vital for attribute classification, such as (a) facial contours and edges, including the outline of the face, jawline and cheekbones, (b) texture of facial regions, such as skin and hair, (c) position and shape information, and (d) lighting condition and its effect on the appearance of facial features. Integrating low-level details from the lower layers of the model will capture local and detailed cues in the learned feature representation.

In our quest to identify these subtle and local cues for learning enhanced feature representation, we aim to leverage fine-grained analysis, integrating both high- and low-level features, toward fair facial attribute classification, FineFACE. This is facilitated through a cross-layer mutual attention learning technique that learns fine-grained features by considering the layers of a deep learning model from shallow to deep as independent ’experts’ knowledgeable about low-level detailed to high-level semantic information, respectively. These experts are trained in leveraging mutual data augmentation to incorporate attention regions proposed by other experts. An ordinary deep learning model can be considered to use only the deepest expert (using high-level semantic information) for classification. Contrarily, our method consolidates the prediction of the categorical label and the attention region of each expert for the final facial attribute classification task.

## Environment

This source code was tested on

- Python = 3.10.12
- PyTorch = 2.2.0+cu118
- torchvision = 0.17.0+cu118
- GPU Model: NVIDIA A10
- NVIDIA-SMI Version: 545.23.08

## Datasets

1. Download the [FairFace](https://github.com/joojs/fairface), [UTKFace](https://susanqq.github.io/UTKFace/), [LFWA+](https://drive.google.com/drive/folders/0B7EVK8r0v71pQ3NzdzRhVUhSams?resourcekey=0-Kpdd6Vctf-AdJYfS55VULA) and [CelebA](https://mmlab.ie.cuhk.edu.hk/projects/CelebA.html) datasets and organize the structure as follows:

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

   
   
