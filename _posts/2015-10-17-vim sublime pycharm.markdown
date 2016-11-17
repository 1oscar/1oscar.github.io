---
layout: post
title: "vim sublime pycharm"
comments: true
share: true
tags: tools
---

I1. **pycharm,vim,sublime这三种工具都曾经在某一段时间段里分别被我长期使用过，现在工作更喜欢三者结合着用，大型的项目或者总是需要查看函数定义的地方使用pycharm,跑服务器上修改代码使用vim，其他小程序，或者文本文件更钟情于sublime，这里做一个总结。**

I2. **vim**<br>
[**我的vim配置**](https://github.com/1oscar/exercises/tree/master/dkf_vim)
平时使用vim没有那么配置什么插件之类，主要还是偶尔用，不频繁<br>
这里有大牛介绍<br>
[**插件**](http://zuyunfei.com/categories/Vim/)<br>
[**大牛常用的插件**](http://www.zlovezl.cn/articles/my-vim-plugins-for-python/)<br>
[**gtihub管理插件**](http://skoo.me/vim/2013/09/18/vim-plugin-manager/)<br>
[**像IDE一样使用vim**](https://github.com/yangyangwithgnu/use_vim_as_ide)<br>
[**vim IDE说明**](http://blog.csdn.net/wklken/article/details/9076621)<br>
[**tmux与vim**](http://blog.jobbole.com/87585/)<br>
[**tmux与vim**](http://blog.jobbole.com/87584/)<br>

**平时使用的基于目前的vim的快捷键**
mac下

```
移动至行尾   ：  shift +4 
移动至该行下一个空格处: shift + e
删除鼠标所在行的后面内容： shit + d
:%s/A/B/g   :表示B替换A
h, j, k, l分别代表向左、下、上、右移动;
分屏后屏间切换，只需要先按一下Ctrl+W+[h/j/k/l]或者Ctrl+W(w点击两下)
CTRL-B和CTRL-F:翻页
在当前行内快速移动:“f“命令移动到光标右边的指定字符上，例如，”fx“，会把移动到光标右边的第一个’x’字符上。”F“命令则反方向查找，也就是移动到光标左边的指定字符上。”3fx“表示移动到光标右边的第3个’x’字符上
移动到行首的命令非常简单，就是”0“.移动到行尾的命令是”$“。命令”^“，用它可以移动到行首的第一个非空白字符。
移动光标到下一个单词的词首，使用命令”w“，移动光标到上一个单词的词首，使用命令”b“；移动光标到下一个单词的结尾，用命令”e“，移动光标到上一个单词的结尾，使用命令”ge“。
”/“是向下查找，而”?“进行反方向查找;":/"是全文查找，查找到某个单词后"n"是各个单词间的切换.
```

I3. **sublime** <br>
[**install**](http://www.sublimetext.com/2)<br>
注册码:

```
----- BEGIN LICENSE -----
Andrew Weber
Single User License
EA7E-855605
813A03DD 5E4AD9E6 6C0EEB94 BC99798F
942194A6 02396E98 E62C9979 4BB979FE
91424C9D A45400BF F6747D88 2FB88078
90F5CC94 1CDC92DC 8457107A F151657B
1D22E383 A997F016 42397640 33F41CFC
E1D0AE85 A0BBD039 0E9C8D55 E1B89D5D
5CDB7036 E56DE1C0 EFCC0840 650CD3A6
B98FC99C 8FAC73EE D2B95564 DF450523
------ END LICENSE ------
```

**包控制**
[**install package control**](https://packagecontrol.io/installation)<br>
Command+Shift+P(Mac) : 打开命令面板,输入 “Package Control: Install Package“即会列出全部可以安装的扩展<br>
[**包扩展页面**](https://packagecontrol.io/)

```
1.ConvertToUTF8： ST2只支持utf8编码，该插件可以显示与编辑 GBK, BIG5, EUC-KR, EUC-JP, Shift_JIS 等编码的
2. cTags: 追踪函数
3. Code Alignment用于代码格式的自动
4.Sublime​REPL编辑界面直接运行 Python 解释器
:Tools -> SublimeREPL -> Python
5. git 
```

**setting** <br>
preferences->Settings-User:(下面是我精挑细选的配置)

```
{
    "color_scheme": "Packages/Color Scheme - Default/Monokai.tmTheme",
    // 按space或tab时，实际会产生白色的点（一个空格一个点）或白色的横线
    // 设置为none时，什么情况下都不显示这些点和线
    // 设置为selection时，只显示选中状态下的点和线
    // 设置为all时，则一直显示
    "draw_white_space": "all",
    "font_size": 12.0,
    "ignored_packages"://屏蔽不想调用的 packages
    [
        "Vintage"
    ],
    "translate_tabs_to_spaces": true,//设为true时，缩进和遇到Tab键时使用空格替代
    "highlight_line": true,// 高亮当前行
    "fold_buttons": true, //显示代码折叠按钮(鼠标移动到左边才显示)
    "line_numbers": true,  //显示行号
    "scroll_past_end": true,//即滚到最后一行后，可以继续向下滚，让整屏只显示最后一行
    "word_wrap": true,  //自动换行
    "wrap_width": 80     //一行显示单词长度
}
```

**use**

```
如何use git:
Command+Shift+P(Mac) : 命令面板
输入“Git:init”来初始化git化境。 ST2会让你选择需要初始化的Git目录，选择到你的工程目录即可
使用Git:status来查看当前的状态。
git:add命令添加新增加的文件
git:commit，来提交更改,Sublime Text会自动跳出一个文本文件，你可以在文件的最上方输入这次更改的comments，然后直接关闭这个文件，就会出发commit操作.ctrl+w关闭文件的同时，commit操作自动触发。
```
**快捷键**

```sql
常用的:
<Ctrl><]>
增加当前行的缩进, 选中多行时多行增加缩进
<Ctrl><[>
减少当前行的缩进, 选中多行时多行减少缩进
<Ctrl><k>+<b>
打开关闭侧边栏
<Ctrl><`>
打开控制台(当前文件目录下)
快速列出/跳转函数就是 Ctrl+R (Mac下是Command+R)
Command+Shift+P(Mac) : 命令面板
Ctrl+~:  调出控制台
command+d:单击一次选出光标所在单词一次，单击两次继续向下同时选中下一个相同的文本进行同时编辑.
command+b: 运行python
Ctrl + Shift + L可以将当前选中区域打散，然后进行同时编辑
Ctrl + J可以把当前选中区域合并为一行
Ctrl + G然后输入行号以跳转到指定行
Ctrl + N在当前窗口创建一个新标签
Ctrl + Shift + N创建一个新窗口
Alt + command + 2进行左右分屏
Alt + command + 5进行上下左右分屏（即分为四屏）

Mac下默认的快捷键:
备注：具体符号对应的按键
⌘Command key
⌃Control key
⌥Option key
⇧Shift Key

为了方便大家记忆，将快捷键分成了8个类型， 分别为

Edit(编辑)
Selection(光标选中)
Find(查找）
View(视图)
Go to(跳转)
Project(工程)
General(通用)
Tabs(标签)
Edit(编辑)
⌘[向左缩进 | Left indent
⌘]向右缩进 | Right Indent
⌘⌃↑与上一行互换（超实用！）| Swap line up
⌘⌃↓与下一￼行互换￼（超实用！）| Swap line down
⌘⇧D复制粘贴当前行（减少多余的粘贴）| Duplicate line
⌘J拼接行（css格式化时挺有用） | join lines
⌘←去往行的开头 | Beginning of line
⌘→去往行末尾 | End of line
⌘⌃/块注释 | Toggle comment block
⌃K从光标开始的地方删除到行尾 | Delete to end
⌃⇧K删除一整行 | delete line
⌃T相邻单词互换位置，在','前试用，有惊喜（很有趣）| Transpose
⌘⇧↩向光标前插入一行|insert line before
⌘↩向光标后插入一行|inter line after
⌘⌥T插入特殊字符|Special characters
⌃D向后删除（很怪异的操作，不过感觉很酷炫）
Selection(光标选中)
⌘D选中相同的词 | Expand selection to words
⌃⌘G多重文本光标选中（再也不用⌘ D一个一个的找啦）| Expand all selection to words
⌘L选中一行|Expand selection to line
Esc单选（取消多重选择）|Single selection,Cancel multiple selections
⌃⇧↑一行一行向上选中|Add previous line
⌃⇧↓一行一行向下选中|Add next line
⌘⇧L将选中的区域分割成多行选中状态(多光标操作状态)|Split into lines
⌥+拖动鼠标多重光标选中
⌘⇧J已缩进层级为依据，一层层向外选中|Expand selection to indentation
⌃⇧M将匹配括号中的内容选中|Expand selection to brackets
Find(查找)
⌘F普通查找|Find
⌘G查找下一个|Find next
⌘⇧F在文件夹中查找| Find in files
⌘⇧E缓存用于替换的内容，方便之后的替换|Use selection for replace
⌘E缓存用于查找的内容，方便之后的查找|Use selection for find
⌘⌥E一个接一个往下替换|Replace next
View(视图)
推荐使用Origami插件，可以随意对sublime进行分割
Go to(跳转/定位)
⌘P跳转文件（很方便）| Go to anything
⌘R定位文件中的方法@| Go to symbol
⌘G定位文件中的行号:| Go to line
⌃M定位匹配的括号 | Jump to matching bracket
⌘F2设置/取消定位标记| Toggle bookmark
F2跳转到定位标记处 | Next bookmark
⌘⇧F2清除所有定位标记| Clear all bookmarks
⌘⌥→下一个打开的文件| Next file
```

**windows平台快捷键设置**

```

{
	"color_scheme": "Packages/Color Scheme - Default/Monokai.tmTheme",
	"draw_white_space": "all",
	"fold_buttons": true,
	"font_size": 13,
	"highlight_line": true,
	"ignored_packages":
	[
		"Vintage"
	],
	"line_numbers": true,
	"scroll_past_end": true,
	"translate_tabs_to_spaces": true,
	"word_wrap": true,
	"wrap_width": 80
}

```

I4. **pycharm**<br>
[**install**](https://www.jetbrains.com/pycharm/download/) <br>
注册码: <br>

```
user: newasp
License key:
09086-12042010
00001EBwqd8wkmP2FM34Z05iXch1Ak
KI0bAod8jkIffywp2WalWZejIQ6AAu
AVVPbzHZpOvqvdJFHEBbvbXW2t1jQI
```
**配置** <br>
preferences->Appearance->Theme: Darcula <br>
跳转函数定义处: command
其余和sublime里差不多




