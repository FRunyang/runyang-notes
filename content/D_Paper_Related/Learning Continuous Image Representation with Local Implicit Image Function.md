[Learning Continuous Image Representation with Local Implicit Image Function](https://yinboc.github.io/liif)

> 学习连续的图像表征方法，根据图片坐标及周围的特征预测RGB值

- 因为连续，可以做任意分辨率超分
- 隐式函数表示本质是用NN学习坐标到相应的信号的映射

The key idea of implicit neural representation is to represent an object as a function that maps coordinates to the corresponding signal (e.g. signed distance to a 3D object surface, RGB value in an image), where the function is parameterized by a deep neural network.