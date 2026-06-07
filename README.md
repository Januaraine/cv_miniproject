# Single-Image Conditional GAN

Shape-Conditioned Image Generation from a Single Image Using NeRF Positional Encoding and Conditional GAN

## Overview

This project investigates shape-conditioned image generation from a single image using a Conditional GAN framework.

The model learns to generate realistic RGB images from structural guidance signals derived from a single training image. To overcome the lack of training data, Thin Plate Spline (TPS) warping and edge-based augmentations are used to create self-supervised training pairs.

Additionally, NeRF-style positional encoding is introduced to provide richer spatial information to the generator and improve high-frequency detail reconstruction.

The project was developed for COMP6528 Computer Vision at the Australian National University.

## Project Structure
```
cv_miniproject/
│
├── dataset/
│   ├── jcsmr.jpg
│   ├── single_image_dataset.py
│   ├── with_training_process.txt
│   └── without_training_process.txt
│
├── models/
│   ├── generator.py
│   ├── discriminator.py
│   └── positional_encoding.py
│
├── utils/
│   ├── loss_functions.py
│   ├── metrics.py
│   └── visualize.py
│
├── results/
│   ├── Figure_1.png
│   └── Figure_2.png
│
├── test.py
│
├── README.md
└── LICENSE
```

## Method

The framework consists of four major components:

1. TPS-based structural augmentation
2. NeRF positional encoding
3. U-Net Generator
4. Multi-scale PatchGAN Discriminator

Training pairs are generated from a single image using TPS warping and edge extraction.

The generator learns:

G(condition) → RGB image

while the discriminator evaluates image realism at multiple scales.

The training objective combines:

- Adversarial Loss
- L1 Reconstruction Loss

## Results

### Training Losses

| Model | Initial L1 Loss | Final L1 Loss |
|---------|---------|---------|
| With Positional Encoding | 28.08 | 3.22 |
| Without Positional Encoding | 14.76 | 2.91 |

### Generated Images

#### Original Training Image

![Original](dataset/jcsmr.jpg)

#### Generated Result (With Positional Encoding)

![With PE](results/with_positional_encoding/fake_epoch_9.png)

#### Generated Result (Without Positional Encoding)

![Without PE](results/without_positional_encoding/fake_epoch_9.png)

## Key Findings

- TPS augmentation successfully enables learning from a single image.
- Conditional GANs can generate visually plausible shape-conditioned outputs.
- NeRF positional encoding improves visual sharpness.
- Under extremely limited data, positional encoding may slow convergence.

## References

- Goodfellow et al., GAN, NeurIPS 2014
- Isola et al., Pix2Pix, CVPR 2017
- Shaham et al., SinGAN, ICCV 2019
- Mildenhall et al., NeRF, ECCV 2020
- Vinker et al., DeepSIM, ICCV 2021

## License

This project is released under the MIT License.
