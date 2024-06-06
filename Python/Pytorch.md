
```python
import torch
import torch.nn as nn
```

# torch


### arange

### stack
将张量数组升维成一个更高维的张量，如：将5个[3×4]矩阵数据，连接成一个[5×3×4]的矩阵，可通过dim参数调整维度下标，默认0

### exp
对矩阵所有元素做以下计算：
$$y_i=e^{x_i}$$
### tril
返回一个矩阵主对角线以下的下三角矩阵，其它元素全部为0 00。当输入是一个多维张量时，返回的是同等维度的张量并且最后两个维度的下三角矩阵的

```python
torch.tril(torch.onse(4,4))

"""
tensor([[1., 0., 0., 0.],
        [1., 1., 0., 0.],
        [1., 1., 1., 0.],
        [1., 1., 1., 1.]])
"""
```


## Tensor

### parameter



### unsqueeze
扩展维度
```python
x = torch.range(0,3)
# [0,1,2]
y = x.unsqueeze(0)
# [[0,1,2]]
y = x.unsqueeze(1)
# [[0],[1],[2]] 
```

### squeeze
降低维度

### expand
维度不变, 扩展某一个维的大小（扩展前该维的大小必须为1）; -1表示该维度不变; 扩展（expand）张量**不会分配新的内存**，只是在存在的张量上创建一个新的视图（view）
```python
x = torch.arange(2).reshape(1,2,1)
# shape [1,2,1]
y = x.expand(3,-1,3)
# y_shape [3,2,3], x_shape [1,2,1]
```

### masked_fill
在掩码为 True 时，用值填充自身张量的元素。掩码的形状必须与底层张量的形状一致。
```python
mask = torch.tril(torch.ones(5,5))
wh = torch.ones(5,5)  
wh = wh.masked_fill(mask == 1, float(-1))

"""
tensor([[-1.,  1.,  1.,  1.,  1.],
        [-1., -1.,  1.,  1.,  1.],
        [-1., -1., -1.,  1.,  1.],
        [-1., -1., -1., -1.,  1.],
        [-1., -1., -1., -1., -1.]])
"""
```

# nn

### Embedding
随机生成一个向量查找表
```python
x = nn.Embedding(5, 2)  
print(x.weight.data)
```

### Linear

```python
# 构造器
def __init__(self, in_features: int, out_features: int, bias: bool = True,  
             device=None, dtype=None) -> None:

# 样例
linear = nn.Linear(in_features=10, out_features=20) # 创建一个全连接神经网络
x = torch.randn(2,3,10) # 随机生成一个张量
out = linear(x) # out.shape[2,3,20]

# 注意* Linear的in_features参数必须与x张量的最后一个维度大小相等
```

### LayerNorm


### Module

```python
class Model(nn.Module):
	def __init__(self, in_dim, hidden_dim1, hidden_dim2, out_dim):
		self.layer1 = nn.Linear(in_dim, hidden_dim1)
		self.layer2 = nn.Linear(hidden_dim1, hidden_dim2)
		self.layer3 = nn.Linear(hidden_dim2, out_dim)
    
	def forward(self, x):
		x = self.layer1(x)	
		x = self.layer2(x)	
		x = self.layer3(x)
	    return x	
```

### 梯度

>损失函数：$$loss=\frac{1}{2}(y-\hat{y})^2 $$