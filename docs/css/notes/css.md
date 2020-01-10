



# CSS基础

## 选择器

## 盒模型

### 外边距

`margin：0 auto`可以设置对象上下外边距为0，左右自动居中。

#### 不能自动居中的原因

1.  如果外层 `DIV` 设置了 `float` 值，就不能居中布局了。
2. 低版本的浏览器和高版本的浏览器需要加入`text-align:center`进行兼容
3. 没有给需要居中的盒子指定宽度。
4. 设置了元素 `display:block` 以外的元素值。

### box-sizing

`box-sizing`  的属性值定义了浏览器将如何定义元素的宽高

| 选项        | 说明                                                      |
| ----------- | --------------------------------------------------------- |
| border-box  | 告诉浏览器，设置的内边距和边框的宽度是包含在`width`内的。 |
| content-box | (默认值) 边框和内边距的宽度会被增加到最后的宽度绘制中。   |

### margin撑满盒子

常见的导航条布局中，通常是左右布局，中间空白。那么简单做法就可以使用 `margin`  撑满中间的距离

```
margin-right: auto;
```



## 背景处理

### 背景样式

#### 背景剪裁

`background-clip ` 设置元素的背景是否延伸到边框下面

| 选项        | 说明                                   |
| ----------- | -------------------------------------- |
| border-box  | 背景延伸至边框下面                     |
| padding-box | 背景延伸至内边距外延，不会绘制到边框处 |
| content-box | 背景剪裁至内容区外沿                   |



## 浮动布局

### 浮动布局

通过设置 `float` 值指定元素像什么方向浮动，浮动后的元素都会变成块级元素。

```css
div:nth-of-type(1) {
	float: left   //元素相左浮动
}
div:nth-of-type(2) {
    float: right  //元素向右浮动
}
div:nth-of-type(3){
    float: none   //元素不浮动
}
```

### clear 清除浮动

元素浮动后将不占据原有的空间，会导致下层没有浮动的盒子上移，如果希望消除这种影响，可以清除浮动。

```
div:nth-of-type(2){
	clear: left;  //清除左边浮动
}
div:nth-of-type(3){
	clear: rigth  // 清除右边浮动
}
div:nth-of-type(1){
	clear: both   //清除两侧浮动
}
```



### 伪元素清除浮动

通过在元素内容的后面添加内容，来清除浮动。

```css
div::after {
	content: "";
    clear: both;
    display: block;
}
```

## 弹性布局

### dispaly 定义

通过 `display` 控制元素的显示类型，这里包含两种基础特征，**外部显示类型**定义了元素怎样参与流式布局的处理，**内部显示类型**定义了元素内子元素的布局方式。

| 外部显示类型 | 内部显示类型 |
| :----------: | :----------: |
| inline-block |     flow     |
|    block     |     flex     |
|    inline    |     grid     |
|              |    table     |
|              |     ruby     |

### 了解弹性盒子

#### display属性值

声明弹性盒子可以设置 `display:flex  ` 或者 ` display: inline-flex`。

区别在于： `inline-flex`  设置的弹性盒子是一个**内联级**弹性盒子。

​					`flex`  设置的弹性盒子是一个**块级**弹性盒子。

### 使用弹性盒子

#### 元素方向

`flex-direction`  ： 控制盒子内元素的排列方向

| 属性           | 说明                    |
| -------------- | ----------------------- |
| row            | (默认) 从左向右水平排列 |
| row-reverse    | 从右向左排列            |
| column         | 从上到下垂直排列        |
| column-reverse | 从下到上垂直排列        |

#### 溢出换行

`flex-wrap`  控制元素在溢出时是否换行，属性值控制元素是从什么方向开始换行

| 属性         | 说明                                       |
| ------------ | ------------------------------------------ |
| wrap         | 根据 `flex-direction` 值的方向开始换行     |
| wrap-reverse | 根据 `flex-direction` 值的方向开始反向换行 |
| nowrap       | (默认值) 不换行                            |

该属性值产生的效果受元素排列方向的影响，因此是与上一个元素结合使用。

#### flex-flow

该属性是 `flex-direction` 和 `flex-wrap` 的简写形式。

语法：　

