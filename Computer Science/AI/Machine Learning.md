#data 

### Resources

![[Data Science VS Machine Learning#^122696]]

<br>

### Data for Machine Learning

data → dataset (成对数据集) for Supervised Learning A - B mapping

Data problems → Garbage in / Garbage out
-   Incorrect labels
-   Missing values

> [!tip]
> AI team and IT team should collaborate at early stage as possible to figure out what data is useful for AI team

Image, Audio, Text → unstructured data

Training set
Test set →  evaluate algorithm performance

##### Don't expect 100% accuracy
- Limitations of ML
- Insufficient data
- Mislabeled data
- Ambiguous labels

<br>

### Deep Learning

"Deep Learning" use interchangeably with "Machine Learning"

> [!NOTE]- (Artificial) Neural Network
> Neural networks were originally inspired by the brain, but the details of how they work are almost completely unrelated to how biological brains work.

Learning → find number weights and biases
Neuron → function() / mathematical equation 

Machine learning tend to learn well when:
1. Concept is simple 
2. A lot data  available 

<br>

###

![[Data Science VS Machine Learning#Machine Learning Process]]

![[Data Science VS Machine Learning#Data Science Process]]


Automated Visual Inspection

### Machine Learning Framework
- TensorFlow
- PyTorch
- Keras
- MXNet
- CNTK
- Caffe
- PaddlePaddle
- Scikit-learn
- R
- Weka

<br>

[**Hugging Face**](https://huggingface.co/)
- 一家主要刚开始致力于NLP的人工智能公司
- 一套方便进行深度学习相关使用开发的工具集合



Convolutional Neural Network, CNN 卷积神经网络
> 是一种深度学习模型，它在图像处理、视频识别和自然语言处理等领域特别有效。CNN在视觉识别任务中特别流行，因为它们能够从图像数据中自动、有效地学习空间层级特征。



---
### Diffusion model
扩散模型
noise ↔︎ denoise
creating images, audio, and other media, oppose to traditional - GAN / VAE
Require large amount VRAM

### Transformer model
大语言模型
Text / General
- LLMs -GPT

Have better understanding but slow to generate media
Text, video, audio → Token →