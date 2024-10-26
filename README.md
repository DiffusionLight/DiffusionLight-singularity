# DiffusionLight-singularity
Singularity setup script for DiffusiongLight. This is useful when you want to run diffusion light on a machine that doesn't have root (Solution for [Issue #5](https://github.com/DiffusionLight/DiffusionLight/issues/5#issuecomment-2439480877))


## Running on Singularity

### Pre-requirement

You need to install Singularity-CE on the machine that you want to run first. 

You can follow [this guide](https://chatgpt.com/share/671cce80-9310-800d-9447-838b4a06d2fc) to install Singularity-CE without root 

Alternatively, you can use [Apptainer](https://apptainer.org/), but I'm going to stick with Singularity-CE for this example.

### Clone this repository 

We first clone this directory and  `cd` into it. because we need 2 files with `singularity.def` for building the container image and `requirement.txt` to install python component

```
git clone https://github.com/DiffusionLight/DiffusionLight-singularity.git
cd DiffusionLight-singularity
```

### Building SIF image 

Then we build the image into SIF format. 

```
singularity build --fakeroot diffusionlight.sif singularity.def
```

### Running DiffusionLight

We clone the main repo directory and `cd` into it. 

```
https://github.com/DiffusionLight/DiffusionLight.git
cd DiffusionLight
```

Note that if diffusionlight.sif is not in this folder, please move it to the DiffusionLight folder using the mv command. 

```
mv ../diffusionlight.sif diffusionlight.sif
```

Assume we will input the image in the `example` folder and output to the `output` folder. We run

```
# inpainting
singularity exec --nv diffusionlight.sif python inpaint.py --dataset example --output_dir output
```

Other python file under DiffusionLight should work with the same environment including [LoRA-Trainer](https://github.com/DiffusionLight/DiffusionLight-LoRA-Trainer) and [Evaluation](https://github.com/DiffusionLight/DiffusionLight-evaluation)

You can run all of them by adding using  `singularity exec --nv diffusionlight.sif <your command>`


## Citation

```
@inproceedings{Phongthawee2023DiffusionLight,
 author = {Phongthawee, Pakkapon and Chinchuthakun, Worameth and Sinsunthithet, Nontaphat and Raj, Amit and Jampani, Varun and Khungurn, Pramook and Suwajanakorn, Supasorn},
 title = {DiffusionLight: Light Probes for Free by Painting a Chrome Ball},
 booktitle = {ArXiv},
 year = {2023},
}
```

## Visit us 🦉
[![Vision & Learning Laboratory](https://i.imgur.com/hQhkKhG.png)](https://vistec.ist/vision) [![VISTEC - Vidyasirimedhi Institute of Science and Technology](https://i.imgur.com/4wh8HQd.png)](https://vistec.ist/)