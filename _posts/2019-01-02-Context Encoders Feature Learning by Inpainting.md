# Context Encoders: Feature Learning by Inpainting

2016 CVPR

在深度学习-图像补全领域最经典的文章，后面很多文章都是基于它改进的。

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190102144403.png)

思想：卷积自编码，输入带miss区域的图像，输出补全后的图。

细节：channel-wise的全连接，用于获取全局信息。

损失函数：两部分组成，一是回归损失，一是对抗损失。如果没有对抗损失，会少很多高频信息，这个对抗损失在后来的一些文章中也逐渐成为标配。

从共识中可以看到，都使用 mask M 来仅仅需要关注缺失区域的损失。也和上图对应了。

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190102152805.png)

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190102152835.png)

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190102153924.png)





文中也对比了有/无 对抗损失，很直观。

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190102154132.png)

作者website: https://people.eecs.berkeley.edu/~pathak/context_encoder/

code github: https://github.com/pathak22/context-encoder



