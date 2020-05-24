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

Some essential packages are also included, pkg{array}, pkg{geometry}, pkg{graphicx}, pkg{titletoc}

However, most packages are included by `\RequirePackage{qyd-<pkg>}` command.
The `qyd-<pkg>.sty` is composed of two parts:
1. the aimed package is loaded by `\RequirePakcage{pkg}`.
2. the settings.

# pkg{geometry}
margin width is set to 0.25 width of the page.

# pkg{fancyhdr}

# pkg{tcolorbox}

# pkg{amsmath} pkg{amssymb}

# pkg{amsthm}

# pkg{ntheorem}

# pkg{listings}

# pkg{enumitem}

# pkg{marginnote}

# pkg{booktabs}

# pkg{longtables}

# pkg{tikz}

# pkg{algorithms}

# pkg{subcaption}

# pkg{xsim}

# pkg{}

# pkg{}

# pkg{}

# pkg{}

# pkg{sjqy} 钢筋符号输入
