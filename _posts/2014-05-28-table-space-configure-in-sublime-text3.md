title: "在Sublime Text中设置Tab-Space"
date: 2014-05-28 09:21:27
categories:
- 教程
- sublime_text
---

### 1: 概述

缩进设置决定了tab符缩进的大小，控制tab键是插入tab符号还是空格。除了自动检测之外，它们可以自定义为全局，某种文件类型，或者某个文件。

### 2: 设置

	|---------------------------|--------------------------------------------------------------------------------------------------------------|
	|tab_size                   | 数字。插入的空格数                                                                                           |
	|translate_tabs_to_spaces   | Boolean, 如果为true，按tab键将会输入空格替代，而不是tab字符                                                  |
	|detect_indentation         | Boolean, 默认为true, tab_size和translate_tabs_to_spaces将会在文件载入是自动计算                              |
	|use_tab_stops              | Boolean, 如果translate_tabs_to_spaces为true, use_tab_stops将会使tab和backspace在下一个tab停止时insert/delete |

### 3: 配置文件

配置文件将会按下面这个顺序应用：

1.	Packages/Default/Preferences.sublime-settings
2.	Packages/Default/Preferences (<platform>).sublime-settings
3.	Packages/User/Preferences.sublime-settings
4.	Packages/<syntax>/<syntax>.sublime-settings
5.	Packages/User/<syntax>.sublime-settings

通常情况下，你应该把你的配置放在`Packages/User/Preferences.sublime-settings`里。如果你要给特定的文件类型指定配置，比如，Python, 应该放在`Packages/User/Python.sublime-settings`文件中

### 4: 配置文件示例

试着把这些保存为`Packages/User/Preferences.sublime-settings`

```
{
    "tab_size": 4,
    "translate_tabs_to_spaces": false
}
```

### 5: 单独语法配置

可以在基础配置之上指定单独的语法配置。在`Preferences/Settings - More/Syntax Specific - User`菜单下

### 6: 缩进的检测

当一个文件载入时，它的内容会被检查，`tab_size`和`translate_tabs_to_spaces`设置将会应用到该文件。状态栏将会报告发了什么。尽管编辑器会处理的很好，如果想要把它禁用的话，可以通过`detect_indentation`来设置

缩进检测可以手动执行，通过`View/Indentation/Guess Settings From Buffer`菜单执行`detect_indentation`命令

### 7: Tab和空格之间转换

`View/Indentation`菜单里有命令可以将当前文件中的空白在tab符和空格符之间转换。这几个菜单项执行的是`expand_tabs`和`unexpand_tabs`命令

### 8: 自动缩进

自动缩进猜测会在换行时给每一行添加一定数量空白符。由下面这个配置控制：

	|-------------------------------|-----------------------------------------------------------------------------------------------------------|
	| auto_indent                   | Boolean, 默认是开启                                                                                       |
	| smart_indent                  | Boolean, 默认是开启。具有一点小聪明的自动缩进，比如，在一个if语法片段的下一行进行缩进                     |
	| trim_automatic_white_space    | Boolean, 默认开启。当断行时由auto_indent去除行头尾的空白                                                  |
	| indent_to_bracket             | Boolean, 默认禁用。缩进时根据第一个前括号来空白数。像下面这样：use_indent_to_bracket(to_indent,like_this) |

### 9：注意事项

<font color="red" > 修改配置文件后，需要关闭所有打开的文件，然后重启Sublime Text </font>
