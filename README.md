# 中山大学开题报告 LaTeX 模板

这是一个中文学位论文开题报告模板，使用 XeLaTeX 编译。封面和排版样式由 `sysuproposal.sty` 管理，主文件 `main.tex` 负责填写封面信息、设置目录和页码，并按顺序引入正文各章。

## 环境要求

- TeX Live（建议使用完整安装）
- XeLaTeX
- `ctex`、`gbt7714` 等模板依赖宏包
- 项目自带的 `font/` 字体文件
- 系统中可用的 Times New Roman 字体

## 编译

在项目根目录打开终端，运行两次 XeLaTeX，以生成 PDF 并更新目录和交叉引用：

```powershell
xelatex -interaction=nonstopmode -halt-on-error main.tex
xelatex -interaction=nonstopmode -halt-on-error main.tex
```

输出文件为 `main.pdf`。如果正文中使用了参考文献引用，先在 `ref.bib` 添加文献条目，再按以下顺序编译：

```powershell
xelatex main.tex
bibtex main
xelatex main.tex
xelatex main.tex
```

## 项目结构

```text
main.tex                              主文件：封面信息、目录、页码和正文引用顺序
sysuproposal.sty                      页面、字体、标题、目录、参考文献及封面样式
font/                                 模板使用的楷体、黑体和隶书字体
sec/                                  按一级章节拆分的正文文件
  01_background_significance.tex      研究背景与意义
  02_research_content.tex             研究内容
  03_research_scheme.tex              研究方案
  04_research_basis_plan.tex          研究基础与研究进展计划
  05_innovation_expected_results.tex  研究创新点与预期成果
ref.bib                               BibTeX 参考文献数据库
main.pdf                              编译生成的 PDF
```

## 修改封面信息

在 `main.tex` 导言区修改以下命令。学位层次可设为“博士”或“硕士”：

```latex
\degreelevel{博士}
\title{论文题目}
\author{姓名}
\stuid{学号}
\dept{院系}
\major{专业}
\research{研究方向}
\mentor{导师姓名及职称}
\date{2026 年 11 月 25 日}
```

## 编写和新增章节

每个一级章节单独放在 `sec/` 下的一个 `.tex` 文件中。章节文件中直接写 `\section{章节标题}`、对应的 `\subsection` 和正文内容；章节编号由 LaTeX 自动生成，不要在标题中手动写编号。

`main.tex` 中 `\input{...}` 的顺序决定章节在文档中的顺序。新增一级章节时：

1. 在 `sec/` 新建一个 `.tex` 文件，并写入 `\section{章节标题}` 和本章内容。
2. 在 `main.tex` 正文区域的对应位置添加 `\input{sec/文件名}`。
3. 重新编译两次，让目录更新。

正文内容只需编辑相应的 `sec/*.tex` 文件；封面、目录和页码等文档整体设置保留在 `main.tex`。
