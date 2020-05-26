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

# pkg{qyd-tcolorbox}

# pkg{qyd-amsmath} pkg{qyd-amssymb}

# pkg{qyd-amsthm}

# pkg{qyd-ntheorem}

# pkg{qyd-listings}

# pkg{qyd-enumitem}

# pkg{qyd-marginnote}

# pkg{qyd-booktabs}

# pkg{qyd-longtables}

# pkg{qyd-tikz}

# pkg{qyd-algorithms}

# pkg{qyd-subcaption}

# pkg{qyd-xsim}

# 带圈数字

众所周知，$LaTeX$ 提供了 `\textcircled` 命令用以给字符加圈，但效果却不怎么好。

stone-zeng 相当完备地总结了[带圈数字](https://stone-zeng.github.io/2019-02-09-circled-numbers/) 的实现方法。
复现了他的方案，同时为了避免以后重复劳动，把这几种处理方法定义成命令，制作成宏包。

## pkg{qyd-pifont-circlednum}
传统的实现带全数字的方法，是利用 Pifont 字体的 `\ding{<number>}` 命令调用杂锦符号（dingbats）。

带圈的数字$1~10$，区分了阴阳文、衬线与非衬线搭配，共有40个。
![](https://stone-zeng.github.io/images/circled-numbers/pifont.svg)

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
* 数字只有1到10.
* 接受参数是 `<number>` 即计数器数字，不是输入字符。所以跟其它几种方法相比，灵活性不足

# pkg{qyd-tikz-textcircled}

# pkg{qyd-xuni-textcircled}

## pkg{qyd-hook-textcircled}


# pkg{qyd-footnote}

# pkg{qyd-}

# pkg{qyd-sjqy} 钢筋符号输入
