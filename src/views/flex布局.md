# flex布局

## 一、flex布局是什么？

flex 是 flexible box的缩写，即弹性盒模型，顾名思义为盒模型提供更加弹性（灵活性）的布局方案。
> 盒模型： 所有 HTML 元素都可以视为一个盒子，该盒子包括：边距(margin)、边框(border)、填充(padding)和实际内容(content)
  
flex布局包含的元素通常用容器和项目来称呼，设置flex布局（display: flex）的元素称为flex**容器** (container)，容器内包含的子元素称为flex**项目**(item)。

## 二、flex布局属性

### 容器属性

* flex-direction
* flex-wrap
* flex-flow
* justify-content
* align-items
* align-content

### 项目属性

* flex-grow
* flex-shrink
* flex-basis
* flex
* align-self
* order

### 2.1 flex-direction 属性

  项目沿主轴方向排列，flex-direction 属性决定主轴的方向。
  > 容器有主轴和与主轴垂直的交叉轴，默认主轴是水平方向。（不要误以为主轴就是横轴）

  ``` css
    .box {
      flex-direction: row | row-reverse | column | column-reverse;
    }
  ```

* row (默认值)：水平方向，项目从左往右排列
* row-reverse：水平方向，项目从右往左排列
* column：垂直方向，项目从上往下排列
* column-reverse：垂直方向，项目从下往上排列

![Alt text](../../../../c:/Users/005/Desktop/%E8%B5%84%E6%96%99/img1.png)
![Alt text](../../../../c:/Users/005/Desktop/%E8%B5%84%E6%96%99/img2.jpg)  
![Alt text](../../../../c:/Users/005/Desktop/%E8%B5%84%E6%96%99/img3.jpg)
![Alt text](../../../../c:/Users/005/Desktop/%E8%B5%84%E6%96%99/img4.jpg)

### 2.2 flex-wrap 属性

  决定在主轴方向项目排列不下时是否换行，默认不换行。

  ``` css
    .box {
      flex-wrap: nowrap | wrap | wrap-reverse;
    }
  ```

* nowrap (默认值)：不换行
* wrap：换行，第一行在上面（主轴是水平方向，反之第一行是在左边)
* wrap-reverse：换行，第一行在下面（主轴是水平方向，反之第一行是在右边)
  
  ![Alt text](../../../../c:/Users/005/Desktop/%E8%B5%84%E6%96%99/img5.jpg)
  ![Alt text](../../../../c:/Users/005/Desktop/%E8%B5%84%E6%96%99/img6.jpg)  
  ![Alt text](../../../../c:/Users/005/Desktop/%E8%B5%84%E6%96%99/img7.jpg)

### 2.3 flex-flow 属性

  默认flex-flow：row nowrap; 可以看出 flex-flow 属性是flex-direction 和flex-wrap的合并简写形式。需要设置这两个值时优先使用简写形式。

  ``` css
    .box {
      flex-wrap: <flex-direction> <flex-wrap>;
    }
  ```

### 2.4 justify-content 属性

  justify-content属性决定项目在**主轴**上的对齐方式。

  ``` css
    .box {
      justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;
    }
  ```

* flex-start (默认值)：主轴起点对齐
* flex-end：主轴终点对齐
* center：主居中对齐
* space-between：两端对齐，两两项目之间间距相等
* space-around: 各项目左右间距相等，所以中间项目间距比两端大一倍
* space-evenly: 各项目均分容器空间（左右端也会有同等间距，但是该属性兼容性不太好，使用时注意）  
  ![Alt text](../../../../c:/Users/005/Desktop/%E8%B5%84%E6%96%99/img8.jpg)

### 2.4 align-items 属性

  align-items 意为垂直方向，交叉轴对齐。align-items属性决定项目在在**交叉轴**上的对齐方式。

  ``` css
    .box {
      align-items: flex-start | flex-end | center | stretch | baseline;
    }
  ```

* flex-start：交叉轴起点对齐
* flex-end：交叉轴终点对齐
* center：交叉轴居中对齐
* stretch (默认值)：如果项目未设置高度或者设为auto，将占满整个容器的高度
* baseline: 项目的第一行文字的基线对齐  

![Alt text](../../../../c:/Users/005/Desktop/%E8%B5%84%E6%96%99/img9.jpg)  

### 2.5 align-content 属性

  align-content属性决定在交叉轴上多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。(可以理解为项目有多行时有效)。默认是stretch（项目没有定义高度或auto）

  ``` css
    .box {
      align-content: flex-start | flex-end | center | space-between | space-around | stretch;
    }
  ```

  属性参数作用同前两点，主要就是该间距比例都是轴线之间，不是各个项目之间  
  ![Alt text](../../../../c:/Users/005/Desktop/%E8%B5%84%E6%96%99/img10.jpg)

***
（以下属性是添加在容器内子元素上的）

### 2.5 flex-grow 属性

flex-grow 属性控制项目放大比例，默认为0，即如果存在剩余空间，也不放大。（负值无效）

