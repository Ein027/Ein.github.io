# SPG-Net: Segmentation Prediction and Guidance Network for Image Inpainting

2018 Baidu

现有的基于生成模型的方法没有利用分割信息来控制对象的形状，这通常会导致对边界的影响。

思路：语义分割+语义预测+语义辅助生成

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106151935.png)

分为 Segmentation Prediction Network (SP-Net) 和 Segmentation Guidance Network (SG-Net)，前者负责预测完整的语义图，后者负责补全图像。



**SP-net**:

输入 缺损图像+缺损图像的分割结果
输出 填补好的输出结果
损失函数：对抗损失+perceptual loss（重构损失）（只关注确实部分的）

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106160930.png)

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106161037.png)

perceptual loss常常用在风格迁移中https://blog.csdn.net/stdcoutzyx/article/details/54025243，在特征图上求重构残差，上面的公式就是将 gt 和 生成的图 G 都输入判别器D，在D提取特征后的两个特征图，相应的feature vector 残差F1范数的平均。



**SG-Net**：

输入：填充好的语义图和为填充好的原图。

输出：补全好的图。

损失函数也是对抗损失+perceptual loss（重构损失）（只关注确实部分的）

这里使用 alex 网络提特征并使用 L2 损失

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106162446.png)

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106162454.png)

