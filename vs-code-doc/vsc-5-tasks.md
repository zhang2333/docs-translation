# Visual Studio Code之任务

全文翻译自[官方Docs][link-1]

## 通过任务来集成外部工具

许多自动化工具（如Make, Ant, Gulp, Jake, Rake, MSBuild）都有像构建、打包、测试和部署这样的任务。

这些工具大多运行在命令行，在外部自动化任务去执行软件内部的工作流（编辑、编译、测试以及调试）。在开发周期中给予它们足够的重视，将有助于你去运行它们并在VS Code中分析运行结果。

## 例子

下面将举几个例子来告诉你VS Code是如何使用任务来集成像linter和compiler这样的外部工具的。

### 将TypeScript转译为JavaScript

[TypeScript专题][link-2]中包含了关于创建一个将TypeScript转译为JavaScript的任务并在VS Code中观察关联错误的例子。

### 将Markdown编译为HTML

Markdown专题中提供了两个将Markdown编译为HTML的例子。

* [使用构建任务手动编译][link-3]
* [使用文件监视器自动编译][link-4]

### 将Less和Sass转译为CSS

CSS专题中提供了两个告诉你如何使用任务来生成CSS文件的例子。

* [使用构建任务手动编译][link-5]
* [使用文件监视器自动编译][link-6]

## 使用问题匹配器来处理任务的输出

VS Code使用问题匹配器来处理任务的输出，我们将在方框中显示它们的数量。

* TypeScript: 假设`$tsc`是相对于已打开目录输出中的文件名
* JSHint: 假设`$jshint`是绝对路径下输出报告的文件名
* JSHint Stylish: 假设`$jshint-stylish`是绝对路径下的文件名
* ESLint Compact: 假设`$eslint-compact`是相对于已打开目录输出中的文件名
* ESLint Stylish: 假设`$eslint-stylish`是相对于已打开目录输出中的文件名
* CSharp and VB Compiler: 假设`$mscompile`是绝对路径下输出报告的文件名
* Less: 假设`$lessCompile`是绝对路径下输出报告的文件名

[link-1]: https://code.visualstudio.com/docs/editor/tasks
[link-2]: https://code.visualstudio.com/docs/languages/typescript#_transpiling-typescript-into-javascript
[link-3]: https://code.visualstudio.com/docs/languages/markdown#_compiling-markdown-into-html
[link-4]: https://code.visualstudio.com/docs/languages/markdown#_automating-markdown-compilation
[link-5]: https://code.visualstudio.com/docs/languages/css#_transpiling-sass-and-less-into-css
[link-6]: https://code.visualstudio.com/docs/languages/css#_automating-sassless-compilation
