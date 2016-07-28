# Visual Studio Code之调试

全文翻译自[官方Docs][link-1]，更新至`1.3`版本。

VS Code一个重要特性是它有很好的调试支持，内置的调试器可以加速你的"编写-编译-调试"工作流。

![概览][p1]

## 调试器扩展

VS Code内置调试器支持调试Node.js运行时，同时也可以调试JavaScript、TypeScript以及其他JS转译语言。

如需调试其他语言与运行时(包括PHP, Ruby, Go, C#, Python等)，请前往[VS Code市场][link-2]寻找相应的`Debuggers(调试器)`扩展程序。

## 开始调试

下文将基于内置的Node.js调试来进行相关的说明，大部分的说明同样适用于其他调试器。

一则建议：开始阅读本文之前你可以尝试去创建一个简单的Node.js应用程序，然后一遍阅读本文一遍动手实验(这里有一篇文章可以教你如何安装Node.js并创建一个的"Hello World"程序[Node.js Applications with VS Code][link-3])。

## 调试视图

单击VS Code左侧视图栏的调试图标即可打开调试视图。

![调试视图][p2]

调试视图顶部栏是调试相关的命令与配置，其下方是所有调试信息的展示。

## 启动配置

想要在VS Code中调试程序，需要先调整好调试的**启动配置**——`launch.json`。单击调试视图顶部栏中的齿轮图标，并选择好调试环境，VS Code会在`.vscode`目录下为你生成一份`launch.json`。

调试Node.js示例：

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Launch",
            "type": "node",
            "request": "launch",
            "program": "${workspaceRoot}/app.js",
            "stopOnEntry": false,
            "args": [],
            "cwd": "${workspaceRoot}",
            "preLaunchTask": null,
            "runtimeExecutable": null,
            "runtimeArgs": [
                "--nolazy"
            ],
            "env": {
                "NODE_ENV": "development"
            },
            "externalConsole": false,
            "sourceMaps": false,
            "outDir": null
        },
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "localhost",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }
    ]
}
```

VS Code支持以调试模式启动应用，或调试一个已运行的应用。这取决于当前配置中`request `的取值(`attach`还是`launch`)，这个属性是必需的，如果你忘记了如何赋值也没关系，填写时VS Code会提示你的。

上例`configurations`中编写了`name`为`Launch`和`Attach`的两种配置，视图顶部栏的下拉菜单可以指定需要以哪个配置运行，如果选择的是`Launch`，那么接着按下`F5`就可以启动调试了。

如需在启动调试前执行某个特定任务(task)，为`preLaunchTask`设置`tasks.json`中的任务名即可。

## 断点

单击**编辑器**侧边缘即可为所在行添加断点，调试时**BREAKPOINTS**区域中也可对断点进行操作(enable/disable/reapply)。

* 断点正常显示为红色的圆
* 被取消的断点是灰色的圆
* 调试启动后，不能被注册的断点显示为灰色的圆圈

![断点][p3]

`Reapply All Breakpoints`命令可以让断点重置至其初始位置，这对于调试环境是**lazy**模式以及还没被执行的误置断点来说十分有帮助。

## 数据审查

调试视图的**VARIABLES**区域可以审查变量，也可以直接在源码上悬停鼠标来查看。变量和表达式的演算则显示在**CALL STACK**区域中。

![变量审查][p4]

在调试视图的**WATCH**区域也可以看到变量和表达式的演算。

![WATCH][p5]

## 调试控制台

在调试控制台可以计算表达式。打开调试控制台需要`Open Console`，该命令可以在调试视图顶部栏和命令面板中被找到(`Ctrl+Shift+P`)。

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

### 函数断点

除了能在源码内直接标记断点外，Node.js的调试现在还可以通过一个函数的名字来创建断点，这尤其适用于未翻阅源码但知道函数名的情况。

**BREAKPOINTS**区域的`+`可以添加函数断点，具体请看下图：

![创建函数断点][p10]

> 注意：函数断点的函数只能是已被定义的全局且`non-native`函数。

### JavaScript源码关联

VS Code的Node.js调试器支持JavaScript源码映射关联，这将有助于调试一些转译语言，比如TypeScript和已被压缩过的JavaScript。有了源码关联，就可以直接在源码上标记断点了。如果源码映射被破坏或者源码没能成功映射到已生成的JS代码上，断点将显示为灰色的圆圈。

设置**启动配置**中的**sourceMaps**属性为`true`可以开启源码关联，关联的源码将允许单步调试以及在其中添加断点。另外，你可以使用**program**属性来指定源码文件（如：`app.ts`）。如果被生成的js文件并不是和源码在同一目录，而是分散放在了其他的路径中，你可以使用**outDir**属性来帮助调试器找到这些文件。无论何时你在转译语言源码中设置了断点，VS Code都会尝试在**outDir**目录下生成的JavaScript源码中找到相应位置去映射关联。

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

如果想要使用VS Code的调试器来调试外部Node.js程序，在命令行如下操作：
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
            "address": "localhost",
            "port": 5858,
            "restart": false
        }
    ]
}
```

