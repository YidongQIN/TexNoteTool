TexTakingNote
=======

My own LaTeX template for taking notes.

# Features
1. Personal perferance for layout and package settings.
   * each package's setting is a single `qyd-<pkg>.sty` file, so it could be used in other documents.
2. Printable materials for knowledge organization and sharing.
   * Inspired by **Feynman Technique**.

# cls{ctex}
In order to use this template for both English and Chinese note, the `ctex` class is loaded.

Some essential packages are also included, pkg{qyd-array}, pkg{qyd-geometry}, pkg{qyd-graphicx}, pkg{qyd-titletoc}

However, most packages are included by `\RequirePackage{qyd-<pkg>}` command.
The `qyd-<pkg>.sty` is composed of two parts:
1. the aimed package is loaded by `\RequirePakcage{pkg}`.
2. the settings.

# pkg{qyd-geometry}
margin width is set to 0.25 width of the page.

# pkg{qyd-fancyhdr}
Three kinds of page style.

# pkg{qyd-tcolorbox}
Colored fancy box.

# pkg{qyd-amsmath} pkg{qyd-amssymb} pkg{qyd-ntheorem}

# pkg{qyd-listings}
1. Programming Language Definition.
2. Highlight

# pkg{qyd-enumitem}

# pkg{qyd-marginnote}

# pkg{qyd-table}
Some package for Table environment.

# pkg{qyd-algorithms}
`pkg{algorithm}` and `pkg{algorithmic}`

# pkg{qyd-figure}
`pkg{graphicx}` and `pkg{subcaption}`

# pkg{qyd-xsim}

# 带圈数字

众所周知，$LaTeX$ 提供了 `\textcircled` 命令用以给字符加圈，但效果却不怎么好。

