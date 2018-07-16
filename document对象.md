`document`对象时文档的根节点, `document`对象是`window`对象的属性
`document`对象继承了`EventTarget`接口, Node接口, `ParentNode`接口

# document的属性
## 快捷方式属性
`document.defaultView` 返回`document`对象所属的`window`对象, 若当前文档不属于`window`则返回`null`
一个html文件
```JavaScript
<!DOCTYPE html>
<html>
<head></head>
<body><body>
</html>
```
+ `document.doctype`返回的是文档的&lt;DOCTYPE&gt;节点, 若html没有声明DTD, 则返回null
+ `document.docueentElement` 返回文档的根节点, 在	html中为&lt;html&gt;节点
+ `document.body`返回html的&lt;body&gt;节点, 属性可写
+ `document.head`返回html的&lt;head&gt;节点, 属性可写
+ `document.scrollingElement`属性返回文档中的滚动节点. 标准模式下返回文档的根节点`document.`documentElement, 兼容模式下返回`document.body`节点, 若不存在则返回null
+ `document.activeElement`返回获得当前焦点的节点. 通常为表单节点(如: &lt;input&gt;, &lt;select&gt;)若当前没有焦点节点则返回&lt;body&gt; 或null
+ `document.fullscreenElement`返回全屏状态的节点(如&lt;video&gt;的全屏), 若没有则返回null

## 节点集合属性
`HTMLCollection`实例是类似数组的对象(array-like Object). 若成员有id和name属性则实例也可以使用这两个属性
`HTMLCollection`实例表示文档内部特定元素的集合, 集合是动态的. 原节点有任何变化, 立刻会反映在集合中
+ `document.links` 返回当前文档所有设定href属性的&lt;a&gt;和&lt;area&gt;节点
+ `document.forms`属性返回所有&lt;form&gt;表单节点
+ `document.images`属性返回页面所有&lt;img&gt;图片节点
+ `document.embeds`和+ `document.plugins`属性返回所有&lt;embed&gt;节点
+ `document.scripts`属性返回所有的&lt;script&gt;节点
以上属性返回的是`HTMLCollection`实例, 可以通过`instanceof`属性判定
+ `document.styleSheets`返回文档内内嵌或引入的样式表集合. 但是返回的不是`HTMLCollection`

## 文档静态信息属性
+ `document.documentURI`和`document.URL`都返回一个字符串表示当前文档的网址. 但是`documentURI`继承自`Document`接口, 可用于所有文档, `URL`继承自`HTMLDocument`接口只能用于HTML文档. 文档中的锚点变化会反映在这两个属性中
+ `document.domain`返回当前文档的域名, 且不包含协议和接口
+ `document.location`返回浏览器的原生对象`Location`, 它提供URL相关的信息和操作方法. 还可以通过`window.location`得到这个对象
+ `document.lastModified`返回一个表示当前文档最后修改时间的字符串. 不同浏览器返回的日期格式不一定一样. 若页面上有JavaScript生成的内容则返回当前时间
+ `document.title`获取当前文档的标题, 默认返回&lt;title&gt;节点. 该属性可写
+ `document.characterSet`返回当前文档的编码
+ `document.referrer`返回一个表示当前文档的访问者来自哪里的字符串. 它和http头信息中的`referer`字段一致. 若无法获取访问者来源(如用户直接输入网址)则返回""(空字符串)
+ `document.dir`返回表示文字方向的字符串, 有rlt表示文字从右到左, ltr文字从左到右
+ `document.compatMode`返回浏览器处理文档的模式, 有向后兼容模式`BackCompat`, 严格模式`CSS1Compat`. 一般网页有&lt;DOCTYPE&gt;声明则都为严格模式

## 文档状态属性
+ `document.hidden`返回布尔值表示当前页面是否可见, 若不可见则返回`true`. 窗口的最小化, 浏览器切换窗口都会导致页面不可见
+ `document.visiblityState`返回文档的可见状态. 它有四种可能:
`visible`：页面可见。注意，页面可能是部分可见，即不是焦点窗口，前面被其他窗口部分挡住了。
`hidden`： 页面不可见，有可能窗口最小化，或者浏览器切换到了另一个 Tab。
`prerender`：页面处于正在渲染状态，对于用于来说，该页面不可见。
`unloaded`：页面从内存里面卸载了。
+ `document.readyState`返回当前文档的状态, 有三种值
`loading`：加载 HTML 代码阶段（尚未完成解析）
`interactive`：加载外部资源阶段
`complete`：加载完成
浏览器加载HTML文档过程如下:
1浏览器开始解析 HTML 文档，+ `document.readyState`属性等于`loading`。
2浏览器遇到 HTML 文档中的&lt;script&gt;元素，并且没有`async`或`defer`属性，就暂停解析，开始执行脚本，这时`document.readyState`属性还是等于`loading`。
3HTML 文档解析完成，`document.readyState`属性变成`interactive`。
4浏览器等待图片、样式表、字体文件等外部资源加载完成，一旦全部加载完成，`document.readyState`属性变成`complete`。

