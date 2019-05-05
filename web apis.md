# day01 

## 一、获取元素  

### 1. 通过ID获取元素  
```html
  <div id="box"></div>

  <script>
    var boxDom = document.getElementById('元素id')   // 返回一个元素对象  DOM元素  
  </script>
```

### 2. 通过标签获取元素  

```html
  <div id="box">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
  </div>

  <script>
    
    方式1： 直接获取
    var lis = document.getElementsByTagName('标签名')   // 返回一个伪数组 建议使用for循环遍历  

    方式2：通过id间接获取
    var box = document.getElementById('box')   // 返回一个元素对象  DOM元素  
    var lis = box.getElementsByTagName('标签名')   //返回一个伪数组 建议使用for循环遍历  
  </script>

```

### 3. 通过类名获取元素  

```html
  <div id="box">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
  </div>

  <script>
    
    方式1： 直接获取
    var lis = document.getElementsClassName('类名')   // 返回一个伪数组 建议使用for循环遍历  

    方式2：通过id间接获取
    var box = document.getElementById('box')   // 返回一个元素对象  DOM元素  
    var lis = box.getElementsClassName('类名')   //返回一个伪数组 建议使用for循环遍历  
  </script>

```

### 4. h5 新增的   （不考虑ie9以下的兼容性，推荐使用）

```html
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>

  <script>
    document.querySelector('.item')   // 获取查找到的第一个元素

    document.querySelectorAll('.item')  // 得到一个伪数组
  </script>
```

## 二、 事件绑定  

+ 事件源 （获取DOM元素）

+ 事件类型  鼠标事件和键盘事件

+ 处理函数   匿名函数

```html

  <button id="btn">btn</button>

  // 1. 获取DOM元素
  var btnDOM = document.querySelector('#btn')

  // 2. 绑定点击事件
  btnDOM.onclick = function(){
    
    <!-- 3. 处理业务 -->
	this.innerHTML = 'ssr'
  }

```

## 三、元素操作   

### 1. innerHTML 和 innerText   

innerHTML 和 innerText 都是可以读写的

```html
  <div id="box">
    box
    <mark>mark标签</mark>
  </div>

  <script>

    var boxDOM = document.querySelector('#box')

    // 读 
      console.log( boxDOM.innerText)   // 去掉标签去掉空格和换行
      console.log( boxDOM.innerHTML)   // 原样输出

    // 写
     boxDOM.innerText='<mark>ssr</mark>'   // 不解析html标签  <mark>ssr</mark>
      boxDOM.innerHTML = <mark>ssr</mark>'   // 解析html标签
    
  </script>
```

### 2. 修改元素的属性

+ alt 
+ src 
+ href 
+ 

```js
什么是元素的属性

一个元素有 标签 属性 属性值 文本内容
<div title="title"></div>

var divDOM = document.querySelector('div')

divDOM.title = 'ssr'
```

### 3. 读写表单元素的属性  

+ type 	 表单类型
+ value        表单值
+ disabled   禁用
+ checked   选中

### 4. 表单元素事件

+ onfocus   获取焦点  
+ onblur     失去焦点

```
element.onfocus = function(){     //只能是表单元素才能这么用
    
}

element.onblur = function(){     //只能是表单元素才能这么用
    
}
```



## day02 

### 一、排他算法

```html
  <button>按钮1</button>
  <button>按钮2</button>
  <button>按钮3</button>
  <button>按钮4</button>
  <button>按钮5</button>

  <script>
    // 1. 获取所有按钮元素
    var btns = document.getElementsByTagName('button');

    // btns得到的是伪数组  里面的每一个元素 btns[i]
    for (var i = 0; i < btns.length; i++) {
      // 把索引保存在每一个buton 的index属性上
      btns[i].index = i  
      //给每一项添加绑定事件
      btns[i].onclick = function () {
        // (1) 我们先把所有的按钮背景颜色去掉  干掉所有人
        
        for (var i = 0; i < btns.length; i++) {
          btns[i].style.backgroundColor = '';
        }
        // (2) 然后才让当前的元素背景颜色为pink 留下我自己
        this.style.backgroundColor = 'pink';
        // btns[this.index].style.backgroundColor = 'pink';
      }
    }
        //2. 首先先排除其他人，然后才设置自己的样式 这种排除其他人的思想我们成为排他思想
  </script>
```



### 二、元素属性操作

 1. element.属性名

 2. element.getAttribute('属性名称')

 3. element.setAttribute('属性名称','属性值')

 4. element.removeAttribute('属性名称')

 5. element.dataset()

```html
	定义的自定义属性建议写成  data-自定义属性名='属性值'
    <div getTime="20" data-index="2" data-list-name="andy"></div>
    <script>
        // 获取DOM元素 
        var div = document.querySelector('div');
        // console.log(div.getTime);
        console.log(div.getAttribute('getTime'));
        div.setAttribute('data-time', 20);
        console.log(div.getAttribute('data-index'));
        console.log(div.getAttribute('data-list-name'));

        
        // h5新增的获取自定义属性的方法 它只能获取data-开头的  ie 11+  
        // dataset 是一个集合里面存放了所有以data开头的自定义属性
        console.log(div.dataset);
        console.log(div.dataset.index);
        console.log(div.dataset['index']);
        // 如果自定义属性里面有多个-链接的单词，我们获取的时候采取 驼峰命名法
        console.log(div.dataset.listName);
        console.log(div.dataset['listName']);
    </script>

```
### 三、节点操作

1. 节点的类型
   + 元素节点  标签 
   + 属性节点  标签的属性 
   + 文本节点  标签之间的文本内容包括空格换行也算

2. element.parentNode

```html
      <div class="demo">
        <div class="box">
            <span class="erweima">×</span>
        </div>
    </div>

    <script>
        // 1. 父节点 parentNode
        var erweima = document.querySelector('.erweima');
        // var box = document.querySelector('.box');
        // 得到的是离元素最近的父级节点(亲爸爸) 如果找不到父节点就返回为 null
        console.log(erweima.parentNode);
    </script>
```

3. element.childNodes 和 element.children

```html
    <ul>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>
    </ul>


    <script>
        // DOM 提供的方法（API）获取
        var ul = document.querySelector('ul');
        var lis = ul.querySelectorAll('li');
        // 1. 子节点  childNodes 所有的子节点 包含 元素节点 文本节点等等
        console.log(ul.childNodes);
        console.log(ul.childNodes[0].nodeType);
        console.log(ul.childNodes[1].nodeType);
        // 2. children 获取所有的子元素节点 也是我们实际开发常用的
        console.log(ul.children);
    </script>
```

​	