`restart`属性用来控制Node.js调试器是否在调试结束后自动重启。如果你使用**nodemon**在文件改动时重启Node，`restart`属性就会显得很有用了。设置`restart`为`true`可以让**node-debug**自动在Node被终止时重连Node。

使用**nodemon**启动Node程序(`server.js`)

```shell
nodemon --debug server.js
```

> 提示：按下`Stop`按钮可以停止调试任务并断开与Node.js的连接，但**nodemon**(以及Node.js)仍会继续运行，如需停止**nodemon**，你需要在命令行中手动停止它。

> 提示：如果程序有语法错误，**nodemon**将不能正常启动Node，直到所有错误都被改正。如果发生了这种情况，VS Code将继续尝试连接Node，但会在10秒后放弃重试，当然，你可以通过`timeout`属性(毫秒值)来增加这个时间。

### 远程调试

通过`address`属性来指定远程主机(host)就可以用Node调试器远程调试了(Node.js版本 >= 4.x)。

默认地，VS Code会将远程的Node目录连接至本地VS Code，并将代码显示到一个只读的编辑器上。你可以单步调试这些代码，但不能修改它们。如果想去编辑源码，那么你需要映射远程和本地。`attach`启动配置中设置`localRoot`和`remoteRoot`属性可以映射远程和本地(支持不同操作系统之间的映射)。

## 常见问题

**Q: 都支持哪些调试场景？**

**A:** Linux、OS X以及Windows下支持调试Node.js程序。Linux、OS X下支持调试运行在Mono上的C#程序。ASP.NET 5应用程序的编译使用的是Roslyn而不是Mono，其调试可以通过VS Code扩展程序进行。

**Q: 调试视图的下拉菜单里我并没有看到可选的启动配置啊？**

**A:** 很有可能是因为`launch.json`文件还没有被生成，抑或是该文件中存在语法错误。

**Q: Node调试需要什么版本的Node呢？**

**A:** 推荐Node.js的LTS版。

[link-1]: https://code.visualstudio.com/docs/editor/debugging
[link-2]: https://marketplace.visualstudio.com/vscode/Debuggers
[link-3]: https://code.visualstudio.com/docs/runtimes/nodejs
[p1]: https://code.visualstudio.com/images/debugging_debugging_hero.png
[p2]: https://code.visualstudio.com/images/debugging_debugicon.png
[p3]: https://code.visualstudio.com/images/debugging_breakpoints.png
[p4]: https://code.visualstudio.com/images/debugging_variables.png
[p5]: https://code.visualstudio.com/images/debugging_watch.png
[p6]: https://code.visualstudio.com/images/debugging_debugconsole.png
[p7]: https://code.visualstudio.com/images/debugging_actions.png
[p8]: https://code.visualstudio.com/images/debugging_breakpointsvalidation.png
[p9]: https://code.visualstudio.com/images/debugging_breakpointstoolbar.png
[p10]: https://code.visualstudio.com/images/debugging_function-breakpoint.gif