``` css
  .item {
    flex-grow: <number>; /* default 0 */
  }
```

  所有项目设置为1时，将均分剩余空间。  
  为什么这里前两个和第三个项目并不是1：2的关系？要理解是分配剩余空间的占比不是项目和项目的比列关系。

  ![Alt text](../../../../c:/Users/005/Desktop/%E8%B5%84%E6%96%99/img11.jpg)

  这里容器总宽500px，三个项目width都为100px，剩余空间即为200px。flex-grow 分别为1 1 2，以1：1: 2的比例分配**剩余空间**那200px。最后形成如图效果。  
  
### 2.6 flex-shrink 属性

flex-shrink 属性控制项目收缩比例，默认为1，即如果空间不足，项目缩小。（负值无效）  
设为0，则该项目在空间不足时也不收缩。

``` css
  .item {
    flex-shrink: <number>; /* default 1 */
  }
```

![Alt text](../../../../c:/Users/005/Desktop/%E8%B5%84%E6%96%99/img12.jpg)

### 2.7 flex-basis 属性

flex-basis属性控制项目占据主轴的空间，优先级大于设定的width（height)。

``` css
  .item {
    flex-basis: <length> | auto; 
  }
```

参数可以是长度单位或百分比，auto 是默认值，长度等于项目的长度。  
![Alt text](%E8%B5%84%E6%96%99/img13.jpg)  
![Alt text](%E8%B5%84%E6%96%99/img14.jpg)

### 2.8 flex 属性

flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。

``` css
  .item {
    flex: <flex-grow> <flex-shrink> <flex-basis>;
  }
```

（简写优于写三个参数）

1. flex: 1 1 auto; 等于 flex: auto; 表示项目等比放大或缩小。
2. flex: 0 0 auto; 等于 flex: none; 表示项目既不扩大也不缩小。
3. flex: 1；其实就是设置了flex-grow：1， 其余两个参数默认值是 1 auto；也就是 flex: 1 ==> flex: 1 1 auto; ==> flex: auto;

### 2.9 align-self 属性

align-self属性可以为项目设置与其他项目不一样的对齐方式，具体参数用法和align-items一致，只不过它是作用于单个项目，属性也是写在项目上（子元素）不是容器上（父元素）。  

``` css
  .box {
    align-self: flex-start | flex-end | center | stretch | baseline;
  }
```

![Alt text](%E8%B5%84%E6%96%99/img15.jpg)

### 2.10 order 属性

order 属性控制项目的排列顺序。默认为0，项目从小到大排列。

``` css
  .item {
    order: <integer>; /* default 0, 可负*/
  }
```

![Alt text](%E8%B5%84%E6%96%99/img16.jpg)

## 三、flex布局应用

### 3.1 三栏布局

左中右布局，中间内容宽度自适应。左右项目宽度固定，中间项目设置flex: auto; 也就是 flex: 1 1 auto;

``` html
  <style>
    .flex-container {
      display: flex;
      width: 500px;
      height: 300px;
      background-color: #f0f0f0;
    }
    .flex-container .flex-item {
      width: 100px;
      height: 30px;
      border: 1px solid #000;
      font-size: 20px;
      text-align: center;
    }
    .flex-container .left-item,.right-item {
      background-color: #ffe4c4;
    }
    .main-item {
      flex: auto;
      background-color: #ffa500;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }
  </style>
  <div class="flex-container">
    <div class="flex-item left-item">left</div>
    <div class="flex-item main-item">main main main main main main main</div>
    <div class="flex-item right-item">right</div>
  </div>
```

![Alt text](%E8%B5%84%E6%96%99/img18.jpg)

### 3.2 左右布局

多个项目，最后一个居右。设置最后一个项目 margin-left: auto;

``` html
  <style>
  .flex-container {
      display: flex;
      width: 500px;
      height: 300px;
      background-color: #f0f0f0;
    }
    .flex-container .flex-item {
      width: 50px;
      height: 30px;
      background-color: #ffa500;
      border: 1px solid #000;
      font-size: 20px;
      text-align: center;
    }
    .right-item {
      margin-left: auto;
    }
  </style>
  <div class="flex-container">
    <div class="flex-item">left1</div>
    <div class="flex-item">left2</div>
    <div class="flex-item">left3</div>
    <div class="flex-item right-item">right</div>
  </div>
```

![Alt text](%E8%B5%84%E6%96%99/img19.jpg)

### 3.3 垂直居中布局

垂直居中布局，可以看成就是在主轴和交叉轴上都采用居中对齐的方式。justify-content: center; align-items: center;

``` html
  <style>
    .flex-container {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 500px;
      height: 300px;
      background-color: #f0f0f0;
    }
    .flex-container .flex-item {
      color: #5e6d82;
      text-align: center;
    }
  </style>
  <div class="flex-container">
    <div class="flex-item">
      <img src="c:\Users\005\Desktop\img\empty.png"/>
      <p>暂无数据</p>
    </div>
  </div>
```

![Alt text](%E8%B5%84%E6%96%99/img17.jpg)

### End

第一次发文，如有错误或不恰当之处，还请指正~  
