# StockingShader
ClothShader/Stocking
# 现实中的丝袜效果
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191017221403832.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTE1NDQ3,size_16,color_FFFFFF,t_70)
主要材质为 约90%聚酰胺纤维（锦纶/尼龙）+ 约10%聚氨酯纤维（氨纶） 
基本上可以推测这种材质的金属性(Metallic)为0，而光滑度(Smoothness)则根据种类不同会有较大区别。

# 丹尼尔值
各种丝袜的厚薄也有区别，“D”或“Denier”是指纤维的纤度单位。5D、10D几乎透明，100D以上则几乎不透，很好理解，请看下图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191017221500276.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTE1NDQ3,size_16,color_FFFFFF,t_70)
在Shader里我们采用Denier值来表示丝袜的厚薄程度。

# 纤维的特性
我们可以发现一种现象——靠近腿部中央的位置丝袜颜色较淡，并且如果丝袜够薄甚至会显出底下皮肤的颜色，而越靠近腿两侧丝袜颜色则会越深。丝袜由无数细小交错的纤维组成，所以正对视线的纤维是最稀疏的，而越靠近腿部轮廓的纤维则对于观察者来说越显得密集。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019101722163971.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTE1NDQ3,size_16,color_FFFFFF,t_70)
# 分析
基于PBR，对丝袜纤维的密集程度定义一个属性 疏密度(Density) ，取值范围0（几乎没有纤维）到 1（完全被纤维覆盖）。依据疏密度提供颜色给Albedo通道，疏密度越高显现更多丝袜颜色，越低则显现皮肤颜色。

计算疏密度需要三部步骤：
1.丹尼尔值对整体疏密度的影响。
2.受丝袜良好弹性影响，需要一张灰度贴图来控制不同区域的拉伸程度，拉伸越大疏密度越低。
3.受观察者视线的影响，丝袜平面与观察者视线角度越小时，疏密度越大。称其为边缘度影响。

## 效果截图：
### Weak：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019101722251576.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTE1NDQ3,size_16,color_FFFFFF,t_70)
### Normal：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191017222748390.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTE1NDQ3,size_16,color_FFFFFF,t_70)
### Strong：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191017222541831.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTE1NDQ3,size_16,color_FFFFFF,t_70)
