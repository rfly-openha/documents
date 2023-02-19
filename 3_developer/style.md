# 代码规范

为确保本仓库中代码风格的统一与一致，且具备一定的可读性，在此，我们对仓库中的代码提出一些基本的约束与规范。
本文主要从代码风格、命名、注释等几个层面给出一定的参考意见，各位仓库贡献者应事先阅读本文，并尽量遵守各项基本要求。

[toc]

## 代码风格

本仓库所托管代码是使用Python实现的开源健康评估框架（Open Source Health Assessment, OpenHA），基本遵循[PEP8](https://www.python.org/dev/peps/pep-0008/)风格规范，用户可点击链接查看其具体基本格式要求。

在这里，我们推荐自动格式化工具`black`，该工具可以自动将代码严格遵循PEP8规范进行格式化。
用户可在其[官网](https://black.readthedocs.io/en/stable/index.html)了解和查看更多内容。

通过命令`pip install black`即可安装`black`。Visual Studio Code或JetBrains PyCharm等集成开发环境一般支持使用`black`等格式化该工具快捷格式化代码的基本功能，如VS Code中，将以下内容添加至其设置文件`settings.json`中，则在Python脚本的编辑界面，通过点击右键菜单中的`Format Document`或快捷键组合`Shift+Alt+F`即可一键格式化代码。

```json
"python.formatting.provider": "black",
"python.formatting.blackArgs": [
    "-S"
]
```

需要注意的是，在本仓库中，严格使用**单引号**表示字符串，即`'str'`或`'''str'''`！！！
由于`black`默认使用双引号，因此应使用参数`-S`或者`--skip-string-normalization`避免其自动将单引号格式化为双引号。

## 命名惯例

常见的变量或函数命名风格有：

- `b` 单个小写字母
- `B` 单个大写字母
- `lowercase` 小写单词
- `lower_case_with_underscores` 下划线分隔小写单词
- `UPPERCASE` 大写单词
- `UPPER_CASE_WITH_UNDERSCORES` 下划线分隔大写单词
- `CapitalizedWords` (or `CapWords`, or `CamelCase`) 大驼峰命名法，首字母大写
- `mixedCase` 小驼峰命名法，首字母小写

总的来说，本仓库中代码主要使用**下划线命名**的整体规范。
- 对于变量与函数名，一般采用**小写单词与下划线**组合，如`load_data()`、`simulation_results`；
- 对于类名，一般采用**大驼峰命名法**，如如`AbstractClass`，其中单词数量建议不超过两个；
- 常量采用**全大写字母加下划线**的命名方式，如`MAX_SIZE`；

总的来说，命名应尽量简短且通俗易懂。在实际编程过程中为兼容其他第三方开源库或出于其他考虑，接受使用驼峰命名、缩写命名等其他较为常用的命名风格。

## 注释与DocStrings

注释是提高代码可读性的关键要素，有助于降低其他用户阅读代码的难度，提高代码编辑、修改和debug效率。
因此在编程过程中应当适时完善注释内容，灵活使用如下所示的各种块注释和行间注释。
需要注意，注释是对算法和程序逻辑关系和注意事项的重点标注，一般情况下，不是对语法的说明。

```python
# We use a weighted dictionary search to find out where i is in
# the array. We extrapolate position based on the largest num
# in the array and the array size and then do binary search to
# get the exact number.

if i & (i-1) == 0:  # True if i is 0 or a power of 2.

```

`DocStrings`是Python中包（Package）、函数（Function）、模块（Module）、类（Class）的第一条语句，可通过`__doc__`属性查看。
本仓库采用的注释与`DocStrings`规范参考[Google Style](https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings)，用户可点击链接查看具体内容。

一个简单的函数注释如下所示：

```python
def plus(a: int, b: int = 0) -> int:
    '''
    函数功能的简要介绍

    这里对该函数`plus()`功能、目的等信息进行详细介绍
    函数声明中建议包含对输入参数及返回值类型的声明

    Args:
        a: int, 参数`a`的介绍
        b: int, optional, 参数`b`的介绍

    Returns:
        返回值介绍

    Raises:
        有可能抛出的异常
    '''

    # 函数体
    return a + b

```

## 版权说明

代码的版权说明应标注在每个文件的最上方，如下示例所示，其中包含了该文件的编码格式说明以及版权说明。

```python
# -*- coding: utf-8 -*-
# Copyright (C) rflylab from School of Automation Science and Electrical Engineering, Beihang University. 
# All Rights Reserved.

# 后接正文

```
