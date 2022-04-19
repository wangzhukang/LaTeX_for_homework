# 在VSCode中使用LaTeX写作业

本项目致力于帮助LaTeX初学者尽快上手，并用其在VSCode环境中完成简单的日常作业。作者本人也是LaTeX新手，因此本项目中难免会有错误和不妥，欢迎大家批评指正。

## 如何操作

### 环境配置

1. 下载安装TexLive，并添加到环境变量。是否成功验证方法：快捷键WIN+R，键入cmd，输入`tex --version`，如果输出一长串英文字符，则安装成功。
2. 下载安装VSCode，点击左侧扩展管理，搜索`LaTeX Workshop`，安装此扩展。
3. VSCode中，快捷键Ctrl+Shift+P，搜索`settings`，选择`Preferences: Open Settings(JSON)`，并做出如下配置：

```json
{
  // LaTex配置

  // 当编译失败时，删除多余文件
  "latex-workshop.latex.autoClean.run": "onFailed",
  // 需要清除的文件类型
  "latex-workshop.latex.clean.fileTypes": [
    "*.aux",
    "*.bbl",
    "*.blg",
    "*.idx",
    "*.ind",
    "*.lof",
    "*.lot",
    "*.out",
    "*.toc",
    "*.acn",
    "*.acr",
    "*.alg",
    "*.glg",
    "*.glo",
    "*.gls",
    "*.ist",
    "*.fls",
    "*.log",
    "*.fdb_latexmk"
  ],
  "latex-workshop.latex.recipe.default": "lastUsed",
  // 反向搜索定位时，采用双击的方法
  "latex-workshop.view.pdf.internal.synctex.keybinding": "double-click",
  // 文件发生改变自动编译
  "latex-workshop.latex.autoBuild.run": "onFileChange",
  // 使用vscode内置的tab预览pdf文件
  "latex-workshop.view.pdf.viewer": "tab",
  "latex-workshop.showContextMenu": true,
  "latex-workshop.intellisense.package.enabled": true,
  "latex-workshop.message.error.show": false,
  "latex-workshop.message.warning.show": false,
  // LaTex编译配置
  "latex-workshop.latex.tools": [
    {
      "name": "xelatex",
      "command": "xelatex",
      "args": [
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "%DOCFILE%"
      ]
    },
    {
      "name": "pdflatex",
      "command": "pdflatex",
      "args": [
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "%DOCFILE%"
      ]
    },
    {
      "name": "latexmk",
      "command": "latexmk",
      "args": [
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "-pdf",
        "-outdir=%OUTDIR%",
        "%DOCFILE%"
      ]
    },
    {
      "name": "bibtex",
      "command": "bibtex",
      "args": ["%DOCFILE%"]
    }
  ],
  "latex-workshop.latex.recipes": [
    {
      "name": "XeLaTeX",
      "tools": ["xelatex"]
    },
    {
      "name": "PDFLaTeX",
      "tools": ["pdflatex"]
    },
    {
      "name": "BibTeX",
      "tools": ["bibtex"]
    },
    {
      "name": "LaTeXmk",
      "tools": ["latexmk"]
    },
    {
      "name": "xelatex -> bibtex -> xelatex*2",
      "tools": ["xelatex", "bibtex", "xelatex", "xelatex"]
    },
    {
      "name": "pdflatex -> bibtex -> pdflatex*2",
      "tools": ["pdflatex", "bibtex", "pdflatex", "pdflatex"]
    }
  ],
}
```

### 正式开始

使用VSCode打开工作文件夹work，可以修改任意`.tex`文件。保存后会自动编译，点击右上角的`View LaTeX PDF file`按键可以实时预览生成的`.pdf`文件。

### 文档介绍

文件夹work中包含image子文件夹，以及main，settings和problem系列`.tex`文件。

- image子文件夹作用是存放作业中可能需要用的图片。
- main是主文件。只有这一个文件会被编译成pdf文件，同时产生`.aux`，`.log`等附加文件。main主要工作方式是依次input各problem文件，使各个作业题按顺序显示在pdf文件中。
- settings是相关设置，包含文档类声明、宏包声明、样式设置、自定义的环境和命令等等，在main的最开始就要input进去。
- problem系列文件描述各个问题及其解答。之所以每道题单独成一个文件，是为了方便更改和整体搬迁。每个problem文件的格式基本上是先叙述题干，再给出解答。其中用到了settings中自定义的`solution`和`myfigure`环境。

### 后记

对于settings.json中的配置以及各`.tex`模板文档，可根据自己需求修改完善。关于TeXLive以及VSCode的安装，请移步互联网。关于LaTeX的相关知识，请参考互联网或刘海洋《LaTeX入门》。
