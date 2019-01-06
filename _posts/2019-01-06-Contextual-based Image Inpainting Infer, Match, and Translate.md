# Contextual-based Image Inpainting: Infer, Match, and Translate

2018 ECCV

inpainting + 风格迁移

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106204233.png)

思路：分为推断和迁移，和之前那篇不同的是，将refinement问题作为学习问题。

定义了一个“patch-swap”层，来传递高频的纹理信息：使用外部与待替换patch最相似的 特征来替换。

补全用的Loss介绍过很多次了，是perceptual+ad loss。

Match部分：使用3*3的patch，在feature map上，计算他们的相似度。

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106203950.png)

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106203255.png)

这个操作可以用卷积并行完成。

Loss：perceptual + ad 训练中使用gt作为输入来训练第二阶段会好很多。

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106204325.png)

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106204331.png)

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20190106204338.png)









