# Python 使用记录（cv2、numpy、plt）

最为一名CVer，python-opencv当然经常使用，但没人去系统地学习它（性价比低），虽然很简单，但每次使用都是“问题+google”，重复查询时间还挺多的，为了减少无用开发时间，一些常用的但总记不住的api，一些被我踩过坑，记录在此，长期更新。

# OPENCV

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







# NUMPY

#### np.astype(np.int32)

强制类型转换。某次我想求两幅图像的差值，但cv2 读入的类型是 ndarray ( numpy 矩阵 )，默认数据类型 dtype 是 uint8 ( 无符号整形 )，数据范围0~255，相减后的数据类型不变，无法表示附属，自然不正确。在相减前必须进行类型强制转换，一般转为 int32。

```python
img = cv2.imread('img/'+'1.bmp', 0)	#ndarray uint8
img_inpaint=cv2.imread('img/'+'1_Inpainted image.png', 0) #ndarray uint8
img_arr=img.astype(np.int32) #ndarray int32
img_inpaint_arr = img_inpaint.astype(np.int32) #ndarray int32

diff=abs(img-img_inpaint)
diff_arr=abs(img_arr-img_inpaint_arr)
```







# MATPLOTLIB

#### 热力图显示

```python
from matplotlib import pyplot as plt

cmap = plt.get_cmap('jet')
rgba_img = cmap(abs(img_arr-img_inpaint_arr)) #需要显示的图片
rgb_img = np.delete(rgba_img, 3, 2)
rgb_img = np.asarray(rgb_img * 255.0, dtype=np.uint8)
destRGB = cv2.cvtColor(rgb_img, cv2.COLOR_RGB2BGR)
plt.imshow(rgb_img)
plt.show()
```

效果：

![](https://raw.githubusercontent.com/Ein027/Blog-Img/master/img/TIM%E6%88%AA%E5%9B%BE20181205131553.png)