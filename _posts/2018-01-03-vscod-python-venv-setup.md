---
layout: post
title: vscode之python环境设置
category : tech
description: ""
guid: 0ee5a216-65a4-4159-bd96-e1fa12fdb561
tags : [Python, vscode]
---
{% include JB/setup %}

使用`vscode`设置`python`开发环境，主要有以下方面:
1. 语法高亮显示，代码自动补及支持debug等
2. 设置`python`路径及`virtualenv`
3. 易于执行代码

这三个方面涉及到两个插件以及一个vscode配置, 具体配置如下:
1. 安装插件`Python`，针对第一个问题
2. 设置`vscode`内置的`python`路径--即`virtualenv`，以便于vscode安装一些其他的module以及调试:

> Shift + Command + P
> // type
> Python: Select Interpreter
> // choose your virtual env

上述步骤也可以通过手工设置方式完成, `Command + ,`编辑`User Setttings`, 添加如下代码:
> "python.pythonPath": "${workspaceFolder}/venv/bin/python3"

3. 安装`Code Runner`插件，解决第三个问题. 但是需要注意的`Code Runner`使用其自身的`python`路径, 因此需要更改为第2步中设置的`virtualenv`. **由于Code Runner内部所用变量不一定与vscode相同，因此要依据其doc上的说明!**

> // 编辑`User Setting`, 添加如何代码
> "code-runner.executorMap": {
>    "python": "$workspaceRoot/venv/bin/python $fullFileName"
>  }


## Reference
1. [用VSCode写python的正确姿势](http://www.cnblogs.com/bloglkl/archive/2016/08/23/5797805.html)
2. [Visual Studio code and virtualenv](https://stackoverflow.com/questions/38545326/visual-studio-code-and-virtualenv)
3. [Code Runner for Visual Studio Code](https://github.com/formulahendry/vscode-code-runner)

*注: 所有操作在macOS进行, 其他系统会有所差别*

*The End.*






