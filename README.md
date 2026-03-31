# Response to Reviewers 通用模板说明

本仓库新增了一个可复用模板文件：

- `reviews/template.tex`

你可以：

- 直接复制整份模板作为某位审稿人的回复文件。
- 或者从本 README 里按块复制代码片段使用。

---

## 1. 文件结构与职责

- `Response_to_reviewers.tex`：主文件，负责整体版式和按审稿人 `\input`。
- `reviews/R1.tex` ~ `reviews/R4.tex`：每位审稿人的具体回复内容。
- `reviews/template.tex`：通用模板（新增）。

---

## 2. 快速开始（30 秒）

1. 复制模板文件（以 Reviewer 1 为例）：

~~~bat
copy reviews\template.tex reviews\R1.tex
~~~

2. 在主文件 `Response_to_reviewers.tex` 增加 Reviewer 1 区块并 `\input{reviews/R1.tex}`（下文有可复制示例）。

3. 在 `reviews/R1.tex` 中，把所有 `<...>` 占位符替换为你的实际内容。

---

## 3. 每一块怎么改（含示例，可直接复制）

### 块 A：审稿人总体意见 + 总体回复

作用：先放该审稿人的总评，再给一个总回应。

怎么改：

- 把 `<Paste the reviewer summary comment here>` 换成审稿人总评原文。
- 把 `<Write your high-level thanks and summary response here>` 换成整体感谢与总回应。

可复制代码块：

~~~latex
\reviewer

\begin{generalcomment}
  <Paste the reviewer summary comment here>
\end{generalcomment}
\begin{revmeta}[]
  <Write your high-level thanks and summary response here>
\end{revmeta}
~~~

示例（替换后）：

~~~latex
\reviewer

\begin{generalcomment}
  The paper studies a meaningful problem in graph unlearning,
  and the empirical results are promising.
\end{generalcomment}
\begin{revmeta}[]
  Thank you for your constructive comments. We have carefully revised
  the manuscript and addressed each point below.
\end{revmeta}
~~~

---

### 块 B：单条点对点回复（核心块）

作用：对应一条审稿意见，分三部分：评论、回复、修改内容。

怎么改：

- `revcomment` 里放审稿意见原文。
- `response` 里放你的解释/回应。
- `changes` 里明确“改了哪里”，建议写 section、page、equation、table、figure 等定位信息。

可复制代码块：

~~~latex
\begin{commentresponse}
  {\begin{revcomment}
    <Reviewer comment #1>
  \end{revcomment}}
  {\begin{response}
    <Your response to comment #1>
  \end{response}}
  {\begin{changes}
    <What changed in manuscript, include section/page/equation/table if possible>
  \end{changes}}
\end{commentresponse}
~~~

示例（替换后）：

~~~latex
\begin{commentresponse}
  {\begin{revcomment}
    The objective seems conceptually inconsistent with retrain-level unlearning.
  \end{revcomment}}
  {\begin{response}
    Thank you for this important point. We clarified the definition of
    retrain-level unlearning and aligned the objective description accordingly.
  \end{response}}
  {\begin{changes}
    We revised Section 3.2 (Page 6, Eq. (8)-(10)) and added explanatory text
    in Section 4.1 (Page 8).
  \end{changes}}
\end{commentresponse}
~~~

---

### 块 C：多条评论时如何扩展

作用：一条评论对应一个 `commentresponse`，有几条就复制几次。

怎么改：

- 每复制一次，替换为下一条评论与对应回复。
- 保持块的结构不变。

可复制代码块：

~~~latex
% Comment #2
\begin{commentresponse}
  {\begin{revcomment}
    <Reviewer comment #2>
  \end{revcomment}}
  {\begin{response}
    <Your response to comment #2>
  \end{response}}
  {\begin{changes}
    <What changed for comment #2>
  \end{changes}}
\end{commentresponse}

% Comment #3
\begin{commentresponse}
  {\begin{revcomment}
    <Reviewer comment #3>
  \end{revcomment}}
  {\begin{response}
    <Your response to comment #3>
  \end{response}}
  {\begin{changes}
    <What changed for comment #3>
  \end{changes}}
\end{commentresponse}
~~~

---

### 块 D：Disadvantage/格式问题回复(可选)

作用：如果审稿意见是“格式、排版、图表质量”等可归类为不足项，可使用该块。

怎么改：

- 默认是可选项，不需要就不写。
- 需要时，直接复制下面代码并替换 `<...>`。

可复制代码块：

~~~latex
\begin{commentdisadvantage}
  {\begin{discomment}
    <Disadvantage or formatting issue>
  \end{discomment}}
  {\begin{response}
    <Your response>
  \end{response}}
  {\begin{changes}
    <What changed>
  \end{changes}}
\end{commentdisadvantage}
~~~

示例（替换后）：

