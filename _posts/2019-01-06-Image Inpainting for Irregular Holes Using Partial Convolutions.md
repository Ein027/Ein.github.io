# Image Inpainting for Irregular Holes Using Partial Convolutions

2018 NVIDIA开始搞事了

现有的基于深度学习的图像修复方法在损坏的图像上使用标准卷积网络，在有效像素以及掩蔽孔中的替代值（通常是平均值）上使用卷积操作。这样是有问题的，通常会导致诸如颜色差异和模糊之类的伪影。

本文想提出已一种“部分卷积”，在没有后处理的情况下也能生成得很好。并且想解决“任意孔洞”的生成问题。

这篇文章没有放网络架构图，就是用的U-Net结构，跳转结构帮助重构细节。

创新点在于部分卷积。

**Partial Convolutional Layer**：

分为卷积和更新，两个步骤。

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106173637.png)

卷积如上，其中，**M**是对应的一个二值mask(和卷积核一个大小)，**1**是和**M**相同大小的全1矩阵。缩放因子sum（1）/ sum（M）应用适当的缩放以调整有效（未屏蔽）输入的变化量。

然后，在经过卷积后，需要更新M：如果卷积能够在至少一个有效输入值上调节其输出，那么我们将该位置标记为有效。

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106173643.png)

损失函数：pixel loss + perceptual loss + tv loss

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106194026.png)

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106194034.png)

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106194041.png)

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106194051.png)

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106194058.png)

