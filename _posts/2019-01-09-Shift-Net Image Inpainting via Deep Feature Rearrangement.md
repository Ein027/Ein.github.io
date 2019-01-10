# Shift-Net: Image Inpainting via Deep Feature Rearrangement

思想：base on U-net结构，在解码器特征上引入了引导损耗，以最小化完全连接层之后的解码器特征与缺失部分的 gt 编码器特征之间的距离。利用这种约束，可以使用缺失区域中的解码器特征来指导已知区域中的编码器特征的移位。 

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190109205449.png)



引导损失 guidance loss :

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190109212106.png)

前者是encoder  后者是decoder 前后输入不一样

shift-connection layer :

使用Φl(I)和ΦL-l(I)给Φl(I gt)更新，

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190109224100.png)

