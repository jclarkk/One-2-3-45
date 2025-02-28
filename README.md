<p align="center" width="100%">
<img src="https://github.com/Dustinpro/Dustinpro/assets/23076389/0fbdb69a-0fb4-4b42-b9da-e0b28532bdfd"  width="80%" height="80%">
</p>


<p align="center">
  [<a href="https://arxiv.org/pdf/2306.16928.pdf"><strong>Paper</strong></a>]
  [<a href="http://one-2-3-45.com"><strong>Project</strong></a>]
  [<a href="https://huggingface.co/spaces/One-2-3-45/One-2-3-45"><strong>Demo</strong></a>]
  [<a href="#citation"><strong>BibTeX</strong></a>]
</p>

<p align="center">
  <a href="https://huggingface.co/spaces/One-2-3-45/One-2-3-45">
    <img alt="Hugging Face Spaces" src="https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Space_of_the_Week_%F0%9F%94%A5-blue">
  </a>
</p>

One-2-3-45 rethinks how to leverage 2D diffusion models for 3D AIGC and introduces a novel forward-only paradigm that avoids the time-consuming optimization.

https://github.com/One-2-3-45/One-2-3-45/assets/16759292/a81d6e32-8d29-43a5-b044-b5112b9f9664



https://github.com/One-2-3-45/One-2-3-45/assets/16759292/5ecd45ef-8fd3-4643-af4c-fac3050a0428


## News
**[08/18/2023]**
Inference code released.

**[07/24/2023]**
Our demo reached the HuggingFace top 4 trending and was featured in 🤗 Spaces of the Week 🔥! Special thanks to HuggingFace 🤗 for sponsoring this demo!!

**[07/11/2023]**
[Online interactive demo](https://huggingface.co/spaces/One-2-3-45/One-2-3-45) released! Explore it and create your own 3D models in just 45 seconds! 

**[06/29/2023]**
Check out our [paper](https://arxiv.org/abs/2306.05425). [[X](https://twitter.com/_akhaliq/status/1674617785119305728)]

## Installation
Hardware requirement: an NVIDIA GPU with memory >=18GB (_e.g._, RTX 3090 or A10). Tested on Ubuntu.

We offer two ways to setup the environment:

### Traditional Installation
<details>
<summary>Step 1: Install Debian packages. </summary> 

```bash
sudo apt update && sudo apt install git-lfs libsparsehash-dev build-essential
```
</details>

<details>
<summary>Step 2: Create and activate a conda environment. </summary>

```bash
conda create -n One2345 python=3.10
conda activate One2345
```
</details>

<details>
<summary>Step 3: Clone the repository to the local machine. </summary>

```bash
# Make sure you have git-lfs installed.
git lfs install
git clone https://github.com/One-2-3-45/One-2-3-45
cd One-2-3-45
```
</details>

<details>
<summary>Step 4: Install project dependencies using pip. </summary>

```bash
# Ensure that the installed CUDA version matches the torch's cuda version.
# Example: CUDA 11.8 installation
wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda_11.8.0_520.61.05_linux.run
sudo sh cuda_11.8.0_520.61.05_linux.run
export PATH="/usr/local/cuda-11.8/bin:$PATH"
export LD_LIBRARY_PATH="/usr/local/cuda-11.8/lib64:$LD_LIBRARY_PATH"
# Install PyTorch 2.0
pip install --no-cache-dir torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
# Install dependencies
pip install -r requirements.txt
# Install inplace_abn and torchsparse
export TORCH_CUDA_ARCH_LIST="7.0;7.2;8.0;8.6+PTX" # CUDA architectures. Modify according to your hardware.
export IABN_FORCE_CUDA=1
pip install inplace_abn
FORCE_CUDA=1 pip install --no-cache-dir git+https://github.com/mit-han-lab/torchsparse.git@v1.4.0
```
</details>

<details>
<summary>Step 5: Download model checkpoints. </summary>

```bash
python download_ckpt.py
```
</details>


### Installation by Docker Images
<details>
<summary>Option 1: Pull and Play (environment and checkpoints). (~22.3G)</summary> 

```bash
# Pull the Docker image that contains the full repository.
docker pull chaoxu98/one2345:demo_1.0
# An interactive demo will be launched automatically upon running the container.
# This will provide a public URL like XXXXXXX.gradio.live
docker run --name One-2-3-45_demo --gpus all -it chaoxu98/one2345:demo_1.0
```
</details>

<details>
<summary>Option 2: Environment Only. (~7.3G)</summary> 

```bash
# Pull the Docker image that installed all project dependencies.
docker pull chaoxu98/one2345:1.0
# Start a Docker container named One2345.
docker run --name One-2-3-45 --gpus all -it chaoxu98/one2345:1.0
# Get a bash shell in the container.
docker exec -it One-2-3-45 /bin/bash
# Clone the repository to the local machine.
git clone https://github.com/One-2-3-45/One-2-3-45
cd One-2-3-45
# Download model checkpoints. 
python download_ckpt.py
# Refer to getting started for inference.
```
</details>

## Getting started (Inference)

First-time running will take longer time to compile the models.

Expected time cost per image: 40s on an NVIDIA A6000.
```bash
# 1. Script
python run.py --img_path PATH_TO_INPUT_IMG --half_precision

# 2. Interactive demo (Gradio) with a friendly web interface
#    An URL will be provided in the output 
#    (Local: 127.0.0.1:7860; Public: XXXXXXX.gradio.live)
cd demo/
python app.py

# 3. Jupyter Notebook
example.ipynb
```


## Citation

If you find our code helpful, please cite our paper:

```
@misc{liu2023one2345,
      title={One-2-3-45: Any Single Image to 3D Mesh in 45 Seconds without Per-Shape Optimization}, 
      author={Minghua Liu and Chao Xu and Haian Jin and Linghao Chen and Mukund Varma T and Zexiang Xu and Hao Su},
      year={2023},
      eprint={2306.16928},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
```
