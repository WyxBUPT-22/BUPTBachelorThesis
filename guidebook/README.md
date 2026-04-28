# 用户手册

这里是关于使用本模版的详细指导。

## 当前工作区版本

当前工作区中的模板已经裁剪为“论文主体版”，默认包含以下内容：

- 可选首页 PDF：`docs/cover.pdf`、`docs/statement.pdf`
- 中英文摘要与关键词
- 目录
- 五章正文示例
- 参考文献、致谢、附录、创新成果

以下材料已从默认编译流程中移除：任务书、成绩评定表、开题报告、中期检查表、教师指导记录表、外文资料原文、外文译文。

## 编译与编辑

完成 LaTeX 的环境安装后，即可在不同的编辑器中编辑、编译文档。

### VSCode

#### 安装扩展 `Latex Workshop`

首先，在 VSCode 中安装扩展 `Latex Workshop`（本手册使用 6.5.1 版）。

#### 设置扩展

安装完成后，对 `Latex Workshop` 进行工作区或用户设置。将下面的 JSON 字符串写入 `settings.json` 中：

```json
{
    "latex-workshop.latex.recipes": [
        {
            "name": "latexmk 🔃",
            "tools": [
                "xelatex",
                "bibtex",
                "xelatex",
                "xelatex"
            ]
        },
        {
            "name": "pdflatex ➞ bibtex ➞ pdflatex`×2",
            "tools": [
                "pdflatex",
                "bibtex",
                "pdflatex",
                "pdflatex"
            ]
        }
    ],
    "latex-workshop.latex.tools": [
        {
            "name": "latexmk",
            "command": "latexmk",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "-outdir=%OUTDIR%",
                "%DOC%"
            ],
            "env": {}
        },
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ],
            "env": {}
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
                "%DOCFILE%"
            ],
            "env": {}
        },
        {
            "name": "xelatex",
            "command": "xelatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        }
    ]
}
```

建议仅对当前工作区进行设置，以免影响 `Latex Workshop` 在其他地方的运行。

#### 开始使用

打开 `main.tex`，使用快捷键 `Ctrl + Alt + B`（`Cmd + Opt + B`）即可编译文档，并在同一目录下生成 `main.pdf`。

### Overleaf

[官方的使用指导](https://cn.overleaf.com/learn/how-to/Creating_a_document_in_Overleaf)  
BYRIO社区也提供了[校内服务](https://overleaf.byrio.work/)，如果遇到访问性问题可以使用校内服务。

### TEXMAKER

`TEXMAKER` 是一款免费的跨平台 LaTeX 编辑器，同时提供了图形化的编译界面。

下载地址：[texmaker](http://www.xm1math.net/texmaker/)

在软件中打开 `main.tex`，依次执行 `xelatex`、`bibtex`、`xelatex`、`xelatex` 即完成编译，并在同一目录下生成 `main.pdf`。
