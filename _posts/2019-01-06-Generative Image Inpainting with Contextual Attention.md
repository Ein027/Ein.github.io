# Generative Image Inpainting with Contextual Attention

2018 CVPR Adobe 也搞事了

明确地利用周围的图像特征作为参考，从而做出更好的预测。

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106195000.png)



思路：包括了两个阶段，第一个阶段利用简单的空洞卷积网络，粗略地预测缺失内容。第二阶段利用上下文注意力模块，使用未缺失区域patch的特征来处理生成的区域。



补全网络的基础是Globally and locally，并加入空洞卷积扩大感受野，以前使用DCGAN，现在使用更先进的WGAN-GP loss 。

文章中还提出，我们把原图作为gt，但“合理的”补全可能和原图相差很远，这样会误导网络训练，直观地，孔边界附近的缺失像素比孔洞中心的具有无关紧要的概率。 这类似于强化学习中观察到的问题。 当长期奖励在采样过程中有很大的变化时，人们会使用时间折扣奖励而不是采样轨迹（不懂）。受此启发，作者使用权重掩模M引入空间折扣（spatially discounted）的重建损失。掩模中每个像素的权重计算为γ^l，其中 l 是像素与最近的已知像素的距离。 在所有实验中γ设定为0.99。其余的还是L1 Loss。



**上下文注意力：**

上下文关注层学习从已知背景补丁借用或复制特征信息的位置以生成缺失补丁。使用预选相似度计算分数

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190109155606.png)

f是前景特征，b是背景特征，做成卷积形式，可生成分数map：

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190109113159.png)



attention 传播

我们通过传播（融合）进一步鼓励注意力的一致性。 一致性的想法是前景补丁的移位可能对应于背景补丁中的相同移位以引起注意。 例如，s * x，y，x0，y0和s * x + 1，y，x0 + 1，y0通常具有接近的值。 为了模拟和鼓励注意力图的一致性，我们进行左右传播，然后进行自上而下的传播，内核大小为k。 以左右传播为例，我们得到了新的注意力得分：

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190109161507.png)