stone-zeng 相当完备地总结了[带圈数字](https://stone-zeng.github.io/2019-02-09-circled-numbers/) 的实现方法。
复现了他的方案，同时为了避免以后重复劳动，把这几种处理方法定义成命令，制作成宏包。

## pkg{qyd-pifont-circlednum}
传统的实现带全数字的方法，是利用 Pifont 字体的 `\ding{<number>}` 命令调用杂锦符号（dingbats）。

![](https://stone-zeng.github.io/images/circled-numbers/pifont.svg)

带圈的数字$1~10$，区分了阴阳文、衬线与非衬线搭配，共有40个。

|        |     阳文      |     阴文      |
| :----: | :-----------: | :-----------: |
|  衬线  | $172 \to 181$ | $182 \to 191$ |
| 非衬线 | $192 \to 201$ | $202 \to 211$ |

### 实现
为 4 种样式分别定义了命令。
* `\pifontrm{}`
* `\pifntrmy{}`
* `\pifontsf{}`
* `\pifntsfy{}`

代码体内部用 `\numexpr\value{#1}+171` 把传入的计数器数字运算到目标区间，然后用 `\ding{}` 调用带圈数字。

### 优势
* 经过设计的字体与样式，总体来说是最美观的。
* 主流 TEX 引擎下都可以使用。

### 劣势
* 数字只有1到10 （也有说可以找到20，暂未验证）。
* 接受参数是 `<number>` 即计数器数字，不是输入字符。所以跟其它几种方法相比，灵活性不足。

## pkg{qyd-tikz-textcircled}
用大名鼎鼎的 Tikz 直接在某个字符外绘制圆圈。

### 实现
几份绘制代码稍有不同，最终采用的是 [StackExchange](https://tex.stackexchange.com/questions/7032/good-way-to-make-textcircled-numbers#) 的这份答案。
因为它不是固定的浮动、圆圈尺寸，而是根据填充内容变化的。

### 优势
* 接受的是一个文字，所以最具有灵活性（数字、字母、字符等）。

### 劣势
* 如果内容过多，圆圈过大。
* 占据更大的水平距离。
* 需要用 `\arabic` 等命令把计数器数字转化为数字文本。

## pkg{qyd-xuni-textcircled} 与 pkg{qyd-hook-textcircled}

### 原理 Unicode
数字 0–50 的带圈版本都分配了对应的 Unicode 码位，因而在现代 TEX 引擎（X⁠E⁠TEX 和 Lua­TEX）中，配合合适的字体，理论上可以直接输入这些符号。

|            | 0     | 1     | 2     | 3     | 4     | 5     | 6     | 7     | 8     | 9     | 10   |
| ---------- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ---- |
| 带圈       | ⓪     | ①     | ②     | ③     | ④     | ⑤     | ⑥     | ⑦     | ⑧     | ⑨     | ⑩    |
|            | 24EA  | 2460  | 2461  | 2462  | 2463  | 2464  | 2465  | 2466  | 2467  | 2468  | 2469 |
|            |       | ⑪     | ⑫     | ⑬     | ⑭     | ⑮     | ⑯     | ⑰     | ⑱     | ⑲     | ⑳    |
|            |       | 246A  | 246B  | 246C  | 246D  | 246E  | 246F  | 2470  | 2471  | 2472  | 2473 |
|            |       | ㉑    | ㉒    | ㉓    | ㉔    | ㉕    | ㉖    | ㉗    | ㉘    | ㉙    | ㉚   |
|            |       | 3251  | 3252  | 3253  | 3254  | 3255  | 3256  | 3257  | 3258  | 3259  | 325A |
|            |       | ㉛    | ㉜    | ㉝    | ㉞    | ㉟    | ㊱    | ㊲    | ㊳    | ㊴    | ㊵   |
|            |       | 325B  | 325C  | 325D  | 325E  | 325F  | 32B1  | 32B2  | 32B3  | 32B4  | 32B5 |
|            |       | ㊶    | ㊷    | ㊸    | ㊹    | ㊺    | ㊻    | ㊼    | ㊽    | ㊾    | ㊿   |
|            |       | 32B6  | 32B7  | 32B8  | 32B9  | 32BA  | 32BB  | 32BC  | 32BD  | 32BE  | 32BF |
| 反白       | ⓿     | ❶     | ❷     | ❸     | ❹     | ❺     | ❻     | ❼     | ❽     | ❾     | ❿    |
|            | 24FF  | 2776  | 2777  | 2778  | 2779  | 277A  | 277B  | 277C  | 277D  | 277E  | 277F |
|            |       | ⓫     | ⓬     | ⓭     | ⓮     | ⓯     | ⓰     | ⓱     | ⓲     | ⓳     | ⓴    |
|            |       | 24EB  | 24EC  | 24ED  | 24EE  | 24EF  | 24F0  | 24F1  | 24F2  | 24F3  | 24F4 |
| 无衬线     | 🄋     | ➀     | ➁     | ➂     | ➃     | ➄     | ➅     | ➆     | ➇     | ➈     | ➉    |
|            | 1F10B | 2780  | 2781  | 2782  | 2783  | 2784  | 2785  | 2786  | 2787  | 2788  | 2789 |
| 无衬线反白 | 🄌     | ➊     | ➋     | ➌     | ➍     | ➎     | ➏     | ➐     | ➑     | ➒     | ➓    |
|            | 1F10C | 278A  | 278B  | 278C  | 278D  | 278E  | 278F  | 2790  | 2791  | 2792  | 2793 |
| 双线       |       | ⓵     | ⓶     | ⓷     | ⓸     | ⓹     | ⓺     | ⓻     | ⓼     | ⓽     | ⓾    |
|            |       | 24F5  | 24F6  | 24F7  | 24F8  | 24F9  | 24FA  | 24FB  | 24FC  | 24FD  | 24FE |
| 加框       |       | ㉈    | ㉉    | ㉊    | ㉋    | ㉌    | ㉍    | ㉎    | ㉏    |       |      |
|            |       | 3248  | 3249  | 324A  | 324B  | 324C  | 324D  | 324E  | 324F  |       |      |
| 带圆括号   |       | ⑴     | ⑵     | ⑶     | ⑷     | ⑸     | ⑹     | ⑺     | ⑻     | ⑼     | ⑽    |
|            |       | 2474  | 2475  | 2476  | 2477  | 2478  | 2479  | 247A  | 247B  | 247C  | 247D |
|            |       | ⑾     | ⑿     | ⒀     | ⒁     | ⒂     | ⒃     | ⒄     | ⒅     | ⒆     | ⒇    |
|            |       | 247E  | 247F  | 2480  | 2481  | 2482  | 2483  | 2484  | 2485  | 2486  | 2487 |
| 带点       | 🄀     | ⒈     | ⒉     | ⒊     | ⒋     | ⒌     | ⒍     | ⒎     | ⒏     | ⒐     | ⒑    |
|            | 1F100 | 2488  | 2489  | 248A  | 248B  | 248C  | 248D  | 248E  | 248F  | 2490  | 2491 |
|            |       | ⒒     | ⒓     | ⒔     | ⒕     | ⒖     | ⒗     | ⒘     | ⒙     | ⒚     | ⒛    |
|            |       | 2492  | 2493  | 2494  | 2495  | 2496  | 2497  | 2498  | 2499  | 249A  | 249B |
| 带逗号     | 🄁     | 🄂     | 🄃     | 🄄     | 🄅     | 🄆     | 🄇     | 🄈     | 🄉     | 🄊     |
|            | 1F101 | 1F102 | 1F103 | 1F104 | 1F105 | 1F106 | 1F107 | 1F108 | 1F109 | 1F10A |
| 汉字括号   |       | ㈠    | ㈡    | ㈢    | ㈣    | ㈤    | ㈥    | ㈦    | ㈧    | ㈨    | ㈩   |
|            |       | 3220  | 3221  | 3222  | 3223  | 3224  | 3225  | 3226  | 3227  | 3228  | 3229 |
| 汉字圆圈   |       | ㊀    | ㊁    | ㊂    | ㊃    | ㊄    | ㊅    | ㊆    | ㊇    | ㊈    | ㊉   |
|            |       | 3280  | 3281  | 3282  | 3283  | 3284  | 3285  | 3286  | 3287  | 3288  | 3289 |

直接输入，或者利用码位，都能在 LATEX 中使用以上这些带圈数字。

```latex
①
\symbol{"2776}
\char"3248\
^^^^3280
^^^^^1f229
```

但是仍旧非常麻烦。所以推荐采用 `xunicode-addon` 宏包（从属于 xeCJK）显示 Unicode 所分配的带圈数字（和字母等）。

### 实现
[刘海洋的回答](https://www.zhihu.com/question/29557216) 给出了实用的实现方法。

1. 引用 `fontspec` 和 `xunicode-addon` 宏包。
2. 设定可以支持带圈数字的字体。比如 `ipag.ttf` 等。
3. 【可选】为了在中文环境 `ctex` 中也能正常时使用，需要把对应码位设定为西文字体（Default类）。如果在纯英文环境中，这一步可以省略。
4. 调用 `\textcircled` 命令时切换到步骤2设定的字体。

   1. 通俗的习惯是，在需要圆圈的命令时，局部改变字体 `{\xxxFontFamily \textcircled{}}` 。

      这也是 `{qyd-xuni-textcircled}` 采用做法。

   2. 粗暴的方法是用钩子 `\AtBeginUTFCommand[]{}` 和 `\AtEndUTFCommand` ，锁住 `\textcircled` 命令。

      见 `{qyd-hook-circled-number}` 的设置。

带圈数字的使用与**字体**密切相关。
stone-zeng 整理了一些常用的、自带的字体，及其适用范围。

| 字体                                  | 带圈  | 反白  | 无衬线 | 无衬线反白 |
| ------------------------------------ | :---: | :---: | :----: | :--------: |
| IPAGothic 和 IPAMincho               | 1–50  | 1–20  |        |            |
| （思源）宋体、黑体                     | 0–50  | 0–20  |  0–10  |    0–10    |
| Junicode                             | 0–20  | 0–20  |        |            |
| DejaVuSans                           | 1–10  | 1–10  |  1–10  |    1–10    |
| FreeSerif                            | 1–10  | 1–10  |  1–10  |    1–10    |
| STIX Two Math                        | 0–20  | 0–20  |  1–10  |    1–10    |
| 微软雅黑、微软正黑                      | 1–10  |       |        |            |
| （方正）书宋、黑体、楷体、仿宋、等线    | 1–10  |       |        |            |
| （中易）宋体、黑体、楷体、仿宋          | 1–10  |       |        |            |

### 优势
* 选择合适的字体，甚至可以满足三位数的序号。其它方法难以处理。

### 劣势
* 需要自己设定数字字体，而有的字体确实会缺失某些编号。
* 如果采用钩子方法，则字体不易更改，**所有**的圆圈只能采用统一的字体；通俗做法可以在不同命令的定义中灵活选择字体样式。

# pkg{qyd-footnote}

建议调用 `{footmisc}` 宏包，开启底端、每页等选项。
而且也方便样式更改。

1. 重新定义 `\footnoterule` 更改分割线的样式。
2. 脚注中的编号竖向居中，来源是[刘海洋的回答](https://www.zhihu.com/question/53030087)。
3. 使用带圈数字作为编号。
   1. 用 `kvoptions` 接受一个字符串型的选项变量。
   2. 根据输入选项，用多个 `\if` 决定不同的圆圈样式。
   3. 重定义 `\thefootnote` 。
4. 更改脚注中编号与文字的间距 `\footnotemargin`。
5. 更改脚注中文字的样式 `\footnotelayout`。
   这个命令可以用于在脚注文字生成前加入粗体、斜体、字号等等命令。

在这个过程中，尝试过用 `\csname...\endcsname` 和 `\expandafter` 组合，让选项直接成为命令。
但这时候才发现，两类带圈数字的方法输入参数不同：
1. pifont 方法需要的是记录在计数器中的数值，需要参与运算。
2. xunicode 和 tikz 需要输入的是文本，前者通过更改样式满足原生的 `\textcircled` 的排版需求，后者不改变输入的文本而是在外侧绘制更大、更对齐的圆形。

所以说，这个想法暂时难以实现，也没有必要。

# pkg{qyd-sjqy} 钢筋符号输入
利用 SJQY.ttf 字体生成钢筋一级到五级的符号。
定义为形如 `\stA` 的命令。
