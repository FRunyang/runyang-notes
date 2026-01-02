---
title: PyTorch参数的初始化与冻结部分参数训练
date: 2020-06-09 23:52:08
tags:
  - pytorch编程
  - Code
cover: https://user-images.githubusercontent.com/60562661/84796426-30618080-b02b-11ea-848a-f3f8bc9ecff6.jpg
---



>在平时训练中，经常会有冻结某些层的参数，单独训练其他参数以及载入预训练模型来初始化参数的需求，最近也是研究了一下如何实现，记录一下相关的知识。


### PyTorch中参数的冻结

​	模型的冻结即参数不再更新即可，可以通过梯度来控制，Pytorch中有几种方法，这里先来总结一下：

- **Tensor.requires_grad**

  这个属性非常重要，在模型**训练**时，`requires_grad_()`函数会改变`Tensor`的`requires_grad`属性并返回`Tensor`，其默认参数为`requires_grad=True`。`requires_grad=True`时，自动求导会记录对`Tensor`的操作，`requires_grad_()`的主要用途是告诉自动求导开始记录对`Tensor`的操作。故只要把该参数设置成False即可冻结。 

  ```python
  if self.freeze_weights:
      m.weight.requires_grad = False
      m.bias.requires_grad = False
  ```

- **with torch.no_grad()**

  在该语句块内的代码都会禁止梯度的计算，加快计算速度，一般用于`Inference`阶段，可以减少计算内存的使用量。

  ```python
  model = HRNet()
  with torch.no_grad():
      ootput = model(input) # 不会改变模型参数
  ```

  

- **detach()**

  detach()函数会函数会返回一个新的Tensor对象`b`，并且新`Tensor`是与当前的计算图分离的，其`requires_grad`属性为`False`，反向传播时不会计算其梯度。`b`与`a`共享数据的存储空间，二者指向同一块内存。

  该函数一般用于**中间需要打印张量**结果，或者是保存图片,使用时应如下：

  ```python
  img = images[i].cpu().detach().numpy()*255
  ```

- **model.eval()**

  训练完train_datasets之后，model要来测试样本了。在model(test_datasets)之前，需要加上**model.eval()**. 否则的话，有输入数据，即使不训练，它也会改变权值。这是model中含有`batch normalization`层所带来的的性质。该参数冻结需要依靠`eval()函数`，即在`Inference`时，

  ```python
  model = HRNet()
  model.eval() 
  with torch.no_grad:
      output = model(input) # 如果有BN层，此时不会改变模型参数
  ```

  保险起见，在**推理**时都需要加上`model.eval()`

- **grad_fn**

   表示积分的方法名

---

### 第二次更新 只冻结 Backbone

在 Backbone 层含有 BatchNorm 时，只冻结参数是不可行的，还需要把 BatchNorm 层进行冻结。*BN 层不靠梯度更新，而是根据当前的动量更新，所以冻结 BN 需要在每一次前向传播用到 backbone 时，把对应的层设置成 eval()*.

```python

def _freeze_bn(self,m):  
    classname = m.__class__.__name__  
    if classname.find('BatchNorm') != -1:  
        m.eval()

def freeze_weight(self):  
    for module in self.modules():  
        parameters = module.parameters()  
        for parameter in parameters:  
            parameter.requires_grad = False

if self.freeze_hrnet_weight:  
    self.hrnet.freeze_weight()  # 进行参数冻结

def forward(self, kf_x, sup_x, **kwargs):
	x = torch.cat([kf_x, sup_x], dim=0)  
	self.hrnet.apply(self._freeze_bn)  # 进行 BN 冻结 
	x_bb_hm, x_bb_feat = self.hrnet(x, multi_scale=True)

```