~~~latex
\begin{commentdisadvantage}
  {\begin{discomment}
    The manuscript contains excessive blank space on several pages.
  \end{discomment}}
  {\begin{response}
    Thank you for pointing this out. We adjusted page breaks and spacing.
  \end{response}}
  {\begin{changes}
    We fixed page layout issues in the revised manuscript and rechecked all
    figure/table placements.
  \end{changes}}
\end{commentdisadvantage}
~~~

---

### 块 E：该审稿人无逐条意见时（最简版本）

作用：当审稿人仅表示“无进一步意见”时，只保留总评和总回应即可。

可复制代码块：

~~~latex
\reviewer
\begin{generalcomment}
  I have no further comment.
\end{generalcomment}
\begin{revmeta}[]
  Thank you for your valuable suggestions in previous rounds.
\end{revmeta}
\clearpage
~~~

---

### 块 F：图示意（可直接放在 changes 里）

作用：当你希望在回复文件中直接展示一张示意图（如流程图、额外可视化）时使用。

注意：

- 推荐使用“非浮动”写法（不要用 `figure` 环境），因为当前回复块在表格单元中，浮动体可能报错。
- 需要在主文件导言区有 `\usepackage{graphicx}`（本仓库已补充）。

可复制代码块：

~~~latex
\begin{changes}
  We added an additional visualization to clarify the mechanism.

  \begin{center}
    \begin{minipage}{0.85\linewidth}
      \centering
      \includegraphics[width=\linewidth]{figures/rebuttal_overview.pdf}

      \small Figure S1. Overview of the updated method.
    \end{minipage}
  \end{center}
\end{changes}
~~~

示例（把占位路径改成你的图路径）：

~~~latex
\begin{changes}
  We add a pipeline sketch to explain the edge-unlearning procedure.

  \begin{center}
    \begin{minipage}{0.82\linewidth}
      \centering
      \includegraphics[width=\linewidth]{figures/edge_unlearning_pipeline.pdf}
      \small Figure S2. Edge-unlearning pipeline in the revised manuscript.
    \end{minipage}
  \end{center}
\end{changes}
~~~

---

### 块 G：表示意（可直接放在 changes 里）

作用：在回复中给一个小表格示意新增实验/消融结果。

注意：

- 同样建议“非浮动”写法（不要用 `table` 环境）。
- 推荐使用 `tabularx` + `minipage`，排版更稳定。

可复制代码块：

~~~latex
\begin{changes}
  We added an ablation summary as follows.

  \begin{center}
    \begin{minipage}{0.9\linewidth}
      \centering
      \setlength{\tabcolsep}{6pt}
      \begin{tabularx}{\linewidth}{lccc}
        \hline
        Setting & AUC & F1 & Time(s) \\
        \hline
        Retrain & 0.901 & 0.846 & 121.3 \\
        Ours    & 0.897 & 0.842 & 8.4   \\
        \hline
      \end{tabularx}

      \small Table S1. Ablation summary on Cora.
    \end{minipage}
  \end{center}
\end{changes}
~~~

示例（替换后）：

~~~latex
\begin{changes}
  We include a compact comparison for node unlearning.

  \begin{center}
    \begin{minipage}{0.92\linewidth}
      \centering
      \setlength{\tabcolsep}{5pt}
      \begin{tabularx}{\linewidth}{lccc}
        \hline
        Method & Accuracy & Forgetting & Time(s) \\
        \hline
        Retrain & 83.2 & 0.51 & 138.0 \\
        AMAU    & 82.7 & 0.53 & 9.6   \\
        \hline
      \end{tabularx}
      \small Table S2. Node unlearning comparison.
    \end{minipage}
  \end{center}
\end{changes}
~~~

---

## 4. 在主文件中挂载新审稿人（可复制）

如果需要新增 Reviewer 5，可在 `Response_to_reviewers.tex` 中按现有风格添加：

~~~latex
% Reviewer #5
\noindent\begin{tikzpicture}
  \draw[decoration=snake, chapterbg, decorate] (0,0) -- (16.4,0);
\end{tikzpicture}
\begin{center}
\Large\textbf{\textcolor{chapterbg}{Reviewer 5}}
\end{center}
\noindent\begin{tikzpicture}
  \draw[decoration=snake, chapterbg, decorate] (0,0) -- (16.4,0);
\end{tikzpicture}

\vspace{1em}
\input{reviews/R5.tex}
~~~

---

## 5. 建议的填写规范（提高通过率）

- 尽量逐条对应，不合并多个意见到一个回复里。
- `changes` 中尽量包含定位信息，例如：Section 3.2、Page 6、Eq. (8)。
- 能补实验就写“新增了什么实验 + 放在什么表/图”。
- 对无法完全满足的建议，要解释原因，并给出折中处理。

---

## 6. 一句话工作流

复制 `reviews/template.tex` -> 替换占位符 -> 必要时复制更多 `commentresponse` 块 -> 在主文件 `\input` 对应 reviewer 文件。