```css
flex-flow: <flex-direction> || <flex-wrap>
```

#### 关于轴

元素溢出换行后，就出现了主轴和交叉轴，不同的排列和换行，轴的方向也不相同。

**水平排列**： 

```css
flex-flow: row wrap;
```

<img src="C:\Users\Admin\Desktop\biji\1.png" alt="1" style="zoom:80%" />

```
flex-flow: row-reverse wrap-reverse
```

<img src="C:\Users\Admin\Desktop\biji\2.png" alt="2" style="zoom:80%;" />



#### 主轴排列方式

`justify-content`  决定浏览器如何分配主轴方向的元素及其剩余空间。

**元素水平分布，从主轴开始的方向排列**

```css
flex-flow: row wrap;
justify-content: flex-start;
```

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20191230173915293.png" alt="image-20191230173915293" style="zoom:80%;" />

​	

**元素水平分布，从主轴结束的方向排列**

```css
flex-flow: row wrap;
justify-content: flex-end;
```

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20191230172647147.png" alt="image-20191230172647147" style="zoom:67%;" />

**元素水平分布，居中排列**

```css
flex-flow: row wrap;
justify-content: center;
```

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20191230174051568.png" alt="image-20191230174051568" style="zoom:80%;" />

**元素水平分布，两端对齐排列**

```css
flex-flow: row wrap;
justify-content: space-between;
```

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20191230174307338.png" alt="image-20191230174307338" style="zoom:80%;" />

**元素水平分布，周边距离相同**

```css
flex-flow: row wrap;
justify-content: space-around;
```

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20191230174637642.png" alt="image-20191230174637642" style="zoom:80%;" />

**元素水平分布，元素之间的间隔相同**

```
flex-flow: row wrap;
justify-content: space-evenly;
```

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20191230174831649.png" alt="image-20191230174831649" style="zoom:80%;" />

#### 交叉轴对齐方式

`align-items`  决定浏览器如何分配元素在交叉轴上的位置

**元素垂直分布，从交叉轴结束位置排列**

```css
flex-flow: column;
align-items: flex-end;
```

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20191230175942369.png" alt="image-20191230175942369" style="zoom:80%;" />

**元素垂直分布，居中排列**

```css
flex-flow: column;
justify-content: center;
align-items: center;
```

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20191230180151917.png" alt="image-20191230180151917" style="zoom:80%;" />

#### 多行排列时交叉轴对齐方式

**元素较多导致溢出换行时交叉轴的排列方式**

**元素周围距离相同分布排列**

```css
flex-flow: row wrap;  //元素水平排列
align-content: space-between;  //元素交叉轴分割距离相同分布
```

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20191230181321201.png" alt="image-20191230181321201" style="zoom:80%;" />

**元素周围间隔相同分布**

```css
flex-flow: row wrap;
align-content: space-evenly;
```

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20191230181711887.png" alt="image-20191230181711887" style="zoom:80%;" />

#### 单个元素的交叉轴控制

`align-self`  可以控制单个元素在交叉轴上的位置。

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20191231122509271.png" alt="image-20191231122509271" style="zoom:80%;" />

如果希望元素的宽高自适应的话，需要将元素本身的宽高去除。

```css
article div:nth-of-type(1){
    align-self: strerch;
	height: auto;
}
```

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20191231122826093.png" alt="image-20191231122826093" style="zoom:80%;" />

#### 元素可用空间分配

`flex-grow`  可以在元素内容没有撑满弹性容器时，对剩余空间进行分配。

```
div:nth-of-type(1){
	flex-grow: 0;   //不参与剩余空间分配，保持不变
}
div:nth-of-type(2){
	flex-grow: 1;   //将剩余空间分成了4份，这里占一份
}
div:nth-of-type(3){
	flex-grow: 3;    //将剩余空间分成了4份，这里占3份
}
```

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20191231124217838.png" alt="image-20191231124217838" style="zoom:80%;" />

#### 元素收缩

当元素的宽度超出弹性盒子的宽度时，通过设置 `flex-shrink` 控制元素的收缩规则。

计算公式如下：

