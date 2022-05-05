# CSS知识点总结

## CSS基础概念

### CSS是谁发明的？
* 李爵士的挪威同事赖先生（Hakon Wium Lie），首先提出CSS。

### CSS厉害在哪儿？

* CSS 厉害在层叠样式表。如：样式层叠（可以多次对同一选择器进行样式声明； 选择器层叠：可以用不同选择器对同一个元素进行样式声明； 文件层叠：可以用多个文件进行层叠。 这些文件特性使得CSS极度灵活，为后来被吐槽留下了隐患。

### CSS的版本

* 使用最广泛的版本是： CSS 2.1 ；
  
* 目前最现代的版本： CSS 3 。

### 经验

* 怎么知道哪些浏览器支持哪些特性呢？
  
  使用 `caniuse.com` 查询。

* 不要用理性思维来学CSS，不要问为什么，而是说原来是这样啊，浏览器说是怎么样，就是怎么样。

### 如何调试CSS？

* border调试法： 怀疑某个元素问题，就给这个元素加border，border没出现，说明选择器错了或者语法错误了，border出现了，看看边界是否符合预期。bug解决了，才可以把border删掉。
  
### 文档流

#### 文档流动方向

* inline元素从左到右，到达最右边才会换行；

* block元素从上到下，每一个都另起一行；
  
* inline-block也是从左到右。

#### 宽度

* inline宽度为内部inline元素的和，不能用width指定；

* block默认自动计算宽度，可用width指定；

* inline-block结合前两者特点，可用width。

#### 高度

* inline高度由line-height间接确定，跟height无关，跟padding也无关；

* block高度由内部文档流元素确定，可用设height；

* inline-block跟block类似，可用设置height。

#### 哪些元素脱离文档流？

* float；

* position：absolute/fixed。

### 盒模型

#### CSS有两种盒模型，分别是：

* content-box： 内容盒-内容就是盒子的边界

* border-box： 边框盒-边框才是盒子的边界 
  
#### 公式

* content-box width=内容宽度
  
* border-box width=内容宽度+padding
  +border

 (border-box更好用，一般情况下都用border-box)

#### margin合并

* 哪些情况会合并： 父子margin合并；兄弟margin合并（合并只出现在上下，不出现在左右)

* 如何阻止合并： 父子合并用padding/border挡住； 父子合并用overflow: hidden 挡住； 父子合并用display：flex。  兄弟合并可以用inline-block消除。

## CSS布局

### 布局

#### CSS布局分为两类：

* 固定宽度布局，一般宽度为960/1000/1024px；

* 不固定宽度布局，主要靠文档流的原理来布局。

* 响应式布局，PC上固定宽度，手机上不固定宽度，也就是一种混合布局。

#### 布局的两种思路：

* 从大到小，先定下大局，然后完善每个部分的小布局（一般老手用的多）

* 从小到大，先完成小布局，然后组成大布局（新手用的多）

### float布局

* 子元素上加`float：lift`和`width`；

* 在父元素上加 `.clearfix` 
  
```
.clearfix:after{
    content: '';
    display: block;
    clear: both;
}
```

### flex布局

#### flex：一维布局用flex，大部分浏览器都兼容。重点记住以下代码：

* `display: flex`
  
* `flex-direction: row/column`
  
* `flex-wrap: wrap`
  
* `justify-content: center/space-between`
  
* `align-items:center`

### Grid布局

#### Grid：二维布局用Grid，暂时还未普及。

## CSS定位

### 布局和定位的区别？

* 布局是屏幕平面上的，定位是垂直于屏幕的。

### 一个div的分层

* 分别是background，border，块级子元素，浮动元素，内联子元素。

### 新属性——position

#### position

* static 默认值，待在文档流里面；

* relative相对定位，升起来，但不脱离文档流；

* absolute绝对定位，定位基准是在祖先里的非static；

* fixed固定定位，定位基准是viewport（有诈）；

* sticky粘滞定位，不好描述。

#### 经验

* 如果你写了absolute，一般都得补一个relative；

* 如果你写了absolute或者fixed，一定要补top和left；

* sticky兼容性很差，主要用于面试。

#### z-index用法？

* auto；0； 正数，负数。

#### 层叠上下文是什么？

* 会把所有的分层包起来，默认的层叠上下文元素html和负z-index。（负的z-index逃不出元素背景，那就是这个元素变成层叠上下文。）

## CSS动画

### 浏览器渲染过程

#### 步骤

