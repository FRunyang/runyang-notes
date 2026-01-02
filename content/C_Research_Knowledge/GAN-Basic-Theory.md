---
title: GAN2_Basic_Theory
date: 2020-02-28 21:35:21
tags:
  - GAN
cover: https://user-images.githubusercontent.com/60562661/75565304-ad6ee700-5a88-11ea-8e26-3ba4df5b25bb.jpeg
---
*GAN系列知识
[[GAN对抗网络初识]]
[[GAN-Basic-Theory]]
[[手动实现GAN网络生成动漫头像]]
[[GAN-4-f-GAN推导]]

这篇文章主要来讨论下GAN基础的理论、公式推导。

## KL 散度

`KL Divergence` 指的是相对熵，其用来衡量两个取值为正的函数或概率分布之间的差异；

`相对熵 = 某个策略的交叉熵 - 信息熵（根据系统真实分布计算而得的信息熵，为最优策略）`  ,  公式如下:
$$
KL(P || Q) = H(P,Q) - H(P) = \sum_{k=1}^N P_k*log_2\frac {1} {Q_k} - \sum_{k=1}^N P_k*log_2\frac {1} {P_k} = \sum_{k=1}^N P_k*log_2\frac {P_k} {Q_k}
$$
复习一下，交叉熵是使用非真实分布，信息熵是使用真实分布计算得到的。

## JS 散度

`JS Divergence`  是 KL散度的变体，衡量两个分布之间的相似性。公式如下：
$$
JS(P||Q) = \frac 1 2 KL(P||\frac{P+Q}{2}) + \frac 1 2 KL(Q||\frac{P+Q}{2})
$$

## Formula Of GAN

首先，生成器要做的事情就是生成一个最靠近真实data的分布，这在之前可以用最大似然估计来找这样的一个分布，最大似然估计实际上可以与KL散度扯上关系：

<img src="https://user-images.githubusercontent.com/60562661/75565315-af38aa80-5a88-11ea-9673-fcc477934c05.png" alt="1582900061983" style="zoom:80%;" />

这里面需要注意的是**约等于** 这一步，意思是最大值求和m笔data的概率其实就是求x服从于真实分布的情况下概率的最大值，所以就 = 下面的积分，而下面的积分后边减去的一项不影响求最大值，所以再意思上是相等的，但是真实值上并不相等。然后上面的公式主要是来说明：

`最大化最大似然估计概率就是最小化KL散度`，即：
$$
G^* = arg\underset G min Div(P_G,P_{data})
$$
所以要训练**Generator**，也就是要计算出真实数据和生成数据之间的散度，而**Discriminator**则可以做到这一件事。

在训练Discriminator时，在固定住Generator的情况下进行，定义对象方程：

![1582901609500](https://user-images.githubusercontent.com/60562661/75565318-afd14100-5a88-11ea-8c7f-a035df1a9034.png)

这里后面一项之所以要定义为1-D(x),是因为判别器做的事情是给Pdata高分，给Pg低分，也就是使得生成的数据和真实的数据分布的散度最大。因此在x服从Pg分布时，写1-D(x) 就可以最大化这个式子，比较容易train，即：
$$
D^* = arg\underset D max V(D,G)
$$
实际上，当生成的图像和真实图像散度比较大，相似度比较小时，判别器是很好训练的，而相似度比较大就比较难训练，所以训练好的判别器其实就是在最大化生成的图像和真实图像的散度。下面证明这一项就是在最大化JS 散度：

<img src="https://user-images.githubusercontent.com/60562661/75565319-b069d780-5a88-11ea-8f2a-a9497fe42922.png" alt="1582902722545" style="zoom: 40%;" />

<img src="https://user-images.githubusercontent.com/60562661/75565323-b19b0480-5a88-11ea-9fe5-14395438c926.png" alt="1582902806605" style="zoom: 90%;" />

<img src="https://user-images.githubusercontent.com/60562661/75565327-b2cc3180-5a88-11ea-993a-4992d7b378dd.png" alt="1582902903882" style="zoom:90%;" />

<img src="https://user-images.githubusercontent.com/60562661/75565330-b364c800-5a88-11ea-92e3-38aadf080966.png" alt="1582902953241" style="zoom:90%;" />

这里最后一步可以参考一开始文章提到的JS散度对比一下公式就会明白。所以此时：
$$
G^* = arg\underset G min (\space \underset D maxV(D,G))
$$
此时梯度下降法求解G*:

<img src="https://user-images.githubusercontent.com/60562661/75565333-b495f500-5a88-11ea-83a5-f46a4ee2b53b.png" alt="1582904545756" style="zoom: 90%;" />

这里的max取微分可以看作分段函数求微分。所以现在已经可以铜鼓哦梯度下降法来更新生成器了，然后进行算法：

![1582905215369](https://user-images.githubusercontent.com/60562661/75565339-b52e8b80-5a88-11ea-8b7c-9caa8bed1e9e.png)

**这里有一个问题，事实上更新G1参数真的是在减小JS散度吗？**

![1582905319178](https://user-images.githubusercontent.com/60562661/75565340-b65fb880-5a88-11ea-8dcd-a5366afdb4bb.png)

举个例子如上图，在G更新后，G的分布已经变了(由左到右)，此时的D0*依然是固定的未发生变化，因此此时的D0\*已经不再是max值了，因此此时`（伪）max V(G,D)`  便不再是JS散度了。所以有个假设，G的变化不能太大，每次更新一点点，否则误差会过大。

**以是就是GAN的基础理论公式推导。**

## Practice

![1582905751928](https://user-images.githubusercontent.com/60562661/75565341-b6f84f00-5a88-11ea-935e-af64fc9f2ab8.png)

最后整体回顾一遍算法流程：

![1582905847010](https://user-images.githubusercontent.com/60562661/75565342-b8297c00-5a88-11ea-8dd5-6d115ff21f5a.png)

**注意的是一般Generator只训练一次 **。原因前面说了 。



以上就是GAN 对抗网络的 Basic Theory，还有其他的一些之后的细节可以看李宏毅老师的视频。有错误欢迎指正！

