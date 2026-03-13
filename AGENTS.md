# AGENTS.md - 数学物理方法课程讲义

## 项目概述

本项目是一个数学物理方法课程的 LaTeX 讲义，涵盖复变函数、积分变换、数理方程和特殊函数四大部分。使用中文排版，基于 ctexbook 文档类。

## 编译命令

### 推荐编译器
```bash
# 使用 XeLaTeX 编译（推荐）
xelatex main.tex
xelatex main.tex  # 运行两次以生成正确的目录

# 或使用 LuaLaTeX
lualatex main.tex
lualatex main.tex
```

### 编译检查
```bash
# 编译并显示错误
xelatex -interaction=nonstopmode main.tex 2>&1 | grep "^!"

# 检查日志中的错误
grep -i "error" main.log
```

### 输出文件
- PDF 输出：`main.pdf`
- 日志文件：`main.log`
- 目录文件：`main.toc`

## 项目结构

```
math_phy/
├── main.tex          # 主文件（导言区、文档结构）
├── chapters/         # 章节文件
│   ├── preface.tex   # 前言
│   ├── ch01.tex      # 第一章：复数与复平面
│   ├── ch02.tex      # 第二章：复变函数
│   ├── ...
│   └── ch17.tex      # 第十七章：其他特殊函数简介
├── appendix/         # 附录
│   ├── appA.tex      # 常用公式表
│   ├── appB.tex      # 傅里叶变换表
│   ├── appC.tex      # 拉普拉斯变换表
│   ├── appD.tex      # 特殊函数公式
│   └── appE.tex      # 坐标系与微分算子
└── figures/          # 图片目录（如有）
```

## LaTeX 编码规范

### 必须遵守

1. **编码格式**：所有 .tex 文件使用 UTF-8 编码
2. **数学模式**：所有数学符号必须在数学环境内
   - 行内公式：`$...$` 或 `\(...\)`
   - 行间公式：`\begin{equation}...\end{equation}` 或 `\[...\]`
3. **中文排版**：使用 ctexbook 文档类，确保中文字体正确显示

### 禁止事项

1. **禁止使用 Unicode 数学符号**在文本模式中
   ```latex
   % 错误
   Γ(1/2) = √π
   
   % 正确
   $\Gamma(1/2) = \sqrt{\pi}$
   ```

2. **禁止不匹配的环境**
   ```latex
   % 错误
   \begin{equation}
   ...
   \end{equation    % 缺少右括号
   
   % 正确
   \begin{equation}
   ...
   \end{equation}
   ```

3. **禁止在章节文件中定义新环境**：所有自定义环境在 main.tex 中定义

4. **禁止使用直引号**：中文引号必须使用 LaTeX 标准格式
   ```latex
   % 错误
   "这门课到底学什么？"
   
   % 正确
   ``这门课到底学什么？''
   ```
   左引号用两个反引号 ``` `` ```，右引号用两个单引号 `''`。

## 自定义环境

### 定理类环境

| 环境 | 用途 | 编号 |
|------|------|------|
| `dingli` | 定理 | 按节编号 |
| `dingliyi` | 定义 | 按节编号 |
| `yinli` | 引理 | 按节编号 |
| `tuilun` | 推论 | 按节编号 |
| `lizi` | 例题 | 按节编号 |
| `zhu` | 注 | 按节编号 |
| `sikao` | 思考题 | 按节编号 |

### 解答环境

```latex
\begin{lizi}
    求解某问题。
    \begin{jie}
        解答内容。
    \end{jie}
\end{lizi}
```

### 提示框环境

```latex
% 警示框（红色）
\begin{jinshi}[标题]
    警告内容
\end{jinshi}

% 提示框（蓝色）
\begin{tishi}[标题]
    提示内容
\end{tishi}

% 物理背景框（绿色）
\begin{wulibj}[标题]
    物理背景说明
\end{wulibj}
```

## 章节结构模板

```latex
% 第N章：章节标题

\chapter{章节标题}

\begin{wulibj}[本章导读]
    章节概述和导读内容。
\end{wulibj}

% ========== 第一节 ==========
\section{节标题}

\subsection{小节标题}

% 内容...

% ========== 本章小结 ==========
\section{本章小结}

% ========== 习题 ==========
\section{习题}

\textbf{基础题}
\begin{enumerate}
    \item 题目
\end{enumerate}

\textbf{综合题}
\begin{enumerate}[resume]
    \item 题目
\end{enumerate}

\textbf{挑战题}
\begin{enumerate}[resume]
    \item 题目
\end{enumerate}
```

## 常用宏包

| 宏包 | 用途 |
|------|------|
| `amsmath, amssymb, amsthm` | 数学公式、定理 |
| `mathtools` | 数学工具扩展 |
| `physics` | 物理符号（偏导、积分等） |
| `tikz` | 绘图 |
| `pgfplots` | 函数图像 |
| `booktabs` | 专业表格 |
| `tcolorbox` | 彩色框 |
| `pifont` | 特殊符号（\ding） |

