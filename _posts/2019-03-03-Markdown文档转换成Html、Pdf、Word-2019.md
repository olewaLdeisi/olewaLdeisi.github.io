# 1.转换成HTML文档
## MdCharm
选择 'File', 'Export to...'，勾选 'HTML', 点击 'Browser...' 选择导出目录并输入导出的文件名，点击 'OK'，即可将当前的 Markdown 文档转换为 HTML 文档。

如果不满意 HTML 文档的样式，可以在设置中自定义 CSS。
  
## Pandoc
参考 [Installing](http://pandoc.org/installing.html)安装Pandoc  
打开命令行，进入文档所在目录：  
``````
cd /path/to/file/
``````
执行下面的命令，将 Markdown 转换为 HTML：  
``````
pandoc -o hello.html hello.md
``````
>默认的转换，只是将 Markdown 内容转换为 HTML 标签，所以只能看到浏览器的默认样式。  

可以执行下面的命令，为导出的 HTML 添加自定义样式：
``````
pandoc -o hello.html -c style.css hello.md
``````
>style.css 仍然是以 \<link\> 的方式关联到 HTML 文档中的，所以在发布的时候需要将 CSS 一同发布出去。

# 2.转换成PDF文档
## MdCharm
与导出 HTML 文档类似，选择 'File', 'Export to...'，勾选 'PDF', 点击 'Browser...' 选择导出目录并输入导出的文件名，点击 'OK'，即可将当前的 Markdown 文档转换为 PDF 文档。

如果不满意 PDF 文档的样式，可以在设置中自定义 CSS。
## Pandoc
使用 Pandoc 导出 PDF 文档，需要先安装某个 LaTeX 引擎（参考 Creating a PDF）。然后执行命令：
``````
pandoc -o hello.pdf hello.md
``````
当然，也可以通过 -c style.css 来指定样式文件。
## Chrome
在将 Markdown 转换为 HTML 文档 之后，可以通过 Chrome 浏览器 打开它。选择 '打印'（Ctrl+P），然后更改 '目标打印机' 为 '另存为 PDF'，再进行一些设置后，即可保存为 PDF 文档。
# 3.转换成Word文档
## 复制粘贴
在导出为 HTML 文档之后，可以（在浏览器中）手动复制 HTML 页面的内容，然后粘贴到 Word 文档中，保存即可。
## Pandoc
执行下面的命令，即可将 Markdown 文档转换为 Word 文档：
``````
pandoc -o hello.docx hello.md
``````