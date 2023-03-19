[TOC]

# 1 XML

XML指可扩展性标记语言(eXtensible Markup Language) XML被设计用来传输和存储数据

示例:

```
<?xml version="1.0" encoding="utf-8"?>
<note>
    <to>Tove</to>
    <from>Jani</from>
    <heading>Reminder</heading>
    <body>Don't forget me this weekend!</body>
</note>

```

# 2 XML树结构

XML 文档形成了一种树结构，它从"根部"开始，然后扩展到"枝叶"。

## 2.1 一个XML文档实例

XML 文档使用简单的具有自我描述性的语法：

    <?xml version="1.0" encoding="UTF-8"?>
    <note>
        <to>Tove</to>
        <from>Jani</from>
        <heading>Reminder</heading>
        <body>Don't forget me this weekend!</body>
    </note>

第一行`<?xml version="1.0" encoding="utf-8"?>`是XML的声明。它定义了XML所使用的版本（1.0）和所使用的编码方式（utf-8）

第2行`<note>`描述的是文档的根目录

接下来的4行，描述的根的4个子元素（to、from、heading和boby）

    <to>Tove</to>
    <from>Jani</from>
    <heading>Reminder</heading>
    <body>Don't forget me this weekend!</body>

最后一行`</note>`定义根元素的结尾

## 2.2 XML文档形成的一种树结构

XML 文档必须包含根元素。该元素是所有其他元素的父元素。
XML 文档中的元素形成了一棵文档树。这棵树从根部开始，并扩展到树的最底端。

所有的元素都可以有子元素：

    <root>
    <child>
    <subchild>.....</subchild>
    </child>
    </root>

我们可以用父、子以及同胞等术语用于描述元素之间的关系。
父元素拥有子元素。相同层级上的子元素成为同胞（兄弟或姐妹）。

所有的元素都可以有文本内容和属性（类似 HTML 中）。

实例:

    <?xml version="1.0" encoding="utf-8"?>
    <bookstore>
        <book category="COOKING">
            <title lang="en">Everyday Italian</title>
            <author>Giada De Laurentiis</author>
            <year>2005</year>
            <price>30.00</price>
        </book>
        <book category="CHILDREN">
            <title lang="en">Harry Potter</title>
            <author>J K. Rowling</author>
            <year>2005</year>
            <price>29.99</price>
        </book>
        <book category="WEB">
            <title lang="en">Learning XML</title>
            <author>Erik T. Ray</author>
            <year>2003</year>
            <price>39.95</price>
        </book>
    </bookstore>

我们可以将它转换为树模型：

<此处有张图>

实例中的根元素是` <bookstore>`。文档中的所有 `<book> `元素都被包含在 `<bookstore> `中。

`<book> `元素有4个子元素：`<title>、<author>、<year>、<price>`

# 3 XML语法规则

*   XML文档必须有根元素
    XML必须包含有根元素，它是所有其他元素的父元素。
    \*XML声明是文件的可选部分，如果存在需要放在文档第一行

*   所有的XML元素都必须有一个关闭标签

*   XML标签对大小写敏感

*   XML必须正确嵌套

*   XML属性值必须加引号

*   实体引用
    在XML中，一些字符存在特俗含义，把这些字符放在xml元素中会反生错误，为了避免，可以使用实体引用来代替：
    在xml中，有5个预定义的实体引用：

| 实体引用 | 字符 | 说明           |
| -------- | ---- | -------------- |
| \&lt     | <    | less than      |
| \&gt     | >    | greater than   |
| \&amp    | &    | ampersand      |
| \&apos   | '    | apostrophe     |
| \&quot   | "    | quotation mark |

*   XML中注释
    `<!-- this is a comment -->`
*   XML中，空格会被保留

# XML命名规则

XML 元素必须遵循以下命名规则：

*   名称可以包含字母、数字以及其他的字符
*   名称不能以数字或者标点符号开始
*   名称不能以字母 xml（或者 XML、Xml 等等）开始
*   名称不能包含空格
*   可使用任何名称，没有保留的字词。

# XML JavaScript

## XMLHttpRequest对象

XMLHttpRequest对象用于在后台与服务器交换数据。
XMLHttpRequest对象是开发者的梦想，因为您能够：

*   在不重新加载页面的情况下更新网页
*   在页面已加载后从服务器请求数据
*   在页面已加载后从服务器接收数据
*   在后台向服务器发送数据

## 创建一个XMLHttpRequest对象

所有现代浏览器（IE7+、Firefox、Chrome、Safari 和 Opera）都有内建的 XMLHttpRequest 对象。
创建 XMLHttpRequest 对象的语法：

    xmlhttp = new XMLHttpRequest();

旧版本的Internet Explorer（IE5和IE6）中使用 ActiveX 对象：

    xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");

## XML解析器（Parser）

所有现代浏览器都有内建的 XML 解析器。
XML 解析器把 XML 文档转换为 XML DOM 对象 (可通过 JavaScript 操作的对象)。

### 解析XML文档

    if(window.XMLHttpRequest){
        //code for IE7+, Firefox, Chrome, Opera, Safari
        xmlhttp=new XMLHttpRequest();
    }else{
        //code for IE6, IE5
        xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
    }
    xmlhttp.open("GET","book.xml",false);
    xmlhttp.send();
    xmlDoc=xmlhttp.responseXML;

### 解析XML字符串

    txt="<bookstore><book>";
    txt=txt+"<title>Everyday Italian</title>";
    txt=txt+"<author>Giada De Laurentiis</author>";
    txt=txt+"<year>2005</year>";
    txt=txt+"</book></bookstore>";
    
    if (window.DOMParser)
    {
        parser=new DOMParser();
        xmlDoc=parser.parseFromString(txt,"text/xml");
    }
    else // Internet Explorer
    {
        xmlDoc=new ActiveXObject("Microsoft.XMLDOM");
        xmlDoc.async=false;
        xmlDoc.loadXML(txt); 
    }

注释：Internet Explorer 使用 loadXML() 方法来解析 XML 字符串，而其他浏览器使用 DOMParser 对象。