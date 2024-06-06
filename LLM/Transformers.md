> python transformer库笔记

# 概念

- 标量
- 向量（一维，二维，三维...）
- 张量 (描述具有任意数量轴的𝑛维数组的通用方法)

# 术语

- batch_size 样本批次
- context_len 文本长度
- d_model 学习维度（超参数）
- num_heads 多头机制头数（切分d_model）

# 训练流程

> 大模型实际就两文件
![[Pasted image 20240428104308.png]]

![[Pasted image 20240428135709.png]]

![[Pasted image 20240509093446.png]]

![[Pasted image 20240509093534.png]]
![[Pasted image 20240428105040.png]]

![[Pasted image 20240428113207.png]]
## Tokenization

- 加载分词器tokenizer.model
```python
# 默认加载目录下tokenizer.model文件
tokenizer = AutoTokenizer.from_pretrained("../finetune_demo/model", trust_remote_code=True)
```

- Encoding
```python
# 分词tokenization
tokenizer.tokenize("Using a Transformer network is simple")
# ['▁Using', '▁a', '▁Trans', 'former', '▁network', '▁is', '▁simple']

# convert_tokens_to_ids
tokenizer("Using a Transformer network is simple")
# {'input_ids': [64790, 64792, 6316, 260, 3107, 17639, 2804, 323, 2718], 'attention_mask': [1, 1, 1, 1, 1, 1, 1, 1, 1], 'position_ids': [0, 1, 2, 3, 4, 5, 6, 7, 8]}
```

- Decoding
```python
tokenizer.decode([64790, 64792, 6316, 260, 3107, 17639, 2804, 323, 2718])
# [gMASK] sop Using a Transformer network is simple
```

- 随机初始化token词汇表维度向量（`Token Embedding Look-up Table`）
![[Pasted image 20240429161121.png]]

## Word Embedding

4段文本(batch_size=4，假设ctx_len=16)
1. `hello world`
2. `today is monday`
3. `Attention Is All You Need`
4. `大模型令人头秃`

4段样本转换成token索引
![[Pasted image 20240429161208.png]]

每个样本转换成维度向量
![[Pasted image 20240429161604.png]]

## Positional Encoding

$$PE_{(pos,2i)}=sin(pos/10000^{2i/d_{\mathrm{model}}})$$
$$PE_{(pos,2i+1)}=cos(pos/10000^{2i/d_{\mathrm{model}}})$$
```python
for pos in range(16):  
    line = []  
    for i in range(32):  
        line.append(sin(pos / 10000 ** (i * 2 / 64)))  
        line.append(cos(pos / 10000 ** (i * 2 / 64)))  
    print(line)
```

![[Pasted image 20240429160320.png]]


## Attention - QKV

![[Pasted image 20240428144752.png]]

![[Pasted image 20240428145116.png]]

## Layer Normalization

> 层归一化规则:
> 1. 均值为0
> 2. 方差为1

$$y=\frac{\alpha-\mu}{\sqrt{\sigma^{2}+\epsilon}}\odot\gamma+\beta $$
两个可调参数：系数γ、偏置项β

```python
// bias对应上面偏置项β
nn.LayerNorm(bias=True)
```

## softmax

>在机器学习尤其是深度学习中，softmax是个非常常用而且比较重要的函数，尤其在多分类的场景中使用广泛。他把一些输入映射为0-1之间的实数，并且归一化保证和为1，因此多分类的概率之和也刚好为1。

$$\sigma(\overrightarrow{z})_{i}=\frac{e^{z_{i}}}{\sum_{j=1}^{k}e^{z_j}}$$
```python
torch.softmax()
```

![[Pasted image 20240428142844.png]]


## 交叉熵损失函数

# 推理原理

![[Pasted image 20240428161257.png]]














# 静态配置

```python 
TOKENIZER_CONFIG_FILE = "tokenizer_config.json"
```

# 代码

## AutoTokenizer

### from_pretrained
1. 根据配置加载`get_tokenizer_config`



## AutoModelForCausalLM

```python
from_pretrained
	
```