* 根据HTML构建HTML树（DOM）

* 根据CSS构建CSS树（CSSOM）

* 将两颗树合并成一棵渲染树（render tree）

* Layout布局（文档流、盒模型、计算大小和位置）

* paint 绘制（把边框颜色、文字颜色、阴影等画出来）

* Compose 合成（根据层叠关系展示画面）

### 三种更新方式

1. JS/CSS > 样式 > 布局 > 绘制 > 合成

2. JS/CSS > 样式 > 绘制 > 合成
   
3. JS/CSS > 样式 > 合成

### transform全解

#### 四个常用功能

* 位移 translate

* 缩放 scale
  
* 旋转 rotate

* 倾斜 skew

#### 经验

* 一般都需要配合transition过渡；

* inline元素不支持transform，需要先变成block。

### transition过渡

1. 作用： 补充中间帧。

2. 语法：

* transition：属性名 时长 过渡方式 延迟

* transition： left 200ms linear

* 可以用逗号分隔两个不同的属性

*  transition： left 200ms ; top 400ms

* 可以用all代表所有属性

* transition： all 200ms 

* 过渡方式有: linear/ease/ease-in/ease-out/ease-in-out/cubic-bezier/step-start/step-end/step ,具体含义要靠数学知识。

#### 注意：

* 并不是所有属性都能过渡；

* display：none =>block 没法过渡；

* 一般改成visibility：hidden=>visible；

* 过渡必须有始有终。

#### 制作红心的案例(transition版)

```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
</head>
<body>
  <div id="heart">
    <div class="left"></div>
    <div class="right"></div>
    <div class="bottom"></div>
  </div>
</body>
</html>
```

```
*{margin:0; padding:0;box-sizing:border-box;}
#heart{
  margin:100px;
  position:relative;
 display: inline-block;
  transition:all .5s;
}
#heart:hover{
  transform: scale(1.5);
}
#heart>.bottom{
  width:50px;
  height:50px;
  transform:rotate(45deg);
  background: red;
}
#heart>.left{
  width:50px;
  height:50px;
  position:absolute;
  transform:rotate(45deg) translateY(32px);
  bottom:100%;
  left:100%;
  border-radius:50% 50% 0% 0%;
  background: red;
}
#heart>.right{
  width:50px;
  height:50px;
  position:absolute;
  transform:rotate(45deg) translateX(32px);
  bottom:100%;
  right:100%;
  border-radius:50% 0% 0% 50%;
  background: red;
}
```

### 使用animation

#### @keyframes完整语法

1. 一种写法是form to

```
@keyframes slidein{
    form{
        transform: translateX(0%);
    }
    to{
        transform: translateX(100%)
    }
}
```

2. 另一种写法是百分数

```
@keyframes indentifier{
0% {top: o%; left: 0;}
30%{top: 50%;}
68%, 72%{left: 50%;}
100% {top: 100px; left: 100%;}
}
```

#### animation缩写语法

* animation：时长|过渡方式|延迟|次数|方向|填充模式|是否暂停|动画名。

* 时长： 1s或者1000ms。

* 过渡方式： 跟transition取值一样，如linear。

* 次数： 3或者2.4 或者infinite

* 方向： reverse|alternate|alternate-reverse

* 填充模式：none|forwards|backwards|both

* 是否暂停：paused|running

* 以上所有属性都对应着单独的属性。

#### 红心跳动的案例（animation版）

```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
</head>
<body>
  <div id="heart">
    <div class="bottom"></div>
    <div class="left"></div>
    <div class="right"></div>
  </div>
</body>
</html>
```

```
*{margin:0; padding:0;box-sizing:border-box;}
#heart{
  margin:200px;
  position:relative;
 display: inline-block;
  animation: heart 500ms linear infinite alternate;
}
@keyframes heart{
  0%{
    transform: scale(1.0);
  }
  100%{
    transform: scale(2.0);
  }
}
#heart>.bottom{
  width:50px;
  height:50px;
  transform:rotate(45deg);
  background: red;
}
#heart>.left{
  width:50px;
  height:50px;
  position:absolute;
  transform:rotate(45deg) translateY(32px);
  bottom:100%;
  left:100%;
  border-radius:50% 50% 0% 0%;
  background: red;
}
#heart>.right{
  width:50px;
  height:50px;
  position:absolute;
  transform:rotate(45deg) translateX(32px);
  bottom:100%;
  right:100%;
  border-radius:50% 0% 0% 50%;
  background: red;
}
```




  







