<div align="center">

<h2>⚡LightingDiT + TREAD</h2>

**_Even faster variant of [LightningDiT](https://github.com/hustvl/LightningDiT) (CVPR 2025 Oral) by combining it with [TREAD](https://github.com/CompVis/tread) (ICCV 2025)_**

<img width="1363" height="251" alt="image" src="https://github.com/user-attachments/assets/41b04b01-04e1-48fd-93e7-f37faee2a3e4" />
</div>
<div align="center">
<p>28% better FID (without CFG)</p>
</div>


[![license](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![paper](https://img.shields.io/badge/ICCV'25-TREAD-b31b1b.svg)]([https://arxiv.org/abs/2501.01423](https://arxiv.org/abs/2501.04765))
[![paper](https://img.shields.io/badge/CVPR'25-VA_VAE-b31b1b.svg)](https://arxiv.org/abs/2501.01423)
[![arXiv](https://img.shields.io/badge/NeurIPS'24-FasterDiT-b31b1b.svg)](https://arxiv.org/abs/2410.10356)

</div>
<div align="center">
<img src="images/vis.png" alt="Visualization">
</div>




## 🎯 How to Use

### Installation

```
conda create -n lightningdit python=3.10.12
conda activate lightningdit
pip install -r requirements.txt
```


### Inference with Pre-trained Models

- Download weights and data infos:

    - Download pre-trained models
        | Tokenizer | Generation Model | FID | FID cfg |
        |:---------:|:----------------|:----:|:---:|
        | [VA-VAE](https://huggingface.co/hustvl/vavae-imagenet256-f16d32-dinov2/blob/main/vavae-imagenet256-f16d32-dinov2.pt) | [LightningDiT-XL-800ep](https://huggingface.co/hustvl/lightningdit-xl-imagenet256-800ep/blob/main/lightningdit-xl-imagenet256-800ep.pt) | 2.17 | 1.35 |
        |           | [LightningDiT-XL-64ep](https://huggingface.co/hustvl/lightningdit-xl-imagenet256-64ep/blob/main/lightningdit-xl-imagenet256-64ep.pt) | 5.14 | 2.11 |

    - Download [latent statistics](https://huggingface.co/hustvl/vavae-imagenet256-f16d32-dinov2/blob/main/latents_stats.pt). This file contains the channel-wise mean and standard deviation statistics.

    - Modify config file in ``configs/reproductions`` as required. 

- Fast sample demo images:

    Run:
    ```
    bash bash run_fast_inference.sh ${config_path}
    ```
    Images will be saved into ``demo_images/demo_samples.png``, e.g. the following one:
    <div align="center">
    <img src="images/demo_samples.png" alt="Demo Samples" width="600">
    </div>

- Sample for FID-50k evaluation:
    
    Run:
    ```
    bash run_inference.sh ${config_path}
    ```
    NOTE: The FID result reported by the script serves as a reference value. The final FID-50k reported in paper is evaluated with ADM:

    ```
    git clone https://github.com/openai/guided-diffusion.git
    
    # save your npz file with tools/save_npz.py
    bash run_fid_eval.sh /path/to/your.npz
    ```

## 🎮 Train Your Own Models

 
- **We provide a 👆[detailed tutorial](docs/tutorial.md) for training your own models of 2.1 FID score within only 64 epochs. It takes only about 10 hours with 8 x H800 GPUs.** 


## ❤️ Acknowledgements

This repo is a modification of [LightningDiT](https://github.com/hustvl/LightningDiT), which is mainly built on [DiT](https://github.com/facebookresearch/DiT), [FastDiT](https://github.com/chuanyangjin/fast-DiT) and [SiT](https://github.com/willisma/SiT). The VAVAE codes are mainly built with [LDM](https://github.com/CompVis/latent-diffusion) and [MAR](https://github.com/LTH14/mar). Thanks for all these great works.

## 📝 Citation

If you find this work useful, please cite the related papers:

```
# ICCV 2025
@article{krause2025tread,
  title={TREAD: Token Routing for Efficient Architecture-agnostic Diffusion Training},
  author={Krause, Felix and Phan, Timy and Gui, Ming and Baumann, Stefan Andreas and Hu, Vincent Tao and Ommer, Bj{\"o}rn},
  journal={arXiv preprint arXiv:2501.04765},
  year={2025}
}

# CVPR 2025
@inproceedings{yao2025vavae,
  title={Reconstruction vs. generation: Taming optimization dilemma in latent diffusion models},
  author={Yao, Jingfeng and Yang, Bin and Wang, Xinggang},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  year={2025}
}

# NeurIPS 2024
@article{yao2024fasterdit,
  title={Fasterdit: Towards faster diffusion transformers training without architecture modification},
  author={Yao, Jingfeng and Wang, Cheng and Liu, Wenyu and Wang, Xinggang},
  journal={Advances in Neural Information Processing Systems},
  volume={37},
  pages={56166--56189},
  year={2024}
}
```
