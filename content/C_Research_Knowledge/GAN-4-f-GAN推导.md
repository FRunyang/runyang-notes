---
date: 2020-03-15 15:43:53
tags:
  - GAN
cover: https://user-images.githubusercontent.com/60562661/76704185-16559080-6712-11ea-8f17-d1a3824e8351.jpg
---
*GAN系列知识
[[GAN对抗网络初识]]
[[GAN-Basic-Theory]]
[[手动实现GAN网络生成动漫头像]]
[[GAN-4-f-GAN推导]]

## 为什么要引入f-GAN？
之前谈到GAN基础理论，可以知道GAN的生成器其实就是在最小化 **P_data** 和 **P_G** 的 JS散度。而事实上不一定要用`JS-Divergence` 来测量，**KL-Divergence、JS-Divergence**等都是属于**f-Divergence**，故f-GAN其实就是想要换掉GAN中的分布之间的距离测度函数。



## f-Divergence

$$
D_f(P||Q) = \int_x q(x)*f(\frac{p(x)}{q(x)})dx
$$
其中，f是`convex凸函数`, f(1) = 0，故：
![](https://user-images.githubusercontent.com/60562661/76704169-fb831c00-6711-11ea-94ea-6a4b4879e385.png)

其中`>=`用到了詹森不等式.

- 若p(x),q(x)相等，则值为0；
- 若其不相等，则**Df>=0**  因此 Df可以用来测量分布之间的距离

<img src="https://user-images.githubusercontent.com/60562661/76704155-ee662d00-6711-11ea-8e2e-17e4da092990.png" alt="1584260831145" style="zoom:67%;" />

此时f(x)取不同的表达式，得到不同的散度。



## 共轭函数

<img src="https://user-images.githubusercontent.com/60562661/76704159-f1f9b400-6711-11ea-9639-528670025d24.png" alt="1584260962776" style="zoom: 80%;" />

每一个凸函数`f`都有一个共轭函数`f*`

对于函数f(x),

- 首先t取t1，x取遍定义域内所有的值x1...xn,找出最大的$f^*(t1) = x_1t_1-f(x)$
- 对于每一个t都用相同的方法计算，就可以知道最终的f*

这样计算太麻烦，于是：

![1584261338486](https://user-images.githubusercontent.com/60562661/76704161-f32ae100-6711-11ea-8892-daa86908a963.png)

如上图，画出所有的函数图像，取得图像上界即可。

![1584280774347](https://user-images.githubusercontent.com/60562661/76704163-f4f4a480-6711-11ea-840f-774ec211ec48.png)

当$f(x) = x\log(x)$时，求的其共轭函数为：$f^*(t) = exp(t-1)$



## Connection with GAN

![1584281621663](https://user-images.githubusercontent.com/60562661/76704164-f58d3b00-6711-11ea-9e3f-aa670f1f3445.png)

这块的逻辑是这样：

- 首先 f(x) 于 f* 互为共轭函数，故可以有第一行的公式，然后把它代入D中，得到上图中得第三行的公式，目前问题变为：找一个t，使得这个积分项最大；
- 直接找t不好找，所以训练一个判别器D，输入是x，输出是t，D(x) = t,便得到上图下部分得公式，所以问题又转化为寻找一个D，可以最大两个积分项做减法得值
- 简单来说，就是把寻找t变为寻找D(x)

![1584282526678](https://user-images.githubusercontent.com/60562661/76704165-f756fe80-6711-11ea-8701-537bbba1819e.png)

这里就很顺理成章了，P_data 和 P_G 之间的f-divergence就可以求出来了;**而D(x)、f*()取不同的表达式 ，得到的就是不同的f-divergence。**

对于生成器来说，就是最小化真实数据和生成数据之间的`f-divergence`

![1584284110315](https://user-images.githubusercontent.com/60562661/76704167-f9b95880-6711-11ea-9b66-0b6a6fb6e0ca.png)

其中，Generator f(u) 就是上面公式中的D(x)表达式；f*(t)就是上面公式的 f\*.

以上就是f-GAN得数学推导过程。