```
缩小比例： 不足的空间 / ( 元素1宽度 * 缩小比例 + 元素2宽度 *　缩小比例 + ... )
最终尺寸： 元素2宽度 - ( 缩小比例 * 元素2的宽度 ) * 元素宽度
```

![image-20191231143232569](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20191231143232569.png)

#### flex

`flex`  是 `flex-grow` 、 `flex-shrink` 以及 `flex-basis` 的缩写组合。

`flex-basis`  是基础尺寸，优先级是 `flex-basis`  >  `width/height`  。

```css
flex: 1 0 50px;  // 表示平均分配剩余空间，不缩放尺寸，基础尺寸为200
```

![image-20191231150055739](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20191231150055739.png)

## 栅格系统

### 栅格介绍

#### 名词解释

`css`网格布局是`CSS`中最强大的布局方式，是一个二维系统，这就意味着它可以同时处理行和列。

与`flex`布局是有相似之处的，都是由父容器包裹多个元素进行使用。

但为什么不火的原因也很明显，兼容性不好。对设备的要求比较高。

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20200102155301406.png" alt="image-20200102155301406" />





### 声明容器

通过设置 `display: grid`  将容器变为栅格容器，接下来就可以愉快的绘制栅格啦~

### 绘制行列

栅格类似于表格，也是按照行和列进行划分，  `grid-template-columns` 可以绘制列，  `grid-template-row` 可以绘制行。

```css
article {
	display: grid;
    grid-template-columns: 50% 50%;
    grid-template-row:　33% 33% 33%;
}
article div {
	background-color:　palevioletred;
    padding: 10px;
    background-clip: content-box;
}
```

![image-20200102162512527](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20200102162512527.png)

绘制行和列有多种方式，当我们绘制的行或者列中的每个元素都是相同尺寸的时候，可以使用简洁的写法

```css
article {
    display: grid;
    grid-template-row: repeat(2, 100px 50px);
    grid-template-columns: repeat(3, 20%);
}
```



![image-20200103141054222](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20200103141054222.png)

上方代码可以很明显看出，`repeat`  的值可以是两种形式。第一个参数是重复的数量，第二个参数是重复值。

1.  重复值可以是具体的数值，以行为例，表示第一行是100px，第二行是50px。
2.  重复值可以是百分比，就是按照外层容器大小进行等比例划分。

### 自动填充

计算每个元素的大小也是一件很繁琐的事情，因此我们可以进行比例划分，是元素自动填充整个容器，这里用到的单位是  `fr`，是一个自适应单位。

```css
article{
    display: grid;
    grid-template-rows:1fr 3fr 1fr;
    gird-template-columns: 1fr 3fr 1fr;
}
```



<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20200103142951587.png" alt="image-20200103142951587"  />

这种自适应尺寸的好处就在于无论容器的大小怎么改变，都可以进行等比例缩放。

### 控制尺寸波动范围

行和列尺寸有多种绘制方式，还可以通过  `minmax`  控制元素的波动范围。

```css
article {
	display: grid;
    grid-template-columns: repeate(5, 1fr);
    grid-template-rows: repeat(2, minmax(50px,100px))   // 表示元素尺寸的波动范围在50-100px之间
}
```

![image-20200103152300179](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20200103152300179.png)



当容器的高度为`200px`时，元素的尺寸为`100px`。

![image-20200103152403435](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20200103152403435.png)

当容器的高度为 `100px`时，元素的尺寸为 `50px`。也是一种根据容器大小自适应尺寸的方式，只是规定了最大最小值。

### 根据栅格线编号放置元素

根据设置具体的栅格线设置放置元素的具体位置，设置的数值可以是正数也可以是负数。

元素定位方式：

```css
div:first-child {
    grid-row-start:1;   //行开始
    grid-column-start:1;  // 列开始
    grid-row-end: 2;   // 行结束
    grid-column-end: 2;   // 列结束
}
```

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20200106104145284.png" alt="image-20200106104145284" style="zoom:80%;" />

### 利用栅格绘制不规则元素布局

栅格绘制出来的形状只能是矩形，因此如果想要绘制不规则的元素布局，可以通过设置元素位置来完成。

