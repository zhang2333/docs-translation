# Visual Studio Code之进阶编辑

全文翻译自[官方Docs][link-1]

Visual Studio Code有着同类代码编辑器一样的标准功能，此外还有一些我们精心设计的独到而有趣之处，相信你会喜欢上它。这一篇将着重为你介绍编辑器一些值得注意的地方。

## 括号匹配

光标一旦临近括号时，左右括号都将被匹配到并高亮显示出来。即便是像php这样的嵌入式语言，括号仍能够被匹配到。如下图：

![括号匹配][1]

> 提示：括号被匹配到之后可以`Ctrl+Shift+]`来跳转光标。

## 多重光标与多重选择

VS Code支持使用多重光标的编辑操作，你可以`Alt+单击`来添加多个光标。每个光标的操作都将是独立的，且仅作用于它所在的位置。使用`Ctrl+Alt+Up`或`Ctrl+Alt+Down`可以快捷地在当前光标的上方或下方添加新的光标。

![多重光标][2]

`Ctrl+D`将选中当前光标所在的词，如果是在选中该词的情况下使用，则会同时选中该词下一次出现的地方（译者注：即多重选择）。如果某次的匹配并不是你想要选择的，`Ctrl+K`再`Ctrl+D`可以跳过这次匹配进而匹配下一个。

> 提示：`Ctrl+Shift+L`可以选中文件中所有该词出现的地方。

## 扩大或缩小选择范围

使用`Shift+Alt+Right`或`Shift+Alt+Left`快速地扩大或缩小选择范围（适应所有语言）。

效果如下图所示:

![扩大选择范围][3]

## IntelliSense 智能感应

我们同样支持单词补全功能，对于更丰富的语言，像JavaScript、JSON、HTML、CSS、Less、Sass、C#以及TypeScript，我们将提供更为强大的IntelliSense体验。当你拼写一个单词的时候，IntelliSense会在光标的位置弹出一个补全建议框（我们称呼它为贴心24小时IntelliSense ），或者你可以`Ctrl+Space`来手动打开它。可以使用`.`、`Tab`、`Enter`来确认某个补全建议，当然你也可以自定义这些快捷键。

![IntelliSense][4]

> 提示：补全建议是支持驼峰命名的，所以你可以输入方法名的首字母来匹配补全建议。比如输入"wl"将可以匹配到"WriteLine"。

> 提示：IntelliSense可以通过`editor.quickSuggestions`和`editor.suggestOnTriggerCharacters`来设置。

## 参数提示

在JavaScript、TypeScript或者C#的语法中，输入一个方法调用之后将弹出相应的参数提示框。你可以使用`Up`或`Down`在不同的重载方法中选择你需要的参数提示。

![参数提示][5]

## Snippet与Emmet

我们不但提供内置的跨语言Snippet，还支持[Emmet][link-2]功能。你可以在HTML、Razor、CSS、Less、Sass、XML或Jade中对Emmet简写语句使用`Tab`来补全代码。

![Emmet][6]

（查看[Emmet cheat sheet][link-3]中的语法示例）

你同样可以定义你自己的Snippet：打开`File | Preferences`下的`User Snippets`，选择语言以指定使用相应的Snippet。欲知更多请查看文档中的[自定制章节][link-4]。

## Go to Definition

如果是一种[支持该功能的语言][link-5]，你可以在一个变量上使用`F12`跳至它被定义的地方。

If you press Ctrl and hover over a symbol, a preview of the declaration will appear:
如果按住`Ctrl`并用鼠标悬停在一个变量上，就会出现声明该变量地方的预览：

![Ctrl+鼠标悬停][7]

> 提示：使用`Ctrl+单击`可以跳至变量被定义的地方，或者使用`Ctrl+Alt+单击`打开定位在该变量被定义位置的侧边新窗口。

## Goto Symbol

在一个文件中使用`Ctrl+Shift+O`可以在Symbol（译者注：经测试，这里指的应该是全局变量和函数）间导航。输入`:`可以将Symbol分类排列，接着`Up`或`Down`就可以定位了。

![Goto Symbol][8]

## 通过名称定位Symbol

在C#和TypeScript中，使用`Ctrl+T`可以快速在多个文件中定位Symbol。输入Symbol的首字母，无需在意哪个文件包含它，按下`Enter`即可定位到定义的位置。

![通过名称定位Symbol][9]

## Gutter indicators 侧边指示器

如果打开的文件夹同时是一个Git仓库，在对其中文件进行修改时，VS Code将会在**编辑器**左侧显示出很有帮助的指示标记。

* 红色三角指示有被删除的行（译者注：被删除的是一行或多行）
* 绿条指示新增的行
* 蓝条指示有所修改的行

