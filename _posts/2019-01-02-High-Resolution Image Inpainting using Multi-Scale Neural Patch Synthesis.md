# High-Resolution Image Inpainting using Multi-Scale Neural Patch Synthesis

Adobe Research 出品

思想：结构预测+风格迁移（解决高频生成问题）+多尺度（解决高分辨率问题）。

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190102164550.png)

在利用深度生成模型进行图像补全时，往往会存在生成“模糊”图像的问题，这一般是L2损失导致的，context encoders中使用对抗损失来解决这个问题，而在这篇文章中，作者在使用全局补全网络补全缺损区域后，再使用一个“风格迁移”网络，使被补区域和其余区域风格（纹理）相似。

损失函数由三部分组成，content，texture 和 TV loss。

Content Loss 就是很普通的L2损失，其中 h 是裁处区域 R 的操作。

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190102171431.png)

Texture Loss 是风格迁移中常见的loss，后面具体讲

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190102192731.png)

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190102192755.png)

TV loss:

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190102192802.png)



分为两个网络，Content Network 和 Context Encoders 差不多，但是输出的就是缺失部分（后者输出的和原图大小一样）。

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190102194159.png)

这个网络的损失函数也是L2+AD：

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190102200430.png)

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190102200435.png)



风格迁移损失：对于孔Rφ（提取的特征）中尺寸为s×s×c的每个局部查询块P，我们在孔外找到其最相似的块，并通过平均查询块与其最近邻居的距离来计算损耗。



多尺度迭代至高分辨率：

使用前一个尺度生成的图像作为第二个尺度的初始值。



实验：可见确实比context encoders好不少。

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190102215439.png)