```css
article {
	width: 200px;
    height: 200px;
    display: grid;
}
article div {
	background-color: tomato;
    color: #fff;
    padding: 10px;
    background-clip: content-box;
    grid-template-rows: repeat(2,1fr);
    grid-template-columns: repeat(2,1fr)
}
article div:first-child {
	grid-row-start: 1;
    grid-column-end: 3;
    grid-row-start: 1;
    grid-column-end: 3;
}
```

![image-20200106110502169](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20200106110502169.png)

### 栅格固定命名放置元素







## 变形透视动画

### 坐标系统

首先需要清楚元素变形的轨迹，也就是坐标轴。通过改变坐标位置来实现变形。

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20200106165043886.png" alt="image-20200106165043886" style="zoom:80%;" />



- 这里的 X 轴就是水平方向上的坐标轴
- Y 轴就是垂直方向上的坐标轴
- Z 轴是纵深轴，简单来说就是你看向电脑屏幕的轨迹。

### 变形操作

使用  `transform` 规则可以控制元素的移动、旋转、变形、倾斜、3D转换等。

#### 移动

```css
div {
    height: 100px;
    width:100px;
    position: absolute;
    left: 50%;
    top: 50%;
    margin-left: -50px;
    margin-top: -50px;
}
div:nth-child(1) {
	background-color: darkkhaki;
    transition: 1s;    //变形速度1s
}
div:nth-child(2) {
    background-color: indianred;
}

main:hover div:nth-child(1) {
    transform: translateX(100px);   // 在X轴上向左移动 100px。
}
```

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20200106170833601.png" alt="image-20200106170833601" style="zoom:80%;" />

<img src="C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20200106170806764.png" alt="image-20200106170806764" style="zoom:80%;" />

- 以 X、Y 轴上移动时，数值都可以使用百分数来表示，比如 100% 就是表示移动当前整个盒子的距离。

- 在 Z 轴上移动时，不可以使用百分数，因为纵深没有具体的数值比例作为参考。

|     值     | 说明                                                         |
| :--------: | :----------------------------------------------------------- |
| translateX | 在X轴移动，正数向右，负数向左                                |
| translateY | 在Y轴上移动，正数向上，负数向下                              |
| translateZ | 在Z轴上移动，正数向前，负数向后                              |
| translate  | 可以有两个值，第一个值代表在 X 轴上移动，第二个值代表在 Y 轴上移动 |

接下来再体验下在 Z 轴上移动的效果，可以理解为一个物体在我们的视线前方进行前后移动。

```css
div {
    height: 100px;
    width:100px;
    position: absolute;
    left: 50%;
    top: 50%;
    margin-left: -50px;
    margin-top: -50px;
}
div:nth-child(1) {
	background-color: darkkhaki;
    transform: perspective(900px);  //添加透视效果
}
div:nth-child(2) {
    background-color: indianred;
    transform: perspective(900px);
}

main:hover div:nth-child(1) {
    transform: perspective(900px) translateZ(200px)  //在Z轴上移动200像素
}
```

![image-20200109173632936](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20200109173632936.png)

![image-20200109173615774](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20200109173615774.png)

我们都知道远小近大的道理，因此视觉上就是div放大了的效果。

#### 3D移动

3D的效果更加立体，也即是有Z轴的参与。可以使用  `translate3d` 同时控制3个方向的移动。

`translate3d`  可以写入三个参数，分别是 X轴、Y轴、Z轴。其中需要注意，Z轴不可以用百分比表示。









### 控制元素居中的方式

有三种比较常用的居中方式，分别是： 

1. 使用  `flex`  布局实现居中
2. 使用  `position`定位实现居中
3. 使用  `transform`  移动实现居中

```css
// 第一种 flex
div {
	display: flex;
    justify-content: center;
    align-items: center;
}
```

```css
//第二种 position
div {
    position: absolute;
    left: 50%;
    top: 50%;
    margin-left: -100px;
    margin-top: -100px;
    height: 200px;
    width: 200px;
}
```

```css
// 第三种 transform
div {
	position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%)
}
```

第二种方法和第三种差不多，都是向左向下移动50%后，再移动自身的一半。

但第二种方法还需要后期计算，并且一旦改变了盒子的宽高，就需要重新计算修改。

第三种方式使用百分比的形式，直接移动自身的一半，更加自适应。























