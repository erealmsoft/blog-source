---
title: CSS布局之position
tags:
  - web
  - 开源
  - CSS
  - CSS position
  - CSS 布局
  - CSS 定位
  - web front-end
  - web 前端
categories:
  - others
date: 2014-11-17 00:00:00
---


&emsp;&emsp;CSS中的`position`规定元素的定位类型， 把浏览器窗口想象成一个坐标系统，你可以将一个元素精确地放在页面上你所指定的地方。。
```css
	div { position: static;}   
	div { position: relative;}    
	div { position: absolute;}
	div { position: fixed;}  
	div { position: inherit;}  
```
 
&emsp;&emsp;`position`属性有五个值，实际上最常用的只有三种，static和inherit不常用。

## Static
&emsp;&emsp;每一个元素默认的position都为static，也就是没有定位，元素出现在正常的流中，left/right/bottom/top对static定位的元素没有影响。

## Relative
 
相对定位，它是相对元素`自身`在`正常文档流`中的位置，是相对它自己的。 
> 很多时候，我们定位某元素为relative是为了它的子元素定位为absolute。

`需注意：` 如果你设置了某元素的position的值为relative,而没有设置其他属性(top, left, bottom or right),那么对该元素将不产生任何影响，就跟设置static是一个效果。但是，如果你除了position为relative外，还设置了其他定位属性，比如top： 10px,那么该元素将相对于它本身在正常文档流中向上偏离10px。 这里有两个问题需要思考：  
 
1. 它还在普通流中吗？也就是它原来的位置会被紧跟着的元素占据吗？ 
 
2. 它移动后会覆盖其它元素吗？ 

首先，其它元素不会调整位置来弥补它偏离后剩下的位置。  

其次，它不仅会覆盖其它元素，而且即使对position值是static，即没有定位的其它元素设置z-index更高的值，这个定位的元素也始终会覆盖其它未被定位的元素。  

当你设置元素position为relative时，有两件事会发生：  
  
- 你可以设置这个元素的z-index属性，它主要设置元素的堆叠顺序。而没有定位的元素，使用这个属性是没有意义的。  

- 它限制了绝对定位的子元素的范围。任何绝对定位的元素，如果祖先元素position为relative，那么这个子元素是在祖先元素内以祖先元素为参考的。这一点下面理解了绝对定位之后就清楚是什么意思了！


## Absolute

绝对定位，它是`相对最近positioned`，也就是已经设置`position`为`absolute`或`relative`的`祖先元素`。注意`最近`两个字，指的是一层一层往上找，如果没有，那么它是相对于body元素。 同样的两个问题：  

1. 它还在普通流中吗？也就是它原来的位置会被紧跟着的元素占据吗？ 
 
2. 它移动后会覆盖其它元素吗？  

![图1](http://i.imgur.com/W2ikffF.png)

每个网页都可以看成是由一层层页面堆叠起来的，元素被设置为`absolute`或`fixed`后，会发生三件事情：  
  
- 相当于把元素往z轴移动了一层，元素脱离了原来正常的文档流了。 。其它的元素表现的就像是它不存在一样，会占据它原来的位置。如果不想覆盖其它元素，可以通过设置z-index。  
 
- 该元素变为块级元素。相当于给元素设置了`display： none`，内联元素也可以设置它的高度了。  

- 如果该元素是块级元素，元素由原来的占据一行，变成了auto。  

上面讲相对定位的时候提过，设置元素position为relative时，它限制了绝对定位的子元素的范围。具体是什么意思呢？  


> 一般我们设置某个元素position为relative，然后设置它的子元素为absolute，这样这个子元素就始终在这个父元素范围内进行定位。  
  
![图1](http://i.imgur.com/XOuP7am.png)  

这是[http://www.erealm.cn](http://www.erealm.cn) contact页面上的部分截图。  

less代码如下：  
```css
    .content {
      min-height: 400px;
      position: relative;
      background-color: @white;
    }


    .contact-details {
      text-align: left;
      position: absolute;
      right: 3%;
      margin: 3em 0;
      z-index: 99;
      background: #39a9a4;
      background: rgb(57,169,164);
      background: rgba(57,169,164, 0.95);
      color: #fff;
      padding: 1.5em;  
      .................  
    }  
```
html页面代码为：  
```html
    <div class="content">
      <div class="contact-details">
        .......................
      </div>
    </div>  
```
&emsp;&emsp;可以看到，父元素div的position为relative，子元素div为absolute。子元素相对于父元素进行定位:`right: 3%`,在父元素偏离于它的右边距3% 。
    
&emsp;&emsp;`再一次，需要记住：相对定位相对元素在文档流中的本来位置，而绝对定位是相对于最近的已定位祖先元素，如果不存在已定位的祖先元素，那么“相对于”body。`  

## Fixed   

&emsp;&emsp;跟absolute定位很相似，唯一不同的是，它是相对于浏览器窗口进行定位的，无论窗口滚动与否，元素都会留在那个位置。相当于一种特殊的absolute。

![图2](http://i.imgur.com/TglXIkt.png)  

&emsp;&emsp;这个绿色图标是[http://www.erealm.cn](http://www.erealm.cn) 页脚元素内的子元素，点击随时返回到顶部。即使窗口滚动，也始终可以看到这个元素在浏览器右下角。  

代码如下：  
```css
    .back-top {
      position: fixed;
      font-size: .8em;
      color: @white;
      bottom: 20px;
      right: 20px;
      line-height: 25px;
      width: 25px;
      height: 25px;
      border-radius: 50%;
      border:1px solid @white;
      text-align: center;
      background: @green;
      z-index: 1000;
	}
```
## Inherit  

继承父元素的position值。 

