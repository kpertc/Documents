#data 

### Resources

![[Data Science VS Machine Learning#^122696]]

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

Simplest form of machine learning: Linear Regression
##### Don't expect 100% accuracy
- Limitations of ML
- Insufficient data
- Mislabeled data
- Ambiguous labels

### Deep Learning

"Deep Learning" use interchangeably with "Machine Learning"

> [!NOTE]- (Artificial) Neural Network
> Neural networks were originally inspired by the brain, but the details of how they work are almost completely unrelated to how biological brains work.

Learning → find number weights and biases
Neuron → function() / mathematical equation

tensor: high dimensional array

Machine learning tend to learn well when:
1. Concept is simple 
2. A lot data  available 

![[Data Science VS Machine Learning#Machine Learning Process]]

![[Data Science VS Machine Learning#Data Science Process]]

Task
- Automated Visual Inspection

##### Neural Network
> [But what is a neural network? | Deep learning chapter 1](https://youtu.be/aircAruvnKk?si=tSTTZQnpATkMo_Up)

Inspired by brain
Neuron → hold a number → "Activation"
hidden layers

higher number of neurons -> lower number of neurons of output

- Convolutional Neural Network, CNN 卷积神经网络 - Good for image recognition
擅长处理空间局部特征
> 	是一种深度学习模型，它在图像处理、视频识别和自然语言处理等领域特别有效。CNN在视觉识别任务中特别流行，因为它们能够从图像数据中自动、有效地学习空间层级特征。
- Long short-term memory network, Good for speech recognition

RNN, recurrent neural networks (RNNs)
擅长处理序列数据

Multi-Layer Perceptrons, MLPs

---
### Diffusion model
扩散模型
noise ↔︎ denoise
creating images, audio, and other media, oppose to traditional - GAN / VAE
Require large amount VRAM

### Transformers
Text / General
- LLMs -GPT

Have better understanding but slow to generate media
Text, video, audio → Token →

- Generative Pre-trained Transformer → [[Large Language Models (LLMs)]]


> [Transformers, the tech behind LLMs | Deep Learning Chapter 5](https://youtu.be/wjZofJX0v4M?si=LQkrtPvJrsBy5a0l)
- To Vector
	- Repeat
		↪ Attention Block
		↪ Attention, MLP
		↪ softmax (T, temperature)

Backpropagation
model parameters are refers to weights
`weights x data = output`
embedding matrix: embed token to vector?
unembedding matrix
context size → matrix size?

Logits → are the raw, unnormalized scores a language model outputs for each possible next token before converting them into probabilities.

Attention
Calculate how much each token attend (relevant) to another token
- key matrix
- query matrix
- value matrix

Query vector? (Adjective)
Multiply matrix on noun? 
masking

---
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

[**Hugging Face**](https://huggingface.co/)
- 一家主要刚开始致力于NLP的人工智能公司
- 一套方便进行深度学习相关使用开发的工具集合