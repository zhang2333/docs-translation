#Visual Studio Code的基本使用
全文翻译自[官方Docs][1]

Visual Studio Code的核心是一个代码编辑器。像许多其他代码编辑器一样，VS Code采用了普遍的UI设计，将显示所有可访问的文件及文件夹的目录树置于左侧，并将文件内容编辑器置于右侧。下面本篇将描述VS Code的几个独特之处。
> 译者注：NodeJS方面VS Code是Sublime很好的替代品，不妨试试

##文件与Project
VS Code以文件、文件夹为基础——你可以通过VS Code打开文件夹来立即启动project。

VS Code可以读写不同框架或平台中不同类型的文件。即便你的VS Code同时打开了`package.json`、 `project.json`、`tsconfig.json`甚至ASP.NET 5 Visual Studio的项目文件，VS Code仍然可以读取它们并为你提供相应的附加功能，如[IntelliSense][2]。

##基本布局
VS Code拥有简洁与直观的界面布局，并为编辑区提供了最大化的区域，以提供足够的空间来浏览。
UI部分划分为以下四个区域：

* **编辑器**：最主要的区域，用来编辑你的文件。你可以以分栏的方式同时打开三个文件。
* **侧边栏**：包含不同的视图，能像文件浏览器一样在工作时协助你。
* **状态栏**：显示已打开的project及正在编辑的文件的信息。
* **视图栏** ：位于最左侧，可以让你在不同的视图间进行切换，以及给予你额外特定的全局指示器，如应用Git时，project的变化会在其上显示相应的数字。

每当你打开VS Code时，都会显示你上次退出时界面的状态。文件夹、布局以及已打开的文件都将是上次被保存的状态。

![VS Code界面布局][p1]

VS Code可允许至多三个可见的**编辑器**并排存在，而不是使用标签页的方式来安放已打开的文件。

这将有助于减少来往于不同标签页的劳动量，但同时也并不限制你打开文件的数量。**文件浏览器**可以为project维持一个实时的树状目录，你可以快速访问你需要打开的文件。

> 提示：你可以移动侧边栏至右手边(View, Move Sidebar)以及控制其是否显示(`Ctrl+B`)。

##分栏编辑
你可以并排打开至多三个**编辑器**。

如果你已经打开了一个**编辑器**，你可以有多种方式再打开一个编辑器与之并排：

