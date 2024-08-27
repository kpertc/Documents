#python 

[Stable Diffusion Crash Course for Beginners by freeCodeCamp.org](https://youtu.be/dMkiOex_cKU)

## Stable Diffusion webui AUTOMATIC1111
[https://github.com/AUTOMATIC1111/stable-diffusion-webui](https://github.com/AUTOMATIC1111/stable-diffusion-webui)

### Plugin:
Control Net - allow use image / hand drawing reference

### API
use API request to access the server


Negative prompt

Easy negative

Install on MAC
1. Install dependency `brew install cmake protobuf rust python@3.10 git wget`
2. Clone the git repo
3. Copy models to model/stable diffusion folder `.ckpt`
4. run `webui.sh` at repo
5. config for performance, `webui-user.sh`

```sh
export COMMANDLINE_ARGS=“—medvram”
```


## ComfyUI

Mac 安装 [https://youtu.be/I8g8rf1LAvI?si=B1FJIx2Q5YvPNQgp](https://youtu.be/I8g8rf1LAvI?si=B1FJIx2Q5YvPNQgp)





## Diffusers 

by Hugging Face

- Python3.7+
- [Pytorch1.7+](https://pytorch.org/)
- transformers
- Diffusers

```python
# 导入需要的模块  
import torch  
from diffusers import StableDiffusionPipeline  
  
pipe = StableDiffusionPipeline.from_pretrained("stabilityai/stable-diffusion-2-base")  
#pipe = pipe.to("cuda")  
#pipe.enable_attention_slicing()  
prompt = "a green apple"  
image = pipe(prompt).images[0]  
image.show()
```



模型会下载到 `~/.cache/huggingface` 目录下

`s/it` second / iteration

## LoRA (Low-Rank Adaptation of Large Language Models)

Fine tune
> ... 和hyper-network，controlNet一样，都是在不修改SD模型的前提下，利用少量数据训练出一种画风/P/人物，实现定制化需求，所需的训练资源比训练SD模要小很多，非常适合社区使用者和个人开发

Train a LoRA “Patch to checkpoint model” [https://civitai.com/models/22530](https://civitai.com/models/22530)

> You can train a mediocre Lora with a bare minimum of 5 images, but I recommend 20 or more, and up to 1000.

can use multiple LoRAs




CLIP - 语义理解　描述词汇
LDM - 图像理解　噪声种子　随机噪声　潜空间
VAE - 性能友好　图像生成


【秋葉aaaki的个人空间-哔哩哔哩】 [https://b23.tv/aFec6JT](https://b23.tv/aFec6JT)


Text Encoder → Noise Predictor → Variational Auto Encoder (VAE)