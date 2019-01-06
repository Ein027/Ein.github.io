# Generative Image Inpainting with Contextual Attention

2018 CVPR Adobe 也搞事了

明确地利用周围的图像特征作为参考，从而做出更好的预测。

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106195000.png)



思路：包括了两个阶段，第一个阶段利用简单的空洞卷积网络，粗略地预测缺失内容。第二阶段利用上下文注意力模块，使用未缺失区域patch的特征来处理生成的区域。