## TikZ 绘图规范

```latex
% 推荐的 TikZ 图形结构
\begin{figure}[htbp]
\centering
\begin{tikzpicture}[scale=1.0]
    % 坐标轴
    \draw[->, gray] (-1, 0) -- (5, 0) node[right] {$x$};
    \draw[->, gray] (0, -1) -- (0, 3) node[above] {$y$};
    
    % 图形内容
    \draw[blue, thick] plot coordinates {...};
    
    % 标注
    \node at (2, 1) {标签};
\end{tikzpicture}
\caption{图片标题}
\label{fig:label-name}
\end{figure}
```

### TikZ 注意事项

- 使用 `even odd rule` 而非 `even odd clip` 填充环形区域
- 中文标签使用 `$...$` 包裹数学符号

## 内容风格要求

1. **口语化讲解**：通俗易懂，循循善诱
2. **所有定理需证明**：使用 `proof` 环境或手写证明
3. **物理背景引入**：每节从物理问题出发
4. **图文并茂**：使用 TikZ 绘制示意图
5. **分层习题**：基础题 → 综合题 → 挑战题

## 讲义撰写要求

### 目标读者
- 大二下学期本科生
- 已修完高等数学、大学物理

### 内容范围
1. **第一篇：复变函数**（第1-6章）
   - 复数与复平面、复变函数、复积分、级数表示、留数理论、保角映射
2. **第二篇：积分变换**（第7-8章）
   - 傅里叶变换、拉普拉斯变换
3. **第三篇：数理方程**（第9-14章）
   - 方程导出与分类、行波法、分离变量法、积分变换法、格林函数法、其他方法
4. **第四篇：特殊函数**（第15-17章）
   - 勒让德函数、贝塞尔函数、其他特殊函数

### 核心撰写原则

#### 1. 物理背景与应用
- 每个概念从物理问题引入
- 先有物理动机，再有数学推导
- 示例：热传导方程从傅里叶定律导出，波动方程从弦振动导出

#### 2. 例题与习题设计
- **基础题**：直接应用公式和定理
- **综合题**：需要多个知识点综合运用
- **挑战题**：带有*标记，需要深入思考或查阅资料
- 例题必须给出完整解答，使用 `jie` 环境

#### 3. 可视化与几何直观
- 每节至少1-2个TikZ图
- 复平面、积分路径、驻波模式等必须配图
- 图形要标注清晰，使用 `figure` 环境和 `caption`

#### 4. 易错点与常见误区
- 使用 `jinshi` 环境标注易错点
- 示例：柯西-黎曼条件的充要性、留数的符号

#### 5. 符号与记号约定
- 复变量：$z = x + iy$，$w = f(z)$
- 积分路径：$C$，$\Gamma$
- 偏导数：$\frac{\partial u}{\partial x}$ 或简写 $u_x$
- 傅里叶变换：$\hat{f}(\omega)$ 或 $\mathcal{F}[f]$
- 拉普拉斯变换：$\tilde{f}(s)$ 或 $\mathcal{L}[f]$

#### 6. 与前修课程衔接
- 复变函数与高等数学中的多元函数对比
- 积分变换与傅里叶级数的关系
- 数理方程与常微分方程的联系
- 遇到困难内容时，提供微积分回顾（使用 `tishi` 环境）

#### 7. 章节结构标准
```
物理背景/引子 → 定义与定理 → 证明 → 例题 → 小结 → 习题
```

#### 8. 自学友好性
- 每章开头有「本章导读」
- 难度较高的章节标注 * 号
- 提供学习路径建议
- 重要公式用 `\boxed{}` 标注

#### 9. 历史注记（可选）
- 重要数学家的贡献
- 概念的历史发展
- 使用脚注或 `tishi` 环境

#### 10. 证明要求
- **所有定理必须给出证明**
- 证明使用 `proof` 环境
- 复杂证明可分为若干步骤
- 可补充证明思路或几何解释

### 写作风格
- **口语化**：像老师讲课一样娓娓道来
- **循循善诱**：从简单到复杂，从特殊到一般
- **自包含**：不依赖外部教材，所有内容自成体系
- **详细**：推导过程不跳步，关键步骤给出解释

### 章节写作检查清单
- [ ] 物理背景/引子
- [ ] 定义清晰
- [ ] 定理有证明
- [ ] 例题有解答
- [ ] TikZ图示
- [ ] 易错点提示
- [ ] 小结
- [ ] 分层习题（基础/综合/挑战）

## 常见编译错误排查

| 错误信息 | 原因 | 解决方案 |
|----------|------|----------|
| `Environment xxx undefined` | 环境未定义 | 在 main.tex 添加 `\newenvironment` |
| `Undefined control sequence` | 命令未定义 | 检查宏包是否加载 |
| `Missing $ inserted` | 数学符号在文本模式 | 使用 `$...$` 包裹 |
| 字符乱码 | 非法 Unicode 字符 | 使用 LaTeX 命令替代 |
