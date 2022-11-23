# DiffEdit with Stable Diffusion
Unofficial implementation of “DiffEdit: Diffusion-based semantic image editing with mask guidance” with [Stable Diffusion](https://github.com/CompVis/stable-diffusion), for better sample efficiency, we use [DPM-solver](https://github.com/LuChengTHU/dpm-solver), as sample method.

Paper: https://arxiv.org/abs/2210.11427

![paper](./assets/paper.png)



## Requirements

A suitable [conda](https://conda.io/) environment named `ldm` can be created
and activated with:

```
conda env create -f environment.yaml
conda activate ldm
```

You can also update an existing [latent diffusion](https://github.com/CompVis/latent-diffusion) environment by running

```
conda install pytorch torchvision -c pytorch
pip install transformers==4.19.2 diffusers invisible-watermark
pip install -e .
```



## usage

just run `diffedit.ipynb` using jupyter notebook.

### important parameters:

```python
encode_ratio: float = 0.6
# encode_ratio indicate how noisy the img is add with, if ratio is near zero, the origin img is likely to return, if ratio is near 1.0, it may casue some problem
clamp_rate: float = 4
# the map value will be clamped to map.mean() * clamp_rate, then values will be scaled into 0~1, then term into binary(split at 0.5). so if a map value is large than map.mean() * clamp_rate * 0.5 will be encode to 1, less will be encode to 0. 
# so the larger clamp rate is, less pixes will be encode to 1, the small clamp rate is, the more pixes will be encode to 1.
ddim_steps: int = 15
# for dpm-solver, steps do not need be too large
# encourage to use other parameter(like order, predict_x0) of dpm-solver
```







## results

| A bowl of fruits               | generated mask               | A bowl of pears                |
| ------------------------------ | ---------------------------- | ------------------------------ |
| ![origin](./assets/origin.png) | ![origin](./assets/mask.png) | ![origin](./assets/target.png) |

