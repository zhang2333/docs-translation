# Visual Studio Code之调试

全文翻译自[官方Docs][link-1]

VS Code一个重要特性是它有很好的调试支持，内置的调试器可以加速你的"编写-编译-调试"工作流。

![概览][p1]

如今我们对全平台**Node.js**(JavaScript和TypeScript)的调试有很好的支持，而对OS X和Linux下的**Mono**(C#和F#)调试尚是实验式支持。如需调试其他语言，请前往[VS Code市场][link-2]寻找相应的`Debuggers(调试器)`插件。

## 调试视图

单击VS Code左侧视图栏的调试图标即可打开调试视图。

![调试视图][p2]

调试视图顶部栏是调试相关的命令与配置，其下方是所有调试信息的展示。

## 启动配置

想要在VS Code中调试程序，需要先调整好调试的**启动配置**——`launch.json`。单击调试视图顶部栏中的齿轮图标，并选择好调试环境，VS Code即为你生成一份`launch.json`。

调试Node.js示例：

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Launch",
            "type": "node",
            "request": "launch",
            "program": "app.js",
            "stopOnEntry": false,
            "args": [],
            "cwd": ".",
            "runtimeExecutable": null,
            "runtimeArgs": [
                "--nolazy"
            ],
            "env": {
                "NODE_ENV": "development"
            },
            "externalConsole": false,
            "preLaunchTask": "",
            "sourceMaps": false,
            "outDir": null
        },
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858
        }
    ]
}
```

VS Code支持以调试模式启动应用，或调试一个已运行的应用。这取决于当前配置中`request `的取值(`attach`还是`launch`)，这个属性是必需的，如果你忘记了如何赋值也没关系，填写时VS Code会提示你的。

上例`configurations`中编写了`name`为`Launch`和`Attach`的两种配置，视图顶部栏的下拉菜单可以指定需要以哪个配置运行，如果选择的是`Launch`，那么接着按下`F5`就可以启动调试了。

如需在启动调试前执行某个特定任务(task)，为`preLaunchTask`设置`tasks.json`中的任务名即可。

## 断点

单击**编辑器**侧边缘即可为所在行添加断点，调试时**BREAKPOINTS**区域中也可对断点进行操作(enable/disable/reapply)。

![断点][p3]

`Reapply All Breakpoints`命令可以让断点重置至其初始位置，这对于调试环境是**lazy**模式以及还没被执行的误置断点来说十分有帮助。

## 数据审查

调试视图的**VARIABLES**区域可以审查变量，也可以直接在源码上悬停鼠标来查看。变量和表达式的演算则显示在**CALL STACK**区域中。

![变量审查][p4]

在调试视图的**WATCH**区域也可以看到变量和表达式的演算。

![WATCH][p5]

## 调试控制台

在调试控制台可以计算表达式。打开调试控制台需要`Open Console`，该命令可以在调试视图顶部栏和命令面板中被找到。

![调试控制台][p6]

## 调试命令

调试一旦启动，**编辑器**顶部就会显示出调试命令栏。

![调试命令][p7]

* 继续 / 暂停 `F5`
* 跳过 `F10`
* 进入 `F11`
* 退出 `Shift+F11`
* 重新开始 `unassigned`
* 停止调试 `Shift+F5`


## 调试Node

### Node控制台

调试Node时，默认启用的是VS Code内置的控制台。内置的调试控制台不支持输入，如果你需要从控制台输入，那么你应该使用外部控制台，在**启动配置**中设置`externalConsole`为`true`即可。

### 断点验证

出于性能的考虑，Node.js解析js文件中的函数时采用了“懒加载”模式。其结果是，未被Node.js解析的源码中的断点不会起作用。

这一点对于调试工作来说自然是不理想的，所以在调试时VS Code自动添加了`--nolazy`选项。这样就可以阻止延迟解析，并确保断点可以在代码运行前被正常地触发了。

`--nolazy`选项会导致启动时间大大增加，如果你不希望如此，添加`--lazy`来作为**runtimeArgs**的属性即可。

实际调试工作中，你可能会发现一些你设置的断点没有在预期位置被触发，而是跳到了下一个可执行行。为了避免混淆，VS Code将实时显示断点的位置（Node.js判断的）。在**BREAKPOINTS**区域，断点将显示出其被触发的位置以及其实际所在行：

![断点][p8]

启动一个已添加好断点的调试，或者在一个已运行的调试中添加了一个新的断点，断点都有可能会跳至其他位置。在Node.js解析完所有代码之后，使用**BREAKPOINTS**区域顶部的**Reapply**按钮可重置断点，可以让断点重新跳回到触发位置。

![重置][p9]

### JavaScript源码关联

VS Code的Node.js调试器支持JavaScript源码映射关联，这将有助于调试一些转译语言，比如TypeScript和已被压缩过的JavaScript。设置**启动配置**中的**sourceMaps**属性为`true`可以开启源码关联，关联的源码将允许单步调试以及在其中添加断点。另外，你可以使用**program**属性来指定源码文件（如：`app.ts`）。如果被生成的js文件并不是和源码在同一目录，而是分散放在了其他的路径中，你可以使用**outDir**属性来帮助调试器找到这些文件。无论何时你在转译语言源码中设置了断点，VS Code都会尝试在**outDir**目录下生成的JavaScript源码中找到相应位置去映射关联。

源码映射关联并不是自动创建的，你必须通过配置TypeScript编译器来完成：

```shell
tsc --sourceMap --outDir bin app.ts
```

TypeScript调试配置示例：

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Launch TypeScript",
            "type": "node",
            "request": "attach",
            "program": "app.ts",
            "sourceMaps": true,
            "outDir": "bin"
        }
    ]
}
```