## 其他属性
+ `document.cookie`用来操作`Cookie`对象
+ `document.designMode`控制当前文档是否可编辑, 属性值为`on`或者`off`, 默认为`off`. 这个属性常用在所见即所得的编辑器
+ `document.implementation`返回一个`DOMImplementation`对象, 这个对象有三个方法
`DOMImplementation.createDocument()`：创建一个 XML 文档。
`DOMImplementation.createHTMLDocument()`：创建一个 HTML 文档。
`DOMImplementation.createDocumentType()`：创建一个 `DocumentType` 对象。

# 方法
+ `document.open()`方法清除当前文档的内容并使文档处于可写状态. 
`docuemnt.close()`关闭`open()`方法打开的文档
+ `document.write()`向文档写入内容, 内容也会被当做html代码解析,但不会转义. 这个方法一定在`open()`和`close()`方法之间.
如果页面已经解析完成（`DOMContentLoaded`事件发生之后），再调用write方法，它会先调用open方法
+ `document.writeln()`方法与write方法用法一致,不同的是这个方法在写入内容的末尾加上换行符. 可在显示上并不换行, 因为html会将连续的多个空格,换行符等解析为一个空格.
+ `document.querySelector()`接受一个css选择器作为参数, 返回满足条件的第一个节点, 没有返回`null`
+ `document.querySelectorAll()`也接受一个css选择器作为参数, 但是返回满足条件的所有节点, 返回值为`NodeList`对象
`querySelector`和`querySelectorAll`不支持伪元素选择器和伪类, 返回的结果不是动态集合
+ `document.getElementsByTagName()`接受标签名做参数返回满足条件的元素节点, 返回值是`HTMLCollection`实例, 实时反映文档节点变化, 可以在任意元素节点调用
+ `document.getElementsByClassName()`接受类名做参数返回满足条件的元素节点, 返回值也是
`HTMLCollection`实例,实时反映文档节点变化, 可以在任意元素节点调用
+ `document.getElementsByName()` 接受的参数是一个属性名, 返回拥有这个属性名的元素节点, 注意返回值是`NodeList`实例, 因为属性名相同的元素可能不止一个
+ `document.getElementById()` 接受一个id参数,返回这个id所在的元素, 这是个单个节点. 注意这个方法只能在`document`对象上使用, 其他元素节点不可用
+ `document.elementFromPoint`方法接受连个参数x, y. 返回位于页面指定位置最上层的元素
+ `document.elementsFromPoint()`返回一个数组，成员是位于指定坐标（相对于视口）的所有元素节点。
+ `document.caretPositionFromPoint()`返回一个`CaretPosition`对象, 用于确定光标点在文本对象内部的具体位置, 它有两个属性
`CaretPosition.offsetNode`：该位置的节点对象
`CaretPosition.offset`：该位置在offsetNode对象内部，与起始位置相距的字符数
+ `document.createElement()`方法用来生成元素节点，并返回该节点. 参数为标签名, 不可以有尖括号
+ `document.createTextNode()`用于生成文本节点并返回该节点, 参数为文本节点的内容. 该方法不对单双引号转义
+ `document.createAttribute()`生成新的属性节点并返回, 参数为属性名
+ `document.createComment()`用于生成注释节点并返回
+ `document.createDocumentFragment()`生成一个空的文档片段对象, 即DocumentFragment实例, 它不属于当前文档
+ `document.createEvent()`方法用于生成一个Event实例
+ `document.addEventListener()`用于添加时间监听函数
+ `document.removeEventListener()`移除事件监听函数
+ `document.dispatchEvent()`用于触发事件
+ `document.hasFocus()`返回一个表示当前文档中是否有元素激活或者获得焦点的布尔值. 若有元素被激活或者获得焦点则返回true. 注意有焦点的文档必定被激活, 激活的文档未必有焦点
+ `document.adoptNode()`，`document.importNode()`都用于移动节点
+ `document.createNodeIterator()`方法返回一个子节点遍历器, 它是NodeFilter实例。`document.createNodeIterator()`方法第一个参数为所要遍历的根节点，第二个参数为所要遍历的节点类型，这里指定为元素节点（`NodeFilter.SHOW_ELEMENT`）
几种主要的节点类型写法如下
所有节点：`NodeFilter.SHOW_ALL`
元素节点：`NodeFilter.SHOW_ELEMENT`
文本节点：`NodeFilter.SHOW_TEXT`
评论节点：`NodeFilter.SHOW_COMMENT`

+ `document.createTreeWalker`方法返回一个 DOM 的子树遍历器, 但它时`TreeWalker`实例. 使用方法和`createNodeIterator()`类似
+ `document.getSelection()`指向`window.getSelection()`方法
