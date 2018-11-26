# CV2 Python 使用记录

最为一名CVer，python-opencv当然经常使用，但没人去系统地学习它（性价比低），虽然很简单，但每次使用都是“问题+google”，重复查询时间还挺多的，为了减少无用开发时间，一些常用的但总记不住的api，一些被我踩过坑，记录在此，长期更新。

#### cv2.imread()

- cv2.IMREAD_COLOR : 默认使用该种标识。加载一张彩色图片，忽视它的透明度。
- cv2.IMREAD_GRAYSCALE : 加载一张灰度图。
- cv2.IMREAD_UNCHANGED : 加载图像，包括它的Alpha通道。     友情链接：[Alpha通道的概念](https://baike.so.com/doc/6780023-6996190.html)

**可以简单的使用1，0，-1**代替。（必须是整数类型）。

```python
img = cv2.imread('messi5.jpg',0)
```



#### cv2.cvtColor()

openCV 的 cv2.imread() 导入图片时是BGR通道顺序，这与 Matplotlib 的显示，或者读取图片的通道不同，如果需要可以转换为 RGB 模式，以下代码显示不同之处，但 BGR 在许多地方使用，caffe倒入数据是以 BGR 方式(坑死我了，有一次用 tf 训练没有转换颜色空间，全是错的)

```python
srcBGR = cv2.imread("sample.png")
destRGB = cv2.cvtColor(srcBGR, cv2.COLOR_BGR2RGB)
```