### 调试外部Node

如果你想要使用VS Code的调试器来调试外部Node.js程序，命令行示例：
```shell
node --debug program.js
node --debug-brk program.js
```

**--debug-brk**选项用于让程序停止在程序源码的第一行。

相应的**启动配置**示例：
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach to Node",
            "type": "node",
            "request": "attach",
            "port": 5858
        }
    ]
}
```

## 常见问题

**Q: 都支持哪些调试场景？**

**A:** Linux、OS X以及Windows下支持调试Node.js程序。Linux、OS X下支持调试运行在Mono上的C#程序。ASP.NET 5应用程序的编译使用的是Roslyn而不是Mono，其调试可以通过VS Code扩展程序进行。

**Q:为什么我不能远程调试我的app？**

**A:** 目前我们只支持本地调试。这是一个已知的限制条件，如果你还有什么困惑，请[告诉我们][link-3]！

**Q: 调试视图的下拉菜单里我并没有看到可选的启动配置啊？**

**A:** 很有可能是因为`launch.json`文件还没有被生成，抑或是该文件中存在语法错误。


[link-1]: https://code.visualstudio.com/docs/editor/debugging
[link-2]: https://marketplace.visualstudio.com/vscode/Debuggers
[link-3]: http://visualstudio.uservoice.com/forums/293070-visual-studio-code/suggestions/7872216-remote-debugging
[p1]: https://code.visualstudio.com/Content/images/debugging_hero.png
[p2]: https://code.visualstudio.com/Content/images/debugging_debugicon.png
[p3]: https://code.visualstudio.com/Content/images/debugging_breakpoints.png
[p4]: https://code.visualstudio.com/Content/images/debugging_variables.png
[p5]: https://code.visualstudio.com/Content/images/debugging_watch.png
[p6]: https://code.visualstudio.com/Content/images/debugging_debugconsole.png
[p7]: https://code.visualstudio.com/Content/images/debugging_actions.png
[p8]: https://code.visualstudio.com/Content/images/debugging_breakpointsvalidation.png
[p9]: https://code.visualstudio.com/Content/images/debugging_breakpointstoolbar.png
