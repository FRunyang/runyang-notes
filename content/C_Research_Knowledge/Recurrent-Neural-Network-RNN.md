---
date: 2020-03-05 12:46:52
tags:
  - RNN
  - LSTM
cover: https://user-images.githubusercontent.com/60562661/75954993-f642f780-5eef-11ea-87a7-d80b32816d96.jpg
---

RNN,循环神经网络，一般用来处理序列化任务。例如一个句子就是一个词序列；一段视频就是一个图像序列；人讲一句话也是一个序列，处理序列就考虑到了时间维的信息。

## SIMPLE RNN

最简单的一个**RNN循环神经网络**就是存储了上一时刻的隐藏状态的值。简单的讨论一下RNN的设计结构。

<img src="https://user-images.githubusercontent.com/60562661/75954684-41103f80-5eef-11ea-9846-59ada03ace43.png" alt="1583384720030" style="zoom:80%;" />

假设只有一个隐藏层，有两个句子：

- leave **Taipei**
- arrive **Taipei**

如果采用一般的神经网络，见到**Taipei**这同一个词汇，输出的值都是相同的，与预期任务就不符合了。

首先leave作为第一时刻的输入，产生一个值；隐藏状态值是a1要存储起来，如上图的蓝色a1，然后下一时刻输入**Taipei**就同时收到`x2、a1` 的影响。后面的也同理，因此同一个输入就有不同的输出。

上面是一个简单的单向的RNN，还有双向的RNN，如下图：

<img src="https://user-images.githubusercontent.com/60562661/75954689-42da0300-5eef-11ea-8ffc-c46500154632.png" alt="1583385188547" style="zoom:67%;" />

训练一个正向的和一个反向的循环神经网络，然后把同一时刻(xt)两个网络的隐藏层拿出来同时计算该时刻的输出(yt).也就是说计算每一时刻的输出都要考虑到整个序列。



## Long Short-term Memory（LSTM）

上面的RNN是一个简单的循环神经网络的结构，它的记忆非常非常有限，只能记住前一个时刻的，这对我们来说仍然是不足的，因此需要记住更久的东西，就有了LSTM。（**注意名字，是多个短期记忆，一般叫长短期记忆网络，应该是很长的短期记忆网络，而不是长-短 期记忆网络。**）

LSTM网络结构如下：

<img src="https://user-images.githubusercontent.com/60562661/75954691-43729980-5eef-11ea-8dce-c0976f87aa09.png" alt="1583385772848" style="zoom:67%;" />

**它的核心在于中间蓝色部分的记忆细胞。**

它的计算过程观察上图，首先有 $z,z_i,z_f,z_o$ 四个gate，这四个门可以理解为四个控制信号，其中

- $z$ 表示的是要输入的信息的信号；
- $z_i$ 表示的是输入门的信号；
- $z_f$ 表示的是遗忘门的信号；
- $z_o$ 表示的是输出门的信号；

$$
Cell = \sigma(z) * \tanh(z_i) + c * \sigma(z_f)\\
Out = \tanh(Cell) * \sigma(z_o)
$$

其中， $z,z_i,z_f,z_o$的值就是输入$x_t$ 乘上四个矩阵得到的，整个流程如下图：

<img src="https://user-images.githubusercontent.com/60562661/75954692-44a3c680-5eef-11ea-9e4f-8663edfda312.png" alt="1583386846200" style="zoom: 80%;" />

细胞贯穿主线，xt的输入得到输出yt嘛，中间经过一系列的组合计算；**注意上图中z其实也是有激活函数的，z激活函数是tanh()**.

上图只是展示了LSTM计算过程，实际操作时会照以下操作（单个LSTM）：

<img src="https://user-images.githubusercontent.com/60562661/75954698-453c5d00-5eef-11ea-9b2f-872c5c166771.png" alt="1583387314831" style="zoom:78%;" />

会把前一时刻的输出值($h_{t-1}$)、记忆单元值($c_{t-1}$)、这一时刻的输入值 ($x_T$)堆在一起，一起再去计算，堆在一起就是torch中的级联：`torch.cat()`

在实际训练网络时单个LSTM肯定是不够的，所以需要计算多个的，此时：

<img src="https://user-images.githubusercontent.com/60562661/75954700-45d4f380-5eef-11ea-9a49-40ac10040c87.png" alt="1583387631495" style="zoom:90%;" />

横向的都是同一个LSTM，纵向的是堆起来的不同的LSTM模块。

**下面总结一下LSTM模块：**

![1583387847413](https://user-images.githubusercontent.com/60562661/75954701-47062080-5eef-11ea-9419-26acce47dc07.png)

这张图实际上前一时刻的细胞状态是没有和输入叠在一起的。以上就是整个LSTM架构，而它的几个变体都是大同小异。



## Why Lstm not Simple-RNN?

RNN基础模型一般不是很容易训练起来，面临梯度弥散、梯度爆炸的问题。

 <img src="https://user-images.githubusercontent.com/60562661/75954702-479eb700-5eef-11ea-9372-eca219db0d1c.png" alt="1583388071831" style="zoom: 80%;" />

如图，绿色的线条是实验的RNN的loss，它震荡不收敛。造成这个的原因在于**Error Surface is rough：**

<img src="https://user-images.githubusercontent.com/60562661/75954705-48374d80-5eef-11ea-9842-0f01ffaf2a53.png" alt="1583388245860" style="zoom:80%;" />**

如图，如果梯度下降法刚好更新到断层上，此时梯度骤升，学习率比较大就会飞出去很远，就直接没有了

<img src="https://user-images.githubusercontent.com/60562661/75954707-48cfe400-5eef-11ea-86fd-f8fe8c1ab044.png" alt="1583388353972" style="zoom:80%;" />

这就很直观的解释了原因，每次RNN都会用前一次的输出不加控制的影响下一个结果，也就是护送每次都hi把Memory的值完全变化掉。w是指数级就很容易有`Gradient Vanish(explore)` 的问题。

而LSTM，

- 它把Memory的值*一个值+input\*一个值更新到Cell中，也就是说它的Memory和input是相加的；

- 如果weight影响到记忆细胞的值，则一直会存在，除非遗忘门决定遗忘。而RNN则会一直洗掉。因此LSTM解决了梯度弥散问题。

- 一般遗忘门经常要开着，bias要比较大。