![侧边指示器][10]

## Peek 先睹为快

在茫茫码海中想要快速检查某个变量是极其麻烦的，为此我们特意制作了解决这个烦恼的**Peek编辑窗**。当你执行引用搜索（可以通过`Shift+F12`）或者查看定义位置（可以通过`Alt+F12`）的操作后，**Peek编辑窗**将显示并悬停在该行下：

![Peek编辑窗][11]

> 提示：你可以在**Peek编辑窗**中不同的变量引用之间来回切换，如果有需要，你甚至可以直接在**Peek编辑窗**中做代码修改！

> 提示：单击**Peek编辑窗**上的文件名或双击右侧引用列表中的某个引用，**Peek编辑窗**之下的**编辑器**将直接定位到该引用所在位置。

## 鼠标悬停

鼠标悬停可以显示出一些很有用的信息，比如某个变量的类型，又或者，在CSS中，悬停在某个选择器之上，将显示被匹配到的HTML元素（译者注：当然，鼠标悬停远不止这两个作用，更多的用法可以多尝试尝试自行摸索出来）：

![CSS选择器上的鼠标悬停][12]


## 引用信息

C#支持行上标记引用的信息，并且是实时更新的，效果如下图：

![引用信息][13]

> 提示：单击这些标记信息会直接调用Find References操作。

> 提示：通过配置文件中的`editor.referenceInfos`可以设置打开或关闭此功能。

## 重命名Symbol

TypeScript和C#中对Symbol的重命名，直接在其上按下`F2`并做出修改后再按下`Enter`即可，文件中所有对其的引用都将被更改（包括其他文件中的引用）。

![重命名Symbol][14]

## 快速修改

JavaScript和CSS支持该功能。如果某段语句出现的问题可以被快速修改，光标置于其上时，下方就会出现一个小灯泡的标记。在下图的例子中，由于使用到了Node.js内置对象`__dirname`，快速修改就会是建议下载包含所有Node.js的定义的文件并将引用添加至`node.d.ts`中。

![快速修改][15]

## Errors & Warnings

代码中Warning和Error的产生，一般是通过[已配置任务][link-6]或富态语言自身的检查来完成的，它们会在后台不断地分析你的代码以更新提示信息。Warning和Error将会显示在如下几处：

* 状态栏中会显示出Warning和Error的计数。
* 单击上述计数或者按下`Ctrl+Shift+M`可以查看错误信息清单。
* 如果你打开的文件中含有Warning或Error，命令窗口中输入`!`即会出现其相应信息。

![Errors & Warnings 1][16]

> 提示：使用`F8`或者`Shift+F8`可以在Warning和Error中快速跳转，并会在下方显示出问题的描述信息以及可以快速修复的建议。效果如下图：

![Errors & Warnings 2][17]



[link-1]: https://code.visualstudio.com/docs/editor/editingevolved
[link-2]: http://docs.emmet.io/
[link-3]: http://docs.emmet.io/cheat-sheet/
[link-4]: https://code.visualstudio.com/docs/customization/userdefinedsnippets
[link-5]: https://code.visualstudio.com/docs/languages/overview
[link-6]: https://code.visualstudio.com/docs/editor/tasks
[1]: https://code.visualstudio.com/Content/images/editingevolved_brackets.png
[2]: https://code.visualstudio.com/Content/images/editingevolved_multicursor.png
[3]: https://code.visualstudio.com/Content/images/editingevolved_expandselection.gif
[4]: https://code.visualstudio.com/Content/images/editingevolved_intellisense.gif
[5]: https://code.visualstudio.com/Content/images/editingevolved_parameterhints.png
[6]: https://code.visualstudio.com/Content/images/editingevolved_emmetsnippet.gif
[7]: https://code.visualstudio.com/Content/images/editingevolved_ctrlhover.png
[8]: https://code.visualstudio.com/Content/images/editingevolved_gotosymbol.png
[9]: https://code.visualstudio.com/Content/images/editingevolved_symbol.png
[10]: https://code.visualstudio.com/Content/images/editingevolved_gutter.png
[11]: https://code.visualstudio.com/Content/images/editingevolved_references.png
[12]: https://code.visualstudio.com/Content/images/editingevolved_hover.png
[13]: https://code.visualstudio.com/Content/images/editingevolved_referenceinfo.png
[14]: https://code.visualstudio.com/Content/images/editingevolved_rename.png
[15]: https://code.visualstudio.com/Content/images/editingevolved_quickfix.png
[16]: https://code.visualstudio.com/Content/images/editingevolved_errors.png
[17]: https://code.visualstudio.com/Content/images/editingevolved_errorsinline.png
