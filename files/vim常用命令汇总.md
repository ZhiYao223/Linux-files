# 第一章

## 1. 安装vim

## 2. 启动vim

# 第二章

## 各种插入模式

- a ------在光标后插入
- o ------在当前行后插入一个新行
- O ------在当前行前插入一个新行
- cw ------替换从光标所在位置后到一个单词结尾的字符

## 简单的移动光标

- 0 ------数字零，到行头
- ^ ------到本行地一个不是blank(空格、tab、换行、回车)字符的位置
- $ ------到本行行尾
- g_ ----到本行最后一个不是blank字符的位置
- `/pattern`*→ 搜索* `pattern` *的字符串（陈皓注：如果搜索出多个匹配，可按n键到下一个）*



## 拷贝、粘贴

- `P` → 粘贴
- `yy` → 拷贝当前行当行于 `ddP`
- p/P都可以，p是表示在当前位置之后，P表示在当前位置之前
- 

## 撤回、重复操作 Undo/Redo

- `:e <path/to/file>` → 打开一个文件
- `:w` → 存盘
- `:saveas <path/to/file>` → 另存为 `<path/to/file>`
- `:x`， `ZZ` 或 `:wq` → 保存并退出 (`:x` 表示仅在需要时保存，ZZ不需要输入冒号并回车)
- `:q!` → 退出不保存 `:qa!` 强行退出所有的正在编辑的文件，就算别的文件有更改。
- `:bn` 和 `:bp` → 你可以同时打开很多文件，使用这两个命令来切换下一个或上一个文件。（陈皓注：我喜欢使用:n到下一个文件）

# 第三章

下面，让我们看一下vim是怎么重复自己的：

1. `.` → (小数点) 可以重复上一次的命令
2. N<command> → 重复某个命令N次

下面是一个示例，找开一个文件你可以试试下面的命令：

## 提升光标效率

1. N`G` → 到第 N 行 （陈皓注：注意命令中的G是大写的，另我一般使用 : N 到第N行，如 :137 到第137行）

2. `gg` → 到第一行。（陈皓注：相当于1G，或 :1）

3. `G` → 到最后一行。

4. 按单词移动:

   >1. `w` → 到下一个单词的开头。
   >2. `e` → 到下一个单词的结尾。
   >
   >\> 如果你认为单词是由默认方式，那么就用小写的e和w。默认上来说，一个单词由字母，数字和下划线组成（陈皓注：程序变量）
   >
   >\> 如果你认为单词是由blank字符分隔符，那么你需要使用大写的E和W。（陈皓注：程序语句）
   >
   >![image-20240429164742090](/home/zhiyao/.config/Typora/typora-user-images/image-20240429164742090.png)

## 最强的光标移动

- `%` : 匹配括号移动，包括 `(`, `{`, `[`. （陈皓注：你需要把光标先移到括号上）
- `*` 和 `#`:  匹配光标当前所在的单词，移动光标到下一个（或上一个）匹配单词（*是下一个，#是上一个）

很多命令都可以和这些移动光标的命令连动。很多命令都可以如下来干：

```
<start position><command><end position>
```

例如 `0y$` 命令意味着：

- `0` → 先到行头
- `y` → 从这里开始拷贝
- `$` → 拷贝到本行最后一个字符

你可可以输入 `ye`，从当前位置拷贝到本单词的最后一个字符。

你也可以输入 `y2/foo` 来拷贝2个 “foo” 之间的字符串。

还有很多时间并不一定你就一定要按y才会拷贝，下面的命令也会被拷贝：

- `d` (删除 )
- `v` (可视化的选择)
- `gU` (变大写)
- `gu` (变小写)
- 等等



# 第四章

## 在当前行上移动光标:

`0` `^` `$` `f` `F` `t` `T` `,` `;`

> - `0` → 到行头
> - `^` → 到本行的第一个非blank字符
> - `$` → 到行尾
> - `g_` → 到本行最后一个不是blank字符的位置。
> - `fa` → 到下一个为a的字符处，你也可以fs到下一个为s的字符。
> - `t,` → 到逗号前的第一个字符。逗号可以变成其它字符。
> - `3fa` → 在当前行查找第三个出现的a。
> - `F` 和 `T` → 和 `f` 和 `t` 一样，只不过是相反方向。
>   ![Line moves](http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/line_moves.jpg)

还有一个很有用的命令是 `dt"` → 删除所有的内容，直到遇到双引号—— `"。`

