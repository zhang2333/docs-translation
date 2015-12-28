# Visual Studio Code之版本控制

全文翻译自[官方Docs][link-1]

Visual Studio Code集成了[Git][link-2]的大部分常用命令。对于管理Commit来说，这绝对是最好的选择（译者注：集成Git的Commit十分直观），不过也别因此而忘了一直在背后默默支持你的命令提示行; )。

> 注意：VS Code将会利用你机器中安装的Git，所以请在使用前先安装好Git。

## 概览

![概览][p1]

VS Code左侧的Git图标将总是**显示出当前仓库中做出修改的数量**。单击Git图标将进入到Git管理界面，这里会显示出当前仓库所有的变化：**未暂存（Unstaged）**、**已暂存（Staged）**以及**未处理的Merge**。

单击其中每一项都会展示出该文件中详细的文本改变。对于未暂存（Unstaged）的改变，右侧的编辑器同样是可以直接使用的，放心去用吧！

位于VS Code的左下角的Git指示器可以**显示当前仓库状态**：**当前分支**、**错误指示器**以及当前分支上**Commit数量**的变化，单击该指示器则可选择**checkout**到其他的分支。

## Commit

通过右键菜单或者拖拽的方式可以选择是否要把文件**暂存(Staging)**。（译者注：这里指的是Git界面左侧的item list）

在文件改动列表上方输入**Commit Message**，然后`Ctrl+Enter`就可以提交了。如果其中有被暂存的改动，那么只有这一部分会被提交，如果没有被暂存的部分，所有的改动都将被提交。

我们发现这将会是一个很好的工作流程。举个例子：在前面的截图中，只有`config.js`会被包含在本次Commit中，再次Commit`vinyl-zip.js`和`tests.js`才会被提交。

更多**Commit功能**可以在Git界面顶部的`...`菜单中找到。

## 分支与标签

在VS Code中可以通过**命令行面板**直接Create或Checkout分支。按下`Ctrl+P`，输入`git`并按下`Space`，你将看到：

![git][p2]

接着输入`checkout`并按下`Space`，你将看到当前仓库中的所有分支以及标签。

![git checkout][p3]

使用`git branch`命令可以快速创建一条新的分支。只需提供新分支的名字，VS Code即为你创建这条分支并切换至其上。

## 远程仓库

如果你的仓库关联了一个远程仓库，并且当前分支也有一个对应的远程仓库分支(upstream)。VS Code将支持`push`、`pull`和`sync`（`push`命令后执行`pull`）的操作，你可以在顶部的`...`菜单中找到这些。

## 合并冲突

![合并冲突][p4]

我们尝试提供最直观的颜色标记帮助你解决冲突。每解决一个冲突，相关文件就会被暂存，所以解决完后就可以直接Commit了。

## 查看Diff

VS Code内置的Git工具支持查看文件的Diff。

![查看Diff][p5]

> 提示：你可以很容易地对比任意两个不同的文件，目录树上在第一个文件右键选择`Set file to compare`，接着在第二个文件上右键选择`Compare with '第一个文件'`即可。或者你也可以`Ctrl+P`然后选择`File: Compare Active File With... `接着从候选文件列表中选择即可。

## Git输出窗口

在使用VS Code内置Git的过程中遇到问题时，就可以通过这个来查看输出的报错信息。

打开方法：`View`-->` Toggle Output`，然后在窗口右上角的下拉列表中选择`Git`。

## 常见问题

**Q: 我已经初始化了仓库，但是`...`菜单却是灰色的，这是怎么回事？**

**A:**需要使用**push**、**pull**或**sync**功能的话，你需要先设置一个**origin**远程仓库的地址。命令行中如下操作：
```shell
git remote add origin http://your-remote-repo-url
git push -u origin master
```
**Q:我的团队使用的是TFVC而不是Git，该怎么办？**

**A:**请使用TFVC命令行工具。
* 跨平台: [Cross-Platform Command-Line Client Beginner's Guide][link-3]
* Windows: [Use Team Foundation version control commands][link-4]

**Q:使用VS Code的过程中，我不小心对一个含有大量文件的文件夹进行了初始化Git仓库的操作。现在VS Code变得无比缓慢难以使用，我该怎么办？**

**A:**首先，如果你需要重新打开VS Code，先退出VS Code，然后命令行输入：
```shell
code -n
```
（这条命令将打开一个新的VS Code窗口）

然后，删除误操作的文件夹中的`.git`目录即可（需要注意的是，这个文件夹是隐藏的），Windows下`Shift+Del`可以很效率地解决。


[link-1]: https://code.visualstudio.com/docs/editor/versioncontrol
[link-2]: http://git-scm.com/
[link-3]: https://msdn.microsoft.com/en-us/library/hh873092.aspx
[link-4]: https://msdn.microsoft.com/en-us/library/vstudio/cc31bk2e.aspx
[p1]: https://code.visualstudio.com/Content/images/versioncontrol_overview.png
[p2]: https://code.visualstudio.com/Content/images/versioncontrol_gitcommands.png
[p3]: https://code.visualstudio.com/Content/images/versioncontrol_gitbranches.png
[p4]: https://code.visualstudio.com/Content/images/versioncontrol_merge.png
[p5]: https://code.visualstudio.com/Content/images/versioncontrol_diff.png