* `Ctrl`(Mac: `Cmd`)+单击目录树中的一个文件
* `Ctrl+\`令当前窗口一分为二
* 在左侧目录树中的文件上右键选择`Open to the Side`

当你打开另一个文件时，当前获得焦点的**编辑器**将显示该文件的内容。所以如果你当前有两个并排的**编辑器**并想要打开文件`foo.css`到右侧的**编辑器**时，那么你需要确定右侧的这个**编辑器**是处于激活（获得焦点）状态（可以通过在**编辑器**内部单击的方式激活）的。

当你打开了多个**编辑器**并希望能快捷地从中切换时，只需要按住`Ctrl`(Mac:`Cmd`)键并按下`1`、`2`或者`3`即可。

> 提示：你可以通过左右拖拽**编辑器**标题栏来调整**编辑器**的位置，通过拖拽**编辑器**之间的分割线来调整它们的宽度。

![分栏编辑][p2]

##Explorer 文件浏览器
**文件浏览器**用于浏览、打开或管理project中的文件及文件夹。

当使用VS Code打开一个文件夹之后，此文件夹中的所有内容都将呈现在**文件浏览器**之中。你可以对其进行如下操作：

* 创建、删除、重命名文件或文件夹
* 通过拖拽的方式来移动文件或文件夹
* 使用右键菜单浏览更多操作

> 提示：你可以通过拖拽一个外部文件到**文件浏览器**中的方式来复制此文件到project。

![右键菜单][p3]

在VS Code中也可以很方便地使用其他的工具，比如命令行工具。如果你想打开以当前工作目录下的命令行，你可以在**文件浏览器**中选中该文件夹（或其下的某个文件）右击并选择右键菜单中的`Open in Console`。

你可以右击某个文件或文件夹并选择`Reveal in Explorer`(Mac:`Reveal in Finder`)来打开该文件或文件夹的本地目录。

> 提示：`Ctrl+P`可以快捷地根据文件名来搜索并打开这个文件。

默认地，VS Code在**文件浏览器**中排除了一些文件夹（比如`.git`）。使用设置中的`files.exclude`来配置在**文件浏览器**中需要隐藏的文件夹的规则。

> 提示：这一点对于隐藏一些资源文件来说非常有用，比如Unity中的`\*.meta`以及TypeScript项目中的`\*.js`。Unitry中需要排除`\*.cs.meata`文件时，匹配规则应该是`"**/*.cs.meta": true`。

##Working Files

**文件浏览器**的顶部是**Working Files**区域，这其中包含了你之前使用VS Code打开过的文件的列表。以下的操作会将文件列入**Working Files**：

* 对一个文件进行了改动
* 在文件浏览器中双击文件
* 打开了一个外部文件

![Working Files][p4]

**Working Files**其实和你熟悉的代码编辑器或IDE中的标签页十分相似，不过是将标签页标题纵向排列。

当你完成了某项工作，你可以很方便地从**Working Files**中单独移除某个文件，也可以通过`Close All Files`的操作来移除所有文件。

> 提示：你可以在设置中配置**Working Files**的显示属性。通过`explorer.workingFiles.maxVisible`设置**Working Files**出现滚动条前的最大显示高度，或者使用`explorer.workingFiles.dynamicHeight`让其为自动高度。

##保存 / 自动保存

默认地，VS Code需要你手动`Ctrl+S`来保存文件改动到硬盘中。

十分便捷的`Auto Save`功能可以在空闲时为你保存文件的改动，而当这项功能开启时，就无需手动保存文件了。

打开或者关闭`Auto Save`：打开**命令面板**(`Ctrl+Shift+P`)，接着输入`auto`过滤显示列表，找到`Auto Save`回车即可。

当然你也可以在菜单`File`中找到这项功能。

##搜索

VS Code可以在当前已打开的文件夹下所有的文件中快速搜索内容，只需要按下`Ctrl+Shift+F`并输入关键词即可。搜索结果将以分组的方式显示包含该关键词的文件，并标记出关键词出现次数和所在位置，单击一个结果即可打开其所在的文件。

![搜索演示][p5]

> 提示：搜索内容支持正则表达式。你可以使用`Ctrl+Shift+J`来打开高级搜索，为你的搜索提供额外的过滤条件。

![高级搜索][p6]

高级搜索中搜索栏下的两个输入框，分别是填写的需要包含和排除的某些文件。单击输入框右侧的按钮(`Use Glob Patterns`)以确保当前支持`Glob Pattern`语法：

*  `*`匹配一个或多个任意字符（译者注：`a*.js` -> `app.js`）
*  `?`匹配一个任意字符（译者注：`ap?.js` -> `app.js`）
*  `**`匹配任意数量的任意字符，即所有
*  `{}`分组条件（例：`{**/*.html,**/*.txt}`将匹配所有`html`以及`txt`文件）
*  `[]`定义字符的范围（例：` example.[0-9]`将匹配`example.0`或`example.1`）

VS Code默认排除了一些你不感兴趣的目录（比如`node_modules`）以优化搜索的结果，当然你也可以对此使用`files.exclude`和`search.exclude section`进行设置。

> 提示：在**文件浏览器**中的文件夹上右键`Find in Folder`将只会在该目录下进行搜索。

##命令面板

VS Code允许使用键盘来调用某些功能。使用快捷键`Ctrl+Shift+P`可以打开**命令面板**，你可以通过它来调用所有VS Code的功能，这其中还包括能使用快捷键控制的常见操作。

![命令面板][p7]

**命令面板**的UI也提供给其他的一些操作命令。在**编辑器**中的一些操作，打开指定文件、搜索symbol或者查看文件大纲等操作都将使用与**命令面板**相同的交互窗口。下面是这些操作的一点提示：

* `Ctrl+P`：输入相应名称即可快速地打开文件或symbol
* `Ctrl+Tab`：快速地从打开过的文件中切换
* `Ctrl+Shift+O`将指向你所指定的symbol所在文件中的位置
* `Ctrl+G`跳至指定行数

在输入框内键入`?`将显示可执行命令的列表：

![Quick Open Help][p8]

##文件切换

当你浏览一个project时，**文件浏览器**能很好地在众多文件中切换。然而，你也会遇到只在几个固定的文件中切换的情况，这个时候**文件浏览器**就显得不那么方便了。于此，VS Code提供了两组非常好用的快捷键以应对这种情况。

按下`Ctrl+Tab`时，将显示从你启动VS Code后你打开过的文件的列表。（译者注：但从**Working Files**关闭的话就不会出现在该列表了）想要打开其中的文件的话，按住`Ctrl`(Mac:`Cmd`)并按下`Tab`选择需要切换的文件即可。

![快速切换][p9]

当然，你也可以使用`Alt+Left`或`Alt+Right`来切换文件。如果你需要在同一文件不同行之间快速跳转，你也可以使用这一对快捷键。

> 提示：想要快速地切换至任一文件的话，只需要`Ctrl+P`并输入文件名即可。

##文件编码

使用`file.encoding`来指定VS Code的文件编码类型，在**User Setting**中设置将作用于全局，而在**Workspace Settings**中设置将只作用于当前工作空间。

![files.encoding][p10]

当前文件的编码类型可以在底部状态栏中看到。

![状态栏中的编码类型][p11]

在状态栏中点击编码类型可以选择以不同的编码类型来重新打开或保存该文件。

![以不同的编码来重新打开或保存][p12]

然后选择一种编码类型。

![Select an encoding][p13]

##从命令行启动

你可以从命令行启动VS Code来快速打开一个文件、文件或者project。命令行切换到目标目录，然后输入：
```batch
code .
```
> 提示：我们在Mac和Linux的[安装版本页面][3]中做出了提示，告诉你该如何启动VS Code。我们也为Windows用户自动添加了VS Code的环境变量。

当你想要打开一个文件时，如果该文件不存在，我们将为你自动创建：
```batch
code index.html style.css readme.md
```
> 提示：你可以用空格分隔文件名来同时打开多个文件。

##命令行参数

下面是一些`code`命令可选的参数。

<table>
	<thead>
		<th width="35%">参数</th>
		<th>描述</th>
	</thead>
	<tbody>
		<tr>
			<td><code>-g</code>或<code>--goto</code></td>
			<td>配以<em>file:line:column</em>时可以定位到文件中指定的位置，列数为可选。如果文件名中包含<code>:</code>，那么该参数为必须。</td>
		</tr>
		<tr>
			<td><code>-n</code>或<code>--new-window</code></td>
			<td>打开一个新的VS Code窗口</td>
		</tr>
		<tr>
			<td><code>-r</code>或<code>--reuse-window</code></td>
			<td>使用当前VS Code窗口打开文件或文件夹</td>
		</tr>
		<tr>
			<td><em>file</em></td>
			<td>指定需要打开文件的名称。如果文件不存在，将自动被创建。该命令也可以指定多个文件。</td>
		</tr>
		<tr>
			<td><em>folder</em></td>
			<td>指定需要打开文件夹的名称，可以指定多个文件夹。</td>
		</tr>
	</tbody>
</table>

对于文件或是文件夹，你都可以使用绝对或相对路径。相对路径指的是相对于你运行命令`code`的地方。

如果你在命令行指定多个文件或文件夹，VS Code将只开启一个实例。

##打开Project

VS Code并不区分你打开的是文件夹还是project。无论你打开的文件夹里包含了什么文件，VS Code都会读取它们并在状态栏标记project状态。而如果文件夹中包含了多个project，你也可以从状态栏方便地切换project。（译者注：对于VS Code来说，project其实相当于文件夹的一个子集，可以把project看作是一种特殊的文件夹）

要打开project所在的文件夹`c:\src\WebApp`：
```batch
code c:\src\webapp
```
换言之，要打开一个包含project的文件夹其实就是要打开这个project：

![Status Bar][14]

##窗口管理

VS Code有一些选项可以控制窗口是需要被新建还是复用。

`window.openInNewWindow`可以让VS Code在打开文件时新建窗口，而不是继续使用已有的窗口。默认地，VS Code会新建窗口（当你双击一个外部文件或者从命令行打开一个文件时）。设置这个属性为`false`的话，打开文件将使用当前已有的窗口。

设置`window.reopenFolders`将告诉VS Code该如何启动。默认地，VS Code将打开上次的project（值：`one`）。设置为`never`后，VS Code启动时则会打开一个空的project。设置为`all`后，VS Code将开启你上次工作过的所有project窗口。

##下一步

OK，到此为止，相信你已经掌握了VS Code的基本使用。而接下来，你将了解到：

* 进阶编辑：Lint、IntelliSense、Lightbulbs、Peek和Goto Definition以及更多。
* 调试：VS Code的闪光点
* 自定制：主题、设置以及快捷键

##常见问题

问：可以全局检索并替换吗？

答：这个功能目前还没有实现，不过你可以期待它的出现。（译者注：全文检索VS Code是支持的，但是不能在同时替换）



[1]: https://code.visualstudio.com/docs/editor/codebasics
[2]: http://baike.baidu.com/link?url=RsUxLFDoubkIRFpsmjfZo4j1StrGDm2ZgBUAu2SbdnG9f81AXFWPBcY_zXdAZCNABI7fHASx-TcDHzm1L2JBrq
[3]: https://code.visualstudio.com/docs/editor/setup
[p1]: http://code.visualstudio.com/Content/images/codebasics_layout.png
[p2]: http://code.visualstudio.com/Content/images/codebasics_sidebyside.png
[p3]: http://code.visualstudio.com/Content/images/codebasics_explorer_menu.png
[p4]: http://code.visualstudio.com/Content/images/codebasics_workingfiles.png
[p5]: http://code.visualstudio.com/Content/images/codebasics_search.png
[p6]: http://code.visualstudio.com/Content/images/codebasics_searchadvanced.png
[p7]: http://code.visualstudio.com/Content/images/codebasics_commands.png
[p8]: http://code.visualstudio.com/Content/images/codebasics_quickopenhelp.png
[p9]: http://code.visualstudio.com/Content/images/codebasics_quicknav.png
[p10]: http://code.visualstudio.com/Content/images/codebasics_filesencodingsetting.png
[p11]: http://code.visualstudio.com/Content/images/codebasics_fileencoding.png
[p12]: http://code.visualstudio.com/Content/images/codebasics_encodingclicked.png
[p13]: http://code.visualstudio.com/Content/images/codebasics_encodingselection.png
[p14]: http://code.visualstudio.com/Content/images/codebasics_status.png
