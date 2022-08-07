# 本地TeX Live + XeLaTeX

**该方法为最推荐的本地编译方式.**

!!! info "提前准备的东西"

- 尽可能最新的TeX Live, 搭配一个编辑器(如`VSCode`, `Sublime Text`)更好

- 如果有旧版的`CTEX`套装, 请直接卸载

- 下载[最新版SSI模板](http://scis.scichina.com/download/ssi-template.zip)至本地

- 下载[picins宏包](http://mirrors.ctan.org/macros/latex209/contrib/picins.zip)至本地, 将压缩包解压后提取其中的`picins.sty`至SSI模板同一目录, **或者**将`picins.sty`移动至`texlive/texmf-local/tex/latex/picins`文件夹内(如果不存在需要自行创建), 并执行`texhash/mktexlsr`刷新宏包数据库

!!! info "使用步骤"

- 使用任何可以**改变文件编码**的编辑器, 将模板文件`SCIS2022cn.cls`的文件编码从`GB2312/GBK`调整为`UTF-8` (此处`2022`可能为其它年份)

- 修改模板文件`SCIS2022cn.cls`的如下加粗地方:

``` latex hl_lines="2 7 11" title="SCIS2022cn.cls"
\let\CCTCJKfonts=1
\LoadClass[twoside,CJK]{ctexart} % cctart -> ctexart
%% math packages
\RequirePackage{amsmath,amsthm,amsfonts,amssymb,bm,upgreek,multicol,mathrsfs,pifont,amscd,latexsym,geometry,color,fancyhdr}
...
\RequirePackage[pdfstartview=FitH,colorlinks,breaklinks,linkcolor=black,citecolor=black,filecolor=black,urlcolor=black,hyperindex,CJKbookmarks]{hyperref}
% \RequirePackage{breakurl} % 注释掉
\RequirePackage{titlesec}
...
\usepackage[bf,footnotesize,labelsep=quad]{caption}
% \captionsetup[subfloat]{labelformat=simple,captionskip=0pt} % 注释掉
\captionsetup[table]{aboveskip=1mm}
\captionsetup[figure]{aboveskip=3mm}
\captionsetup[algorithm]{font=footnotesize}
```

- 使用`XeLaTeX`编译

!!! tip "该方法的优点"

- 本地编译方式中**相对不折腾**的方法

- 与最新的TeX Live兼容性最好, 一般不会出现奇怪的编译问题和编码问题

- 投稿时一般不需要修改文章中的代码

!!! warning "该方法的不足"

- 字体略微与原生模板有所不同
