# Globally and Locally Consistent Image Completion

SIGGRAPH 2017

思想：不仅用一个全局判断，也用一个 local 的判别器来判别生成的质量。

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190104162445.png)

细节：将mask作为一个 channel 作为输入，输出补全好的图像。

全局判别：为了增大感受野，采用了空洞卷积。下图解释了why。

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190104173433.png)

局部判别：输入被补好的区域，判断为假的，在孔周围采样与孔不重叠的patch作为真的。

训练：训练阶段总是只有一个孔，在孔的周围采一个patch用作局部判别。

损失函数：

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190104190115.png)



![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190104190122.png)

其中，Md是随机patch，Mc是缺失区域。

注，该文章可处理随即形状的mask。

code: https://github.com/tadax/glcic