## 区域选择 

`<action>a<object>` 或 `<action>i<object>`

在visual 模式下，这些命令很强大，其命令格式为

```
<action>a<object>` 和 `<action>i<object>
```

- action可以是任何的命令，如 `d` (删除), `y` (拷贝), `v` (可以视模式选择)。
- object 可能是： `w` 一个单词， `W` 一个以空格为分隔的单词， `s` 一个句字， `p` 一个段落。也可以是一个特别的字符：`"、` `'、` `)、` `}、` `]。`

假设你有一个字符串 `(map (+) ("foo"))`.而光标键在第一个 `o `的位置。

> - `vi"` → 会选择 `foo`.
> - `va"` → 会选择 `"foo"`.
> - `vi)` → 会选择 `"foo"`.
> - `va)` → 会选择`("foo")`.
> - `v2i)` → 会选择 `map (+) ("foo")`
> - `v2a)` → 会选择 `(map (+) ("foo"))`

![Text objects selection](http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/textobjects.png)

## 块操作: `<C-v>`

块操作，典型的操作： `0 <C-v> <C-d> I-- [ESC]`

- `^` → 到行头
- `<C-v>` → 开始块操作
- `<C-d>` → 向下移动 (你也可以使用hjkl来移动光标，或是使用%，或是别的)
- `I-- [ESC]` → I是插入，插入“`--`”，按ESC键来为每一行生效。

![Rectangular blocks](http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/rectangular-blocks.gif)

在Windows下的vim，你需要使用 `<C-q>` 而不是 `<C-v>` ，`<C-v>` 是拷贝剪贴板。

## 自动提示： `<C-n>` 和 `<C-p>`

在 Insert 模式下，你可以输入一个词的开头，然后按 `<C-p>或是<C-n>，自动补齐功能就出现了……`

``![Completion](http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/completion.gif)

## 宏录制： 

`qa` 操作序列 `q`, `@a`, `@@`

- `qa` 把你的操作记录在寄存器 `a。`
- 于是 `@a` 会replay被录制的宏。
- `@@` 是一个快捷键用来replay最新录制的宏。

> ***示例\***
>
> 在一个只有一行且这一行只有“1”的文本中，键入如下命令：
>
> - ```
>   qaYp<C-a>q
>   ```
>
>   →
>
>   - `qa` 开始录制
>   - `Yp` 复制行.
>   - `<C-a>` 增加1.
>   - `q` 停止录制.
>
> - `@a` → 在1下面写下 2
>
> - `@@` → 在2 正面写下3
>
> - 现在做 `100@@` 会创建新的100行，并把数据增加到 103.

![Macros](http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/macros.gif)

## 可视化选择

`v`,`V`,`<C-v>`

前面，我们看到了 `<C-v>`的示例 （在Windows下应该是<C-q>），我们可以使用 `v` 和 `V`。一但被选好了，你可以做下面的事：

- `J` → 把所有的行连接起来（变成一行）
- `<` 或 `>` → 左右缩进
- `=` → 自动给缩进 （陈皓注：这个功能相当强大，我太喜欢了）

![Autoindent](http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/autoindent.gif)

在所有被选择的行后加上点东西：

- `<C-v>`
- 选中相关的行 (可使用 `j` 或 `<C-d>` 或是 `/pattern` 或是 `%` 等……)
- `$` 到行最后
- `A`, 输入字符串，按 `ESC。`

![Append to many lines](http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/append-to-many-lines.gif)

## 分屏 

`:split` 和 `vsplit`.

下面是主要的命令，你可以使用VIM的帮助 `:help split`. 你可以参考本站以前的一篇文章[VIM分屏](https://coolshell.cn/articles/1679.html)。

> - `:split` → 创建分屏 (`:vsplit`创建垂直分屏)
> - `<C-w><dir>` : dir就是方向，可以是 `hjkl` 或是 ←↓↑→ 中的一个，其用来切换分屏。
> - `<C-w>_` (或 `<C-w>|`) : 最大化尺寸 (<C-w>| 垂直分屏)
> - `<C-w>+` (或 `<C-w>-`) : 增加尺寸

![Split](http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/split.gif)

## 查看进程

`ps -ef`查看进程信息

`ps -ef | grep <keyword> ` 过滤指定关键字进程信息

`kill [-9] 进程号PID` 关闭指定进程号的进程







