# CSS 清除浮动

------

​	最初引入 float 属性是为了能让 web 开发人员实现简单的布局，包括在一列文本中浮动的图像，文字环绕在它的左边或右边。在非IE浏览器（如Firefox）下，当容器的高度为 auto，且容器的内容中有浮动（ float 为 left 或 right ）的元素，在这种情况下，容器的高度不能自动伸长以适应内容的高度，使得内容溢出到容器外面而影响（甚至破坏）布局的现象。这个现象叫浮动溢出，为了防止这个现象的出现而进行的 CSS 处理，就叫 CSS 清除浮动。

----

### 给浮动元素的容器设置具体高度

​	给浮动元素的容器设置具体高度即可消除浮动溢出对后面的布局的影响，但是在实际的开发过程中，有时并不方便给容器具体高度数值。

-----

### **使用邻接元素处理**

​	给浮动元素后面的元素添加clear属性。

```css
<style>
	.bigBox {
    	width: 600px;
        margin: 0 auto;
        background-color: rgb(190, 250, 40);
    }

    .box1 {
        width: 200px;
        height: 200px;
        background-color: skyblue;
        float: left;
    }

    .box2 {
        width: 200px;
        height: 200px;
        background-color: aquamarine;
        float: right;
    }

    .footer {
        width: 100%;
        height: 100px;
        background-color: burlywood;
        clear: both;
    }
</style>
<body>
	<div class="bigBox">
    	<div class="box1"></div>
    	<div class="box2"></div>
	</div>
	<div class="footer"></div>
</body>
```

----------

### 使用带clear属性的空元素

​	有时没有现有的元素可以应用清理，所以我们只能添加一个空元素并且清理它，如：<div class="clear"></div>

缺点：大量无语义的html元素，后期不容易维护。

```css
<style>
	.clear {
		clear: both;
	}
</style>
<body>
    <div class="box2"></div>
    <div class="clear"></div>
</body>
```

--------

### 给浮动的元素的容器添加浮动

​	给浮动元素的容器也添加上浮动属性即可清除内部浮动，但是这样会使其整体浮动，影响布局，不推荐使用。

------------

### 使用CSS的overflow属性

​	给浮动元素的容器添加overflow:hidden;或overflow:auto;可以清除浮动，另外在 IE6 中还需要触发 hasLayout ，例如为父元素设置容器宽高或设置 zoom:1。在添加overflow属性后，浮动元素又回到了容器层，把容器高度撑起，达到了清理浮动的效果。

```css
<style>
	.bigBox {
      	overflow:hidden;
      	zoom:1;
	}
</style>
```

-------

### 使用CSS的:after伪元素

​	给浮动元素的容器添加一个clearfix的class，然后给这个class添加一个:after伪元素(注意这不是伪类，而是伪元素，代表一个元素之后最近的元素)实现元素末尾添加一个看不见的块元素清理浮动。需要注意的是为了IE6和IE7浏览器，要给clearfix这个class添加一条zoom:1;触发haslayout。

```css
<style>
	.clearfix:after{
  		content: ""; 
  		display: block;
  		clear: both; 
  		visibility: hidden;  
  	}

	.clearfix {
  		/* 触发 hasLayout */ 
  		zoom: 1; 
  	}
</style>
<body>
	<div class="bigBox clearfix">
    	<div class="box1"></div>
    	<div class="box2"></div>
	</div>
</body>
```

-----

## JS清除浮动

### HTML DOM clear 属性

语法：

```javascript
Object.style.clear=left|right|both|none
```

-------------