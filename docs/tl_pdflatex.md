# 本地TeX Live + PDFLaTeX + CCT

**该方法为最折腾的本地编译方式, 请谨慎选择该方法. 另一方面, 该方法可能对于其它中文模板的编译有所帮助.**

!!! info "提前准备的东西"

- 尽可能最新的TeX Live, 搭配一个编辑器(如`VSCode`, `Sublime Text`)更好

- 如果有旧版的`CTEX`套装, 请直接卸载

- 下载[最新版SSI模板](http://scis.scichina.com/download/ssi-template.zip)至本地

- 下载[picins宏包](http://mirrors.ctan.org/macros/latex209/contrib/picins.zip)至本地, 将`picins.sty`移动至`texlive/texmf-local/tex/latex/picins`文件夹内, 并执行`texhash/mktexlsr`刷新宏包数据库

- 下载[CCT宏包合集](./static/cct_ccmap_fonts_bundle.zip)至本地, 将解压后的目录结构(即`fonts`, `makeindex`和`tex`三个文件夹)移动至`texlive/texmf-local`文件夹内, 并执行`texhash/mktexlsr`刷新宏包数据库

!!! info "编译步骤"

- 为了避免PDF文件复制时出现乱码, 需要在`tex`源文件的导言区加入如下语句:

``` latex title="document.tex"
\documentclass{SCIS2022cn}
{++\usepackage{ccmap}++}
...
\begin{document}
...
```

- 修改模板文件`SCIS2022cn.cls`的如下加粗地方:

``` latex title="SCIS2022cn.cls"
...
{--\RequirePackage[pdfstartview=FitH,colorlinks,breaklinks,linkcolor=black,citecolor=black,filecolor=black,urlcolor=black,hyperindex,CJKbookmarks]{hyperref}--}
{++% \RequirePackage[pdfstartview=FitH,colorlinks,breaklinks,linkcolor=black,citecolor=black,filecolor=black,urlcolor=black,hyperindex,CJKbookmarks]{hyperref}++}
\RequirePackage{breakurl}
\RequirePackage{titlesec}
...
\usepackage[bf,footnotesize,labelsep=quad]{caption}
{--\captionsetup[subfloat]{labelformat=simple,captionskip=0pt}--}
{++% \captionsetup[subfloat]{labelformat=simple,captionskip=0pt}++}
\captionsetup[table]{aboveskip=1mm}
\captionsetup[figure]{aboveskip=3mm}
\captionsetup[algorithm]{font=footnotesize}
```

- 使用`PDFLaTeX`编译两次(或者使用`latexmk`这样的自动化工具)

!!! tip "该方法的优点"

- ~~没有什么优点~~, 唯一的优点就是锻炼动手能力

!!! warning "该方法的不足"

- 非常折腾, ~~如果没有相应字体会更加折腾~~

!!! info "额外的说明: 另外的编译方法"

- 直接参考[此页面](https://liam.page/2013/10/15/LaTeX-CCT-template/), 不需要下载其中的`CCT_TDS.zip`文件, 只需要在`tex`源文件`\begin{document}`之前加入如下语句:

``` latex title="document.tex"
\documentclass{SCIS2022cn}
...
{++\AtBeginDvi{\input{zhwinfonts}} ++}
\begin{document}
...
```

- 如果你使用了`TeX Live 2021`及以上版本, 由于`LaTeX3`的引入和`ifpdf`宏包的修改, `zhmetrics`中的`zhwinfonts`宏包已经不再适用, 需要进行修改:

``` latex title="texlive/xxxx/texmf-dist/tex/generic/zhmetrics/zhwinfonts.tex"
...
{--\input ifpdf.sty --}
{++\input iftex.sty ++}

\ifpdf
   \pdfmapline{=gbk@UGBK@ <simsun.ttc} 
   \pdfmapline{=gbksong@UGBK@ <simsun.ttc}
... 
```

!!! appendix "额外的说明"

- 由于调用字体的原因, 第一次编译耗时可能较长, 后续由于字体缓存已经被建立, 耗时不会很长

- 注释掉`hyperref`宏包的原因: 由于新版`hyperref`宏包与`CCT`不兼容, 此时如果出现`\section`, `\subsection`或者`\subsubsection`指令, 编译会报错: `TeX capacity exceeded, sorry [parameter stack size=10000]. \CCTSetChar #1#2-`, 注释掉该宏包对后续编译无影响

- `CCT`宏包中的字体由`CTEX`套装中的`FontSetup.exe`提取而来, 首先会得到一个`chinese`文件夹, 文件结构如下:

```text
/chinese
- /gbkfs
- /gbkhei
- /gbkkai
- /gbksong
- /unifs
- /unihei
- /unikai
- /unisong
```

- 此时直接编译文件仍然会缺失字体, 我们使用了如下脚本进行了字体转换:

```python title="convert_font.py"
for filename in os.listdir(source_dir):
    newfilename = filename.replace('song', '')
    os.rename(os.path.join(source_dir, filename), 
              os.path.join(source_dir, newfilename))
```
