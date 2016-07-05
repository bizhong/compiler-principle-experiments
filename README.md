# 《编译原理》实验（Compiler Principle Experiments）

JavaScript 实现《编译原理》实验：词法分析和算术表达式语法分析。

## 概览

- [词法分析](#词法分析)
- [语法分析](#语法分析)

## 词法分析

### 实验目的

通过编写一个具体的词法分析程序，加深对词法分析原理的理解。掌握在对程序设计语言源程序进行扫描过程中将其分解为各类单词的词法分析方法。

编制一个读单词过程，从输入的源程序中，识别出各个具有独立意义的单词，即基本保留字（关键字）、标识符、常数、运算符、分隔符五大类。依次输出各个单词的内部编码及单词符号自身值。

### 实验要求

基本要求

- 要求用可视化编程工具编写；要求有界面（即一般 windows 下应用程序界面）。输入为 C 语言源代码。

- 识别保留字：`if`、`int`、`for`、`while`、`do`、`return`、`break`、`continue` 等等；单词种别码为 1。

- 其他的都识别为标识符；单词种别码为 2。

- 常数为无符号数；单词种别码为 3。

- 运算符包括：`+`、`-`、`*`、`/`、`=`、`>`、`<` 等；可以考虑更复杂情况 `>=`、`<=`、`!=` ；单词种别码为 4。

- 分隔符包括：`,`、`;`、`(`、`)`、`{`、`}` 等；单词种别码为 5。

扩充和修改

- 运算符能处理一元运算符、二元运算符、三元运算符。

- 能处理注释，单行注释和多行注释。例如：“`/*lex*/`”或者“`// lex`”等。

- 能处理一些特殊 C 程序代码输入。例如：“`20.35`”、“`123+++`”等。

- JavaScript 实现，增加“打开文件”、“保存文件”功能。

### 状态转换图

- 识别基本保留字和标识符的状态转换图：

![识别基本保留字和标识符的状态转换图][1]

结束标志：空格或者不是字母且不是数字。

查基本保留字表：存在，flag = 1，是基本保留字；否则，flag = 2，是标识符。

- 识别常数（整数、浮点数）的状态转换图：

![识别常数（整数、浮点数）的状态转换图][2]

flag = 3

- 识别运算符的状态转换图：

![识别运算符的状态转换图][3]

flag = 4

“`/`”例外，得单独分析。“`/`”有可能是注释的开始。

- 识别分隔符的状态转换图：

![识别分隔符的状态转换图][4]

flag = 5

- 识别注释的状态转换图：

![识别注释的状态转换图][5]

### 程序流程图

![程序流程图][6]

### 程序界面

- 点击打开“lexical-analysis”文件夹下的“index.html”文件。在 Chrome 浏览器中的界面如下图：

![程序界面1][7]

点击“打开文件”或者在输入框中输入 C 语言源程序代码。下面以点击“打开文件”为例。

- 点击“打开文件”，选择“test.c”文件，点击“打开(O)”。

![程序界面2][8]

“test.c”文件的 C 语言源程序代码如下：

![程序界面3][9]

![程序界面4][10]

- 点击“词法分析”，右侧依次输出各个单词的内部编码及单词符号自身值。

![程序界面5][11]

- 如果要将词法分析结果保存下来，点击“保存结果”，在 Chrome 浏览器最下角会有下载记录。要查看下载文件，点击列表按钮，选择“打开(O)”。

![程序界面6][12]

下载文件的内容如下：

![程序界面7][13]

## 语法分析

### 实验目的

根据某一文法编制调试递归下降分析程序，以便对任意输入的符号串进行分析。本次实验的目的主要是加深对递归下降分析法的理解。

注：也可以采用预测分析方法、算符优先分析方法来进行分析。具体参照课本上的说明。

### 实验要求

基本要求

- 对算术表达式文法，用递归下降分析法（或预测分析方法、算符优先分析方法等）对任意输入的符号串进行分析，如合法给出相应信息，如果不合法，最好能给出在哪个产生式出现的问题。

- 算术表达式至少包含 `+`、`-`、`*`、`/`、`(`、`)`。例如：“`i1 + i2 * ( 34 - i3 / 2 )`”。

- 提示：先做词法分析，然后语法分析。

扩充和修改

- 对算术表达式文法，选择用算符优先分析方法。

- JavaScript 实现。

### 程序流程图

![程序流程图][14]

### 程序界面

- 点击打开“syntax-analysis”文件夹下的“index.html”文件。在 Chrome 浏览器中的界面如下图：

![程序界面1][15]

- 在输入框中输入合法的算术表达式。例如：“`i1 + i2 * ( 34 - i3 / 2 )`”。

![程序界面2][16]

- 点击“语法分析”，输入框下面依次输出符号栈 S、关系、输入流和最左素短语。最后给出相应的语法分析结果信息：“**算术表达式合法。**”。

![程序界面3][17]

- 在输入框中输入不合法的算术表达式。例如：“`a1 + a2 ) * 22`”。

![程序界面4][18]

- 点击“语法分析”，输入框下面依次输出符号栈 S、关系、输入流和最左素短语。最后给出相应的语法分析结果信息：“**算术表达式不合法，在 ) 时出现问题。**”。

![程序界面5][19]

  [1]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/lexical-analysis/state-transition-diagram/1.png
  [2]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/lexical-analysis/state-transition-diagram/2.png
  [3]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/lexical-analysis/state-transition-diagram/3.png
  [4]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/lexical-analysis/state-transition-diagram/4.png
  [5]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/lexical-analysis/state-transition-diagram/5.png
  [6]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/lexical-analysis/program-flow-diagram/1.png
  [7]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/lexical-analysis/application-interface/1.png
  [8]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/lexical-analysis/application-interface/2.png
  [9]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/lexical-analysis/application-interface/3.png
  [10]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/lexical-analysis/application-interface/4.png
  [11]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/lexical-analysis/application-interface/5.png
  [12]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/lexical-analysis/application-interface/6.png
  [13]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/lexical-analysis/application-interface/7.png
  [14]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/syntax-analysis/program-flow-diagram/1.png
  [15]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/syntax-analysis/application-interface/1.png
  [16]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/syntax-analysis/application-interface/2.png
  [17]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/syntax-analysis/application-interface/3.png
  [18]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/syntax-analysis/application-interface/4.png
  [19]: https://github.com/basfed/compiler-principle-experiments/blob/master/images/syntax-analysis/application-interface/5.png