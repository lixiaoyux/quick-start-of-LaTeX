## LaTeX 入门教程

<span id="t"></span>

*写在前面：这是笔者学习LaTeX时记下的些许学习笔记，偏向于基础和常用性，用于快速入门，但还有部分内容没有涉及，我也会在后续的学习中保持补充更新。若读者需要深入系统地学习LaTeX，推荐阅读相关文档。*

<span id="hw"></span>

#### 1. Hello World!

---

```
\documentclass{article}
\begin{document}
Hello World!
\end{document}
```

第一行调用`article`文档类(对应模板)。

```
\documentclass[11pt,twosides,a4paper]{article}
```

上述命令指定LaTeX使用**论文**版式，11磅字体，A4纸张。

关于{}中的可选项，有以下选择：

---

`article`：排版程序文档等

`report`：排版短片书籍、博士论文等。

`book`：排版书籍。

---

`%`用于注释标记。

```
% this is annotation
```

`\begin`和`\end`构成一个**环境**，必须成对出现。

```
\begin{}
...
\end{}
```

**如何实现中文输出**

```
\documentclass[UTF8]{ctexart}
\begin{document}
你好，World!
\end{document}
```

指示以`UTF-8`编码保存。

*[Back to top](#t)

#### 2. Some Information

---

在`\documentclass{}`和`\begin{}`之间(正文之前，即**导言区**)，可加入文档信息，e.g. **作者、标题、日期**等信息。

```
\documentclass[UTF8]{ctexart}
\title{标题}
\author{Li xy}
\date{\today}
\begin{document}
\maketitle
你好，World!
\end{document}
```

其中`\maketitle`用于展示前文设置的文档内容，若注释掉该行，则设置内容不显示。

在`\maketitle`后可加入`\tablecontents`，编译两次后显示目录及其内容。此处注意`\maketitle`和`\tablecontents`的位置顺序，若调换顺序，则部分内容不能正常显示。

若想要将中文的`目录`(default)更换为英文的`Content`，使用`\renewcommand\contentsname{Content}`。

关于输出格式，若想要输出**换行**，则需要使用两个换行，对于一个换行和多个空格，LaTex视作一个空格处理。

*[Back to top](#t)

#### 3. Section and Paragraph

---

这一节对于组织编排十分重要，`article`和`ctexart`中有五个控制序列：

+ `\section{}`, e.g. **1.**(居中)，{}内为标题内容。
+ `\subsection{}`, e.g. **1.1**，{}内为标题内容。
+ `\subsubsection{}`, e.g. **1.1.1**，{}内为标题内容。
+ `\paragraph{}`，{}可用于段落开头。
+ `\subparagraph{}`，{}可用于段落开头。

**脚注**:

使用命令`\footnote{}`可以把脚注内容排印于当前页的页脚位置

*[Back to top](#t)

#### 4. Mathematics

---

为了使用数学功能，需要使用`\usepackage{package_name}`在导言区加载`amsmath`宏包：

```
\usepackage{amsmath}
```

具体格式同**markdown**，不过建议对于行间公式插入使用`$...$`，对于行间公式插入使用`\[ ... \]`作为一个数学环境(不带编号)。若需要带编号的数学公式，对于单行公式，可使用

```
\begin{equation}
a+b=c
\end{equation}
```

对于多行公式，可使用

```
\begin{equation}
	\begin{aligned}
	a+b &= c\\
	c+d+e &= \frac{1}{2}
	\end{aligned}
\end{equation}
```

或者

```
\begin{align}
a+b &= c\\
c+d+e &= \frac{1}{2}
\end{align}
```

其中，`\\`用于换行，`&`是对齐符号。

对于分段函数，可使用`cases`次环境。

```
\[
y = \begin{cases}
-x,\quad x\le 0\\
x, \quad x>0
\end{cases}
\]
```

其中，`\quad`是间隔。

关于常用的公式，请查询[相关资料](https://blog.csdn.net/caiandyong/article/details/53351737)。

*[Back to top](#t)

#### 5. Image and Table

---

插入图片可以使用`graphicx`宏包中的`\includegraphics`命令。

```
\documentclass{article}
\usepackage{graphicx}
\begin{document}
\includegraphics{example.jpg}
\end{document}
```

若需要控制图片的缩放，则添加参数:

```
\includegraphics[width=0.8\textwidth]{example.jpg}
```

上例将图片宽度缩放至**当前页面宽度**的百分之八十。

表格功能使用`tabular`环境，使用`\hline`表示横线，`|`表示竖线，`&`来分列，用`\\`来换行。对于居左、居中、居右等对齐方式，分别用`l`，`c`，`r`表示。

```
\begin{tabular}{|l|c|r}
  \hline
  A& B& C\\
  \hline
  C& D& E\\
  \hline
\end{tabular}
```

若希望使表格居中，则使用`center`环境。

```
\begin{center}
  \begin{tabular}
  ...
  \end{tabular}
\end{center}
```

*[Back to top](#t)

#### 6. Layouts

---

设置**页边距**，可以使用`geometry`宏包。例如下述命令将设置纸张长度、宽度，下上左右边距。

```
\usepackage{geometry}
\geometry{papersize={20cm,15cm}}
\geometry{left=1cm,right=2cm,top=3cm,bottom=4cm}
```

设置页眉页脚，可以使用`fancyhdr`宏包。

```
\usepackage{fancyhdr}
\pagestyle{fancy}
\lhead{\author}			% 页眉左
\chead{}
\rhead{}				% 页眉右
\lfoot{}				% 页脚左
\cfoot{}
\rfoot{}
```

调整行间距，可以使用`setpace`宏包。

```
\usepackage{setpace}
\onehalfspacing			% 设置行距为字号大小的1.5倍
```

*[Back to top](#t)