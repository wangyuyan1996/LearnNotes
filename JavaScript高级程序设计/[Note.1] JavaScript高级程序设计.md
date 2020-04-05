## JavaScript简介
JavaScript是以一种专门为与网页交互而设计的脚本语言，由三部分组成：

- ECMAScript, 由ECMA-262定义，提供核心语言功能
- 文档对象模型（DOM），提供访问和操作网页内容的方法和接口
- 浏览器对象模型（BOM），提供与浏览器交互的方法和接口
<br />
<br />

## 1.在HTML中使用JavaScript
#### 1.1 使用<script>元素
在HTML中潜入JavaScript的主要方法就是使用<script>标签，该标签由6个属性：<br />
① async [可选]: 表示立即下载脚本，但不妨碍页面的其他操作，比如下载其他资源或者等待加载其他脚本。该属性只对外部脚本文件有效。
<br />

② charset [可选]: 表示通过src属性指定的代码字符集。由于大多数浏览器会忽略它的值所以较少使用
<br />

③ defer [可选]: 表示脚本可以延迟到文档完全被解析和显示后再执行。只对外部脚本文件有效。
<br />

④ src [可选]: 表示包含要执行代码的外部文件。

⑤ type [可选]: 表示编写代码使用的脚本语言内容类型（也称为MIME类型）
考虑到约定俗称和最大限度的浏览器兼容性，目前type属性的值依旧还是text/javascript，该值是默认值，非必须声明。

~~⑥language: 已废弃，不作赘述~~


```
Example:

//在<script>中嵌入js代码
<script type="text/javascript">
  function helloWorld() {
    alert ('Hello World!');
  }
</script>

//引入文件（本地文件）
<script type="text/javascript" src="example.js"></script>

//引入文件（外部域文件）
<script type="text/javascript" src="http://www.somewhere.com/file.js"></script>

---
注意：带有src属性的script元素不应该再嵌入其他额外的JavaScript代码，如果嵌入也只会下载和执行外部脚本文件。
```

> script标签只要不存在defer和async属性，浏览器都会按照其在页面中出现的先后顺序依次进行解析。

##### 1.1.1 标签位置
> 按照惯例应该是把<script>标签都放在<head>标签里，这样做是为了把所有外部文件（css文件，js文件）的引用都放在相同的地方，但这意味着必须等所有JavaScript代码都被下载和解析执行完成之后才能开始呈现<body>部分的内容。这会导致页面渲染的延迟，为了避免这个问题，现在web应用程序一本都把JavaScript引用放在<body>中靠后部分：

```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <div>
    <h3>Test</h3>
    <p>This is a test page.</p>
  </div>
  
  <script type="text/javascript" src="example.js"></script>
  <script type="text/javascript">
    //在<script>中嵌入js代码
    function helloWorld() {
      alert('Hello World!');
    }

    helloWorld();
  </script>
</body>

</html>
```

##### 1.1.2 延迟脚本
> defer属性用途就是表明脚本在执行时不会影响页面的构造。也就是脚本会延迟到整个页面都解析完毕后再运行。所以在<script>设置defer属性就是告诉浏览器，立即下载但延迟执行

```
<head>
  <script type="text/javascript" src="example.js" defer></script>
</head>

//这里虽然放在head中，但其中包含的脚本将延迟到浏览器遇到</html>标签后再执行。
//都设置了defer属性的脚本会按照顺序执行（也并非所有浏览器都会严格按照顺序执行）
```
> IE4、Firefox 3.5、Safari 5和Chrome是最早支持defer属性的浏览器，其他浏览器会忽略这个属性，因此把延迟脚本放在页面底部较好

> 在XHTML中，要把defer设置为defer="defer"

##### 1.1.3 异步脚本
async属性与defer属性类似，都用于改变处理脚本的行为。与defer不同的是，async的脚本并不保证按照指定他们的先后顺序执行

```
<head>
  <script type="text/javascript" src="example1.js" async></script>
  <script type="text/javascript" src="example2.js" async></script>
</head>

//以上两个脚本的执行顺序无法确定，所以要确保两者之间没有依赖关系，指定async的目的是为了不让页面等待两个脚本的下载和执行，从而异步加载页面其他内容。建议异步脚本不要在加载期间修改DOM。
//异步脚本一定会在页面的load事件前执行，但可能会在DOMContentLoaded事件触发之前或之后执行。
```
> 在XHTML中，要把async设置为async="async"

#### 1.2 嵌入代码与外部文件
虽然在HTML中嵌入JavaScript没有问题，但是一般认为最好的做法还是通过引入外部文件来包含JavaScript代码，外部文件引入有以下优点:
<br/>
① 可维护性: 把所有JavaScript文件放在一个文件中，维护性良好，而且HTML和JavaScript代码可以分开维护
<br />
② 可缓存: 浏览器能够根据具体设置，缓存链接的所有外部JavaScript文件，这样能够更快加载页面
<br />
③ 适应未来: 通过外部文件来包含JavaScript无需使用XHTML或者注释hack

#### 1.3 文档模式
文档模式是使用文档类型doctype切换实现的。主要是影响CSS内容呈现，但某些情况下也会影响到JavaScript解释执行。
<br />
① 混杂模式(quirks mode)
<br />
② 标准模式(standards mode)
<br />
③ 准标准模式(almost standards mode)

如果在文档开始时没有发现文档类型声明则默认启用混杂模式，该模式不推荐使用，会使得不同浏览器下行为差异很大。

对于标准模式，可以通过使用下面任何一种文档类型来开启：
```
<!-- HTML 4.01 严格型 -->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">

<!-- HTML5 -->
<!DOCTYPE html>
```

对于准标准模式，可以使用过渡性或框架集型文档来触发

```
<!-- HTML 4.01 过渡型 -->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">

<!-- HTML 4.01 框架集型-->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">
```
> 准标准模式和标准模式非常接近，差异可以忽略不计
<br />
<br />