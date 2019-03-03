# 1. 区块元素
## 1.1 标题
### 1.1.1 Setext形式
```markdown
h1 1号字体
====
h2 2号字体
----
```
  
### 1.1.2 atx形式
```markdown
### h3 三号字体
#### h4 四号字体
或者
##### h5 五号字体 #####
###### h6 六号字体 #######
```
  
## 1.2 段落和换行
1.段落前后必须是空行:  
空行是行内什么都没有或者只有空白符（空格或者制表符） 
相邻两行文本，如果中间没有空行，则会显示在一行内（换行符会被转换成空格）

2.如果需要在段内加入换行（`<br />`）：  
可以在前一行的末尾加入至少两个空格，再换行写其他文字


## 1.3 区块引用
### 1.3.1 单行引用
markdown语法:
```markdown
>引用内容
```
显示结果:
>引用内容

### 1.3.2 多行引用
markdown语法:
```markdown
>多行引用  
>可在每行前加`>`
```
显示结果:
>多行引用  
>可在每行前加`>`  

### 1.3.3 嵌套引用
markdown语法:
```markdown
>也可以在引用中
>>使用嵌套的引用
```
显示结果:
>也可以在引用中
>>使用嵌套的引用

## 1.4 列表
### 1.4.1 无序列表
markdown语法:
```markdown
* 可以使用 `*` 作为标记
+ 也可以使用 `+`
- 或者 `-`
```
显示结果:
* 可以使用 `*` 作为标记
+ 也可以使用 `+`
- 或者 `-`

### 1.4.2 有序列表
markdown语法:
```markdown
1. 有序列表以数字和 `.` 开始；
3. 数字的序列并不会影响生成的列表序列；
4. 但仍然推荐按照自然顺序（1.2.3...）编写。
```
显示结果:
1. 有序列表以数字和 `.` 开始；
3. 数字的序列并不会影响生成的列表序列；
4. 但仍然推荐按照自然顺序（1.2.3...）编写。

### 1.4.3 嵌套列表
markdown语法:
```markdown
1. 第一层
    + 1_1
    + 1_2
2. 无序列表和有序列表可以随意相互嵌套
    1. 2_1
    2. 2_2
  
* 1
    * 1_1
        * 1_1_1
    * 1_2
        * 1_2_1
        * 1_2_2
* 2
    * 2_1
    * 2_2
```
显示结果:
1. 第一层
    + 1_1
    + 1_2
2. 无序列表和有序列表可以随意相互嵌套
    1. 2_1
    2. 2_2
  
* 1
    * 1_1
        * 1_1_1
    * 1_2
        * 1_2_1
        * 1_2_2
* 2
    * 2_1
    * 2_2
            
## 1.5 代码区块
markdown语法:
```markdown
这是一个普通段落：

    这是一个代码区块。
    
Here is an example of AppleScript:

    tell application "Foo"
        beep
    end tell
```
显示结果:  
这是一个普通段落：

    这是一个代码区块。
    
Here is an example of AppleScript:

    tell application "Foo"
        beep
    end tell

## 1.6 分隔线
1. 可以在一行中使用三个或更多的 *、- 或 _ 来添加分隔线（`<hr>`）:  
2. 多个字符之间可以有空格（空白符），但不能有其他字符

markdown语法:
```markdown
***
------
___
```
显示为:
***
------
___

# 2 区段元素
## 2.1 链接
### 2.1.1 行内式
格式为`[link text](URL 'title text')`  
1.普通链接:
```markdown
[Google](http://www.google.com/)
```
显示结果:[Google](http://www.google.com/)  
2.指向本地文件的链接:
```markdown
[icon.png](./images/icon.png)
```
显示结果:[icon.png](./images/icon.png)  
3.含有title的链接:
```markdown
[Google](http://www.google.com/ "Google")
```
显示结果:[Google](http://www.google.com/ "Google")
>title 使用 ' 或 " 都是可以的。

### 2.1.2 参考式
markdown语法:
```markdown
[Google][link]

[link]: http://www.google.com/ "Google"

[Baidu][]

[Baidu]: https://www.baidu.com/ "Baidu"

```
显示结果:  
[Google][link]

[link]: http://www.google.com/ "Google"

[Baidu][]

[Baidu]: https://www.baidu.com/ "Baidu"
>第二个中括号的内容是识别符(可省略)，可以是字母、数字、空白或标点符号，不区分大小写  
>注意两行之间有一行空行

## 2.2 强调
1.使用 * * 或 _ _ 包括的文本会被转换为 <em></em> ，通常表现为斜体：  
markdown语法:
```markdown
这是用来 *演示* 的 _文本_
```
显示结果:  
这是用来 *演示* 的 _文本_  
2.使用 ** ** 或 __ __ 包括的文本会被转换为 <strong></strong>，通常表现为加粗：  
markdown语法:
```markdown
这是用来 **演示** 的 __文本__
```
显示结果:  
这是用来 **演示** 的 __文本__  
3.用来包括文本的 * 或 _ 内侧不能有空白，否则 * 和 _ 将不会被转换（不同的实现会有不同的表现）：  
markdown语法:
```markdown
这是用来 * 演示* 的 _文本 _
```
显示结果:  
这是用来 * 演示* 的 _文本 _               

4.如果需要在文本中显示成对的 * 或 _，可以在符号前加入 \ 即可：  
markdown语法:
```markdown
这是用来 \*演示\* 的 \_文本\_
```
显示结果:  
这是用来 \*演示\* 的 \_文本\_  
5.*、**、_ 和 __ 都必须 成对使用 。

## 2.3 代码
标记一小段行内代码，用反引号`` ` ``，如`print`

使用` ``` ` 可引入代码段如:

``````
```python
class A:
    def __init__(self):
        self.name = 'myname'
        self.age = 23
    
    def __str__(self):
        return f'姓名:{self.name}, 年龄:{self.age}'
```
``````
则会显示
```python
class A:
    def __init__(self):
        self.name = 'myname'
        self.age = 23
    
    def __str__(self):
        return f'姓名:{self.name}, 年龄:{self.age}'
```

## 2.4 图片
插入图像与超链接语法基本一致，只是在前面多加一个`!`
### 2.4.1 行内式
markdown语法:
```markdown
![GitHub](https://github.com/olewaLdeisi/blog/blob/master/Me.jpg)
```
显示结果:  
![GitHub](https://github.com/olewaLdeisi/blog/blob/master/Me.jpg)
### 2.4.2 参考式
markdown语法:
```markdown
![GitHub][github]

[github]: ../Me.jpg "Me"
```
显示结果:  
![GitHub][github]

[github]: ../Me.jpg "Me"

# 3 其他
## 3.1 反斜杠
markdown语法:
```markdown
\*literal asterisks\*
```
显示结果:  
\*literal asterisks\*
Markdown支持以下符号前加上反斜杠来帮忙插入普通的符号:
```markdown
\   反斜线
`   反引号
*   星号
_   底线
{}  花括号
[]  方括号
()  括弧
#   井字号
+   加号
-   减号
.   英文句点
!   惊叹号
```
## 3.2 自动链接
使用 <> 包括的 URL 或邮箱地址会被自动转换为超链接：
markdown语法:
```markdown
<http://www.google.com/>

<123@email.com>
```
显示结果:  
<http://www.google.com/>

<123@email.com>