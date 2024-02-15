<h1 align="center"> LHRS-Bot: Empowering Remote Sensing with VGI-Enhanced Large Multimodal Language Model </h1> 

<h5 align="center"><em>Dilxat Muhtar*, Zhenshi Li* , Feng Gu, Xueliang Zhang, and Pengfeng Xiao</em>
</br>(*Equal Contribution)</h5>


<figure>
<div align="center">
<img src=https://pumpkintypora.oss-cn-shanghai.aliyuncs.com/lhrsbot.png width="20%">
</figure>
<p align="center">
  <a href="#news">News</a> |
  <a href="#introduction">Introduction</a> |
  <a href="#Preparation">Preparation</a> |
  <a href="#Demo">Demo</a> | 
  <a href="#acknowledgement">Acknowledgement</a> |
  <a href="#statement">Statement</a>
</p >



## News

+ **\[Feb 7 2024\]:** Model weights are now available on both Google Drive and Baidu Disk.
+ **\[Feb 6 2024\]:** Our paper now is available at [arxiv](https://arxiv.org/abs/2402.02544).
+ **\[Feb 2 2024\]:** We are excited to announce the release of our code and model checkpoint! Our dataset and training recipe will be update soon!

## Introduction

We are excited to introduce **LHRS-Bot**, a multimodal large language model (MLLM) that leverages globally available volunteer geographic information (VGI) and remote sensing images (RS). LHRS-Bot demonstrates a deep understanding of RS imagery and possesses the capability for sophisticated reasoning within the RS domain. In this repository, we will release our code, training framework, model weights, and dataset!

<figure>
<div align="center">
<img src=assets/performance.png width="50%">
</div>
  <div align="center">
<img src=assets/vis_example.png width="100%">
</div>
</figure>




## Preparation

### Installation

1. Clone this repository.

    ~~~shell
    git clone git@github.com:NJU-LHRS/LHRS-Bot.git
    cd LHRS-Bot
    ~~~

2. Create a new virtual enviroment

    ~~~shell
    conda create -n lhrs python=3.10
    conda activate lhrs
    ~~~

3. Install dependences and our package

    ~~~shell
    pip install -e .
    ~~~

### Checkpoints

+ LLaMA2-7B-Chat

    + Automaticaly download:

        Our framework is designed to automatically download the checkpoint when you initiate training or run a demo. However, there are a few preparatory steps you need to complete:

        1. Request the LLaMA2-7B models from [Meta website](https://llama.meta.com/llama-downloads/).

        2. After your request been processed, login to huggingface using your personal access tokens:

            ~~~shell
            huggingface-cli login
            (Then paste your access token and press Enter)
            ~~~

        3. Done!

    + Mannually download:

        + Download all the files from [HuggingFace](https://huggingface.co/meta-llama/Llama-2-7b-hf).

        + Change the following line of each file to your downloaded directory:

            + `/Config/multi_modal_stage{1, 2, 3}.yaml`

                ~~~yaml
                ...
                text:
                	...
                  path: ""  # TODO: Direct to your directory
                ...
                ~~~

            + `/Config/multi_modal_eval.yaml`

                ~~~yaml
                ...
                text:
                	...
                  path: ""  # TODO: Direct to your directory
                ...
                ~~~

+ LHRS-Bot Checkpoints:

	|                            Staeg1                            |                            Stage2                            |                            Stage3                            |
	| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
	| [Baidu Disk](https://pan.baidu.com/s/1CYjUgGSvdchTuGtxUFNkGA?pwd=sgi7), [Google Drive](https://drive.google.com/drive/folders/1LYrKJ_SpsNQEFTuo6N3rc-TLyaWb4d1Y?usp=drive_link) | [Baidu Disk](https://pan.baidu.com/s/1WYCVPqbizowvLyNGWx9mIw?pwd=986f), [Google Drive](https://drive.google.com/drive/folders/1ZPwkxvapEtvPoEdjKfvOe3j0SqpQeAu5?usp=drive_link) | [Baidu Disk](https://pan.baidu.com/s/1n1h_ZImeKTgvoNHjr5bq3Q?pwd=qhqw), [Google Drive](https://drive.google.com/drive/folders/1dzWTE1k935MjMVnfLtTJiIqw7yCj-e3m?usp=drive_link) |
	
	+ ⚠️ Ensure that the `TextLoRA` folder is located in the same directory as `FINAL.pt`. The name `TextLoRA` should remain unchanged. Our framework will automatically detect the version perceiver checkpoint and, if possible, load and merge the LoRA module.
	
	+ Development Checkpoint:
	
	    We will continually update our model with advanced techniques. If you're interested, feel free to download it and have fun :)
	    
	    |                         Development                          |
	    | :----------------------------------------------------------: |
	    | [Baidu Disk](https://pan.baidu.com/s/134VYRigS4f9TuMk7ekoZbg?pwd=dxk4), [Google Drive](https://drive.google.com/drive/folders/1UPJXGvFsrt-OSI732AaAzsD_FPNJOBK3?usp=drive_link) |

## Demo

+ Online Web UI demo with gradio:

    ~~~shell
    python lhrs_webui.py \
         -c Config/multi_modal_eval.yaml \           # config file
         --checkpoint-path ${PathToCheckpoint}.pt \  # path to checkpoint end with .pt
         --server-port 8000 \                        # change if you need
         --server-name 127.0.0.1 \                   # change if you need
         --share                                     # if you want to share with other
    ~~~

+ Command line demo:

  ~~~shell
  python cli_qa.py \
       -c Config/multi_modal_eval.yaml \                 # config file
       --model-path ${PathToCheckpoint}.pt \             # path to checkpoint end with .pt
       --image-file ${TheImagePathYouWantToChat} \       # path to image file (Only Single Image File is supported)
       --accelerator "gpu" \                             # change if you need ["mps", "cpu", "gpu"]
       --temperature 0.4 \
       --max-new-tokens 512
  ~~~



## Acknowledgement

+ We gratitude to the following repositories for their wonderful works:
    + [LLaVA](https://github.com/haotian-liu/LLaVA)
    + [MiniGPT-4](https://github.com/Vision-CAIR/MiniGPT-4)
    + [LLaMA](https://github.com/facebookresearch/llama)


## Statement

+ If you find our work is useful, please give us 🌟 in GitHub and consider cite our paper:

    ~~~tex
    @misc{2402.02544,
    Author = {Dilxat Muhtar and Zhenshi Li and Feng Gu and Xueliang Zhang and Pengfeng Xiao},
    Title = {LHRS-Bot: Empowering Remote Sensing with VGI-Enhanced Large Multimodal Language Model},
    Year = {2024},
    Eprint = {arXiv:2402.02544},
    }
    ~~~

+ Licence: Apache