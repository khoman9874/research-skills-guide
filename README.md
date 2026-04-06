# Research Skills - 安装与使用指南

> **学术研究工作流技能集合**：3 个核心技能，覆盖开题报告、文献综述、幻灯片制作

---

## 📋 目录

- [简介](#简介)
- [技能概览](#技能概览)
- [安装步骤](#安装步骤)
- [research-proposal 详解](#research-proposal-详解)
- [medical-imaging-review 详解](#medical-imaging-review-详解)
- [paper-slide-deck 详解](#paper-slide-deck-详解)
- [使用场景](#使用场景)
- [常见问题](#常见问题)

---

## 简介

Research Skills 是一个由 luwill 开发的学术研究工作流技能集合，包含 3 个核心技能：

1. **research-proposal**：生成博士研究提案
2. **medical-imaging-review**：写医学影像综述论文
3. **paper-slide-deck**：从论文生成专业幻灯片

**GitHub Stars**：310（增长 48%）
**许可证**：MIT License
**支持平台**：Claude Code、Cursor、Codex 等

---

## 技能概览

| 技能 | 触发词 | 核心功能 | 输出 |
|------|--------|---------|------|
| **research-proposal** | `/research-proposal`、"研究计划"、"PhD proposal" | 生成 2,000-4,000 字博士研究提案 | Markdown + 质量检查清单 |
| **medical-imaging-review** | `/medical-imaging-review`、"综述"、"survey" | 写医学影像 AI 综述论文 | 完整综述稿件 |
| **paper-slide-deck** | `/paper-slide-deck paper.pdf` | 从论文生成幻灯片 | PPTX/PDF + PNG 图片 |

---

## 安装步骤

### 前提条件

- **Claude Code** 或其他支持 Agent Skills 标准的 AI 代理
- **Python 3.8+**（用于 paper-slide-deck 脚本）
- **Zotero**（可选，用于文献管理）

### 方法 1：全局安装（推荐）

```bash
# 1. 克隆仓库
cd ~
git clone https://github.com/luwill/research-skills.git

# 2. 创建技能目录
mkdir -p ~/.claude/skills

# 3. 安装所有技能
cp -r ~/research-skills/research-proposal ~/.claude/skills/
cp -r ~/research-skills/medical-imaging-review ~/.claude/skills/
cp -r ~/research-skills/paper-slide-deck ~/.claude/skills/
```

### 方法 2：项目本地安装

```bash
# 在项目根目录
mkdir -p .agents/skills

# 安装特定技能
cp -r ~/research-skills/research-proposal .agents/skills/
```

### 方法 3：选择性安装

**只安装 research-proposal**：
```bash
git clone https://github.com/luwill/research-skills.git
cp -r research-skills/research-proposal ~/.claude/skills/
```

**只安装 medical-imaging-review**：
```bash
git clone https://github.com/luwill/research-skills.git
cp -r research-skills/medical-imaging-review ~/.claude/skills/
```

**只安装 paper-slide-deck**：
```bash
git clone https://github.com/luwill/research-skills.git
cp -r research-skills/paper-slide-deck ~/.claude/skills/

# 安装脚本依赖
cd ~/.claude/skills/paper-slide-deck/scripts
npm install  # TypeScript 脚本
pip install PyMuPDF  # PDF 处理
```

### 验证安装

重启 Claude Code，然后输入：
```
/research-proposal
```

如果技能已正确安装，Claude 会激活该技能并开始提问。

---

## research-proposal 详解

### 核心功能

生成**博士研究提案**，适用于 PhD 申请、开题报告、研究计划书。

**目标输出**：2,000-4,000 字（默认 3,000 字）

### 5 阶段工作流程

```
Phase 1: 需求收集 → 主题、领域、语言、字数
    ↓
Phase 2: 文献收集 → WebSearch + Zotero + arXiv + PubMed
    ↓
Phase 3: 大纲生成 → 用户确认（必须！）
    ↓
Phase 4: 内容写作 → 基于批准的大纲生成全文
    ↓
Phase 5: 输出审核 → Markdown + 质量检查清单
```

### 标准结构

```markdown
# [研究标题]

## 摘要（150-300 字，5-10%）

## 1. 引言（500-800 字，15-20%）
### 1.1 背景与上下文
### 1.2 问题陈述
### 1.3 研究问题/目标
### 1.4 范围与界限

## 2. 文献综述（500-1000 字，20-25%）
### 2.1 理论框架
### 2.2 研究现状
### 2.3 研究空白分析
### 2.4 本研究定位

## 3. 研究方法（500-800 字，20-25%）
### 3.1 研究设计
### 3.2 数据收集方法
### 3.3 数据分析方法
### 3.4 效度与局限

## 4. 时间线（200-300 字，5-10%）
### 4.1 研究阶段
### 4.2 关键里程碑

## 5. 意义与预期贡献（200-400 字，10-15%）
### 5.1 理论贡献
### 5.2 实践意义
### 5.3 更广泛影响

## 参考文献（最少 40 篇）
```

### 文献收集策略

| 文献来源 | 用途 | 工具 |
|---------|------|------|
| **WebSearch** | 最新综述、研究趋势、突破新闻 | 内置搜索 |
| **Zotero MCP** | 用户上传的付费文献 | Zotero 插件 |
| **arXiv** | 最新预印本、开放获取论文 | arXiv MCP |
| **PubMed** | 同行评审临床研究 | PubMed MCP |

**重要**：提醒用户在开始前上传相关付费文献到 Zotero。

### 写作风格要求

#### ✅ 学术谨慎语言（Hedging）

| 避免 | 使用 |
|------|------|
| "will prove" | "aims to demonstrate" |
| "definitely" | "likely", "potentially" |
| "is obvious" | "evidence suggests" |
| "proves" | "indicates", "demonstrates" |

#### ✅ 流畅散文风格（避免列表）

❌ **错误**（点对点列举）：
```
贡献包括：
- 新颖的分割算法
- 多模态融合框架
- 临床验证研究
```

✅ **正确**（流畅散文）：
```
本研究预计将通过几个相互关联的贡献推进该领域。首先，新颖分割算法
的开发将使自动化斑块检测的准确率超越现有方法。在此基础上，多模态
融合框架将整合互补的成像数据，捕捉单一模态无法获得的斑块特征。最后，
严格的临床验证将确立这些计算生物标志物在预测心血管事件方面的预后价值。
```

#### ✅ 段落结构

```
主题句（主要论点）
  → 支持证据（引用 + 数据）
  → 分析（批判性评估）
  → 过渡到下一段
```

### 图表建议

**重要**：在适当位置包含 3-5 个图表建议。

**格式**：
```markdown
> **[图 1 建议]** *标题：提议的研究框架概览*
> 内容：展示三阶段研究设计的流程图或示意图，显示从成像模态到
> AI 处理再到临床结果的数据流。包括 CCTA/IVUS/OCT 输入、深度
> 学习模块和输出预测的图标。
> 推荐风格：清晰的矢量图形，配色一致。
```

**图表类型建议**：

| 章节 | 建议图表类型 |
|------|------------|
| 引言 | 概念图展示研究范围和定位 |
| 文献综述 | 关键发展时间线；现有方法分类 |
| 研究方法 | 研究框架流程图；网络架构图；数据处理流程 |
| 时间线 | 甘特图展示研究阶段和里程碑 |
| 意义 | 影响图展示理论和实践贡献 |

### 质量检查清单

#### 结构
- [ ] 所有必需章节存在
- [ ] 字数在指定范围内
- [ ] 章节间逻辑流畅
- [ ] 清晰的章节标题

#### 内容
- [ ] 研究问题清晰陈述
- [ ] 文献综述识别具体空白
- [ ] 研究方法适合研究问题
- [ ] 时间线现实且详细
- [ ] 意义清晰表达

#### 学术风格
- [ ] 全文正式学术语气
- [ ] 使用适当的谨慎语言
- [ ] 章节间过渡流畅
- [ ] 无口语或非正式表达
- [ ] **流畅散文**（最少化项目符号/列表）

#### 图表
- [ ] **包含 3-5 个图表建议**
- [ ] 图表建议包括标题、内容描述和风格推荐
- [ ] 图表分布在各章节（不聚集）
- [ ] 每个图表达成清晰的交流目的

#### 引用
- [ ] 所有主张有参考文献支持
- [ ] 引用格式一致
- [ ] **博士提案最少 40 篇参考文献**
- [ ] 包含近期文献（约 60% 来自最近 5 年）
- [ ] 适当引用开创性/基础性工作

### 使用示例

**示例 1：MBA 论文开题报告**

```
/research-proposal

我想写一篇关于"数字化转型对企业绩效影响"的 MBA 论文开题报告。
领域：管理学
目标期刊：《管理世界》
字数：3,000 字
语言：中文
```

**示例 2：博士申请研究提案**

```
/research-proposal

Research Topic: Deep Learning for Coronary Artery Plaque Analysis
Domain: STEM (Computer Science / Medical Imaging)
Language: English
Word Count: 3,500 words
Target Institution: Stanford University, School of Medicine

I have uploaded relevant literature to Zotero about:
- Coronary CT angiography segmentation
- Plaque characterization using deep learning
- Clinical validation of AI biomarkers
```

### 格式转换

```bash
# 转换为 Word 文档
pandoc proposal.md -o proposal.docx

# 转换为 PDF（需要 LaTeX）
pandoc proposal.md -o proposal.pdf

# 转换为 PDF（自定义样式）
pandoc proposal.md -o proposal.pdf --template=academic.latex
```

---

## medical-imaging-review 详解

### 核心功能

写**医学影像 AI 综述论文**，适用于 survey papers、systematic reviews、literature analyses。

**目标输出**：完整综述稿件（80-120 篇参考文献）

### 7 阶段工作流程

```
Phase 1: 项目初始化 → 创建 CLAUDE.md、IMPLEMENTATION_PLAN.md、manuscript_draft.md
    ↓
Phase 2: 文献收集 → arXiv + PubMed + Zotero
    ↓
Phase 3: 文献分类 → 按方法类别组织
    ↓
Phase 4: 内容写作 → 按模板逐节撰写
    ↓
Phase 5: 表格与图表 → 比较表格、方法图表
    ↓
Phase 6: 审稿与完善 → 质量检查清单
    ↓
Phase 7: 最终输出 → Markdown 稿件
```

### 支持的医学影像领域

- **冠状动脉分析**（CCTA）
- **肺部成像**（CT/X-ray）
- **脑成像**（MRI/CT）
- **心脏成像**（MRI/CT/Echo）
- **病理学**（全切片图像）
- **视网膜成像**（Fundus/OCT）

### 标准综述结构

```markdown
# [标题]：最新进展与未来方向

## 关键要点
- [3-5 个要点总结主要发现]

## 摘要

## 1. 引言
### 1.1 临床背景
### 1.2 技术挑战
### 1.3 范围与贡献

## 2. 数据集与评估指标
### 2.1 公开数据集（表 1）
### 2.2 评估指标

## 3. 深度学习方法
### 3.1 [类别 1]
### 3.2 [类别 2]
（表 2：方法比较）

## 4. 下游应用

## 5. 商业产品与临床转化（表 3）

## 6. 讨论
### 6.1 当前局限
### 6.2 未来方向

## 7. 结论

## 参考文献
```

### 方法描述模板

```markdown
### 3.X [方法类别]

[1-2 段介绍与动机]

**[方法名称]：** [作者] et al. [ref] 提出了 [方法]，该 [创新点]：
- [关键组件 1]
- [关键组件 2]
在 [数据集] 上达到 Dice X.XX。

**局限性：** 尽管有优势，[类别] 方法面临：
(1) [限制 1]；(2) [限制 2]。
```

### 引用模式

```markdown
# 数据引用
"...达到 Dice 0.89 [23]"

# 方法引用
"Gu et al. [45] 提出了..."

# 多引用
"多项研究显示... [12, 15, 23]"

# 比较引用
"虽然 [12] 专注于...，但 [15] 解决了..."
```

### 核心原则

#### ✅ 谨慎语言（Hedging）

- 使用 "may", "suggests", "appears to", "has shown promising results"
- 避免 "X is the best method"
- 每个主张需要参考文献

#### ✅ 必需元素

- **关键要点框**（3-5 个要点）在标题后
- **比较表格**针对每个主要章节
- **性能指标**：Dice (0.XXX), HD95 (X.XX mm)
- **图表占位符**附带详细标题
- **参考文献**：80-120 篇典型，按主题组织

#### ✅ 段落结构

```
主题句（主要论点）
  → 支持证据（引用 + 数据）
  → 分析（批判性评估）
  → 过渡到下一段
```

### 文献来源策略

| 来源 | 最佳用途 | 工具 |
|------|---------|------|
| **ArXiv** | 最新 DL 方法、预印本 | `search_papers`, `read_paper` |
| **PubMed** | 临床验证、同行评审 | `pubmed_search_articles` |
| **Zotero** | 现有库、组织的参考文献 | `zotero_search_items` |

### 使用示例

**示例 1：冠状动脉分割综述**

```
/medical-imaging-review

Write a comprehensive review on "Deep Learning for Coronary Artery 
Segmentation in CCTA" covering:
- U-Net variants
- Attention mechanisms
- Multi-scale approaches
- Clinical applications

Domain: Coronary Artery Analysis (CCTA)
Target venue: Medical Image Analysis
```

**示例 2：肺部 AI 综述（中文）**

```
/medical-imaging-review

写一篇关于"肺部 CT 图像 AI 分析"的综述论文，包括：
- 肺结节检测
- 肺部分割
- COVID-19 诊断
- 临床转化

领域：肺部成像（CT/X-ray）
语言：中文
```

---

## paper-slide-deck 详解

### 核心功能

从学术论文或内容生成**专业幻灯片**，支持：
- 自动图表检测
- AI 生成视觉效果
- 17 种视觉风格
- PPTX/PDF 导出

### 使用方法

```bash
# 从 PDF 生成
/paper-slide-deck path/to/paper.pdf

# 从 Markdown 生成
/paper-slide-deck path/to/content.md --style academic-paper

# 指定风格和受众
/paper-slide-deck path/to/content.md --style sketch-notes --audience beginners

# 指定语言和幻灯片数量
/paper-slide-deck path/to/content.md --lang zh --slides 10

# 只生成大纲
/paper-slide-deck path/to/content.md --outline-only
```

### 17 种视觉风格

| 风格 | 描述 | 最佳用途 |
|------|------|---------|
| **academic-paper** | 清晰专业，精确图表 | 会议演讲、论文答辩 |
| **blueprint**（默认） | 技术示意图，网格纹理 | 架构、系统设计 |
| **chalkboard** | 黑板，彩色粉笔 | 教育、教程、课堂 |
| **notion** | SaaS 仪表板，卡片布局 | 产品演示、SaaS、B2B |
| **bold-editorial** | 杂志封面，粗体字，深色 | 产品发布、主题演讲 |
| **corporate** | 海军蓝/金色，结构化布局 | 投资者演示、提案 |
| **dark-atmospheric** | 电影级深色模式，发光点缀 | 娱乐、游戏 |
| **editorial-infographic** | 杂志解释，平面插图 | 科技解释、研究 |
| **fantasy-animation** | 吉卜力/迪士尼风格，手绘 | 教育、讲故事 |
| **intuition-machine** | 技术简报，双语标签 | 技术文档、学术 |
| **minimal** | 超干净，最大留白 | 高管简报、高端 |
| **pixel-art** | 复古 8 位，像素块 | 游戏、开发者演讲 |
| **scientific** | 学术图表，精确标签 | 生物、化学、医学 |
| **sketch-notes** | 手绘，温暖友好 | 教育、教程 |
| **vector-illustration** | 平面矢量，复古可爱 | 创意、儿童内容 |
| **vintage** | 老旧纸张，历史风格 | 历史、遗产、传记 |
| **watercolor** | 手绘纹理，自然温暖 | 生活方式、健康、旅行 |

### 自动风格选择

| 内容信号 | 选择的风格 |
|---------|----------|
| paper, thesis, defense, conference, ieee, acm, icml, neurips | `academic-paper` |
| tutorial, learn, education, guide, intro, beginner | `sketch-notes` |
| classroom, teaching, school, chalkboard | `chalkboard` |
| architecture, system, data, analysis, technical | `blueprint` |
| creative, children, kids, cute, illustration | `vector-illustration` |
| briefing, bilingual, infographic, concept | `intuition-machine` |
| executive, minimal, clean, simple, elegant | `minimal` |
| saas, product, dashboard, metrics | `notion` |
| investor, quarterly, business, corporate | `corporate` |
| launch, marketing, keynote, bold, impact | `bold-editorial` |
| entertainment, music, gaming, creative | `dark-atmospheric` |
| explainer, journalism, science communication | `editorial-infographic` |
| story, fantasy, animation, magical | `fantasy-animation` |
| gaming, retro, pixel, developer | `pixel-art` |
| biology, chemistry, medical, pathway | `scientific` |
| history, heritage, vintage, expedition | `vintage` |
| lifestyle, wellness, travel, artistic | `watercolor` |

### 工作流程

```
Step 1: 分析内容 → 保存源文件、深度分析
    ↓
Step 2: 生成大纲 → 带风格指令、IMAGE_SOURCE 映射
    ↓
Step 3: 提取图表 → 自动检测 + AI 生成
    ↓
Step 4: 应用模板 → 学术图表容器模板
    ↓
Step 5: 生成幻灯片 → Gemini API 图像生成
    ↓
Step 6: 合并输出 → PPTX/PDF 导出
```

### 文件管理

每次会话创建独立目录：

```
slide-deck/{topic-slug}/
├── source-{slug}.{ext}    # 源文件
├── outline.md             # 大纲
├── prompts/               # 提示词
│   └── 01-slide-cover.md, 02-slide-{slug}.md, ...
├── 01-slide-cover.png, 02-slide-{slug}.png, ...  # 生成的幻灯片
├── {topic-slug}.pptx      # PowerPoint 文件
└── {topic-slug}.pdf       # PDF 文件
```

### 布局选项

#### 幻灯片特定布局

| 布局 | 描述 | 最佳用途 |
|------|------|---------|
| `title-hero` | 大标题居中 + 副标题 | 封面幻灯片、章节分隔 |
| `quote-callout` | 特色引用 + 署名 | 证言、关键洞察 |
| `key-stat` | 单个大数字作为焦点 | 影响统计、指标 |
| `split-screen` | 半图半文 | 功能亮点、比较 |
| `icon-grid` | 图标网格 + 标签 | 功能、能力、优势 |
| `two-columns` | 平衡列内容 | 配对信息、双点 |
| `three-columns` | 三列内容 | 三重比较、类别 |
| `bullet-list` | 结构化项目符号 | 简单内容、列表 |

#### 学术特定布局

| 布局 | 描述 | 最佳用途 |
|------|------|---------|
| `paper-title` | 标题、作者、单位、会议 | 会议论文封面 |
| `outline-agenda` | 编号章节列表 + 高亮 | 演讲结构概览 |
| `methods-diagram` | 中心架构/流程图 | 方法、系统设计 |
| `results-chart` | 图表区域 + 数据注释 | 定量结果 |
| `equation-focus` | 居中方程 + 变量定义 | 数学推导 |
| `qualitative-grid` | 2x2 或 3x2 图像比较网格 | 视觉结果、消融实验 |
| `references-list` | 编号引用列表 | 关键参考文献幻灯片 |
| `contributions` | 编号贡献点 | 贡献总结 |

### 脚本依赖

```bash
# TypeScript 脚本
cd ~/.claude/skills/paper-slide-deck/scripts
npm install

# Python 依赖
pip install PyMuPDF  # PDF 处理
pip install google-generativeai  # Gemini API
```

### 使用示例

**示例 1：从论文 PDF 生成学术幻灯片**

```
/paper-slide-deck ~/papers/deep-learning-cardiac.pdf --style academic-paper --slides 15
```

**示例 2：从 Markdown 生成教程幻灯片**

```
/paper-slide-deck ~/notes/machine-learning-tutorial.md --style sketch-notes --audience beginners --lang zh
```

**示例 3：只生成大纲**

```
/paper-slide-deck ~/content.md --outline-only
```

---

## 使用场景

### 场景 1：博士申请

**推荐技能**：`research-proposal`

**工作流程**：
```
1. 使用 research-proposal 生成研究提案
   - 输入：研究方向、目标院校、字数
   - 输出：3,000 字研究提案 + 质量检查清单

2. 准备答辩幻灯片
   - 使用 paper-slide-deck 从提案生成幻灯片
   - 风格：academic-paper 或 minimal
   - 受众：专家（教授、招生委员会）

3. 准备相关文献综述
   - 使用 medical-imaging-review（如果是医学影像领域）
   - 或使用 research-proposal 的文献收集功能
```

**示例提示词**：
```
/research-proposal

Research Topic: AI-Driven Precision Medicine for Cardiovascular Disease
Domain: STEM (Biomedical Informatics)
Language: English
Word Count: 3,500 words
Target Institution: Harvard Medical School

I have uploaded 15 relevant papers to Zotero about:
- Deep learning for cardiac imaging
- Precision medicine in cardiology
- Clinical decision support systems
```

---

### 场景 2：医学影像综述论文

**推荐技能**：`medical-imaging-review`

**工作流程**：
```
1. 初始化综述项目
   - 创建 CLAUDE.md、IMPLEMENTATION_PLAN.md
   - 定义综述范围和领域

2. 系统性文献搜索
   - arXiv：最新 DL 方法
   - PubMed：临床验证研究
   - Zotero：已收集的文献

3. 分类和组织文献
   - 按方法类别
   - 按应用领域
   - 按性能指标

4. 按模板撰写各章节
   - 引言、数据集、方法、应用、讨论、结论

5. 创建比较表格
   - 方法比较表
   - 数据集表
   - 商业产品表

6. 质量检查
   - 使用 QUALITY_CHECKLIST.md
   - 确保最少 80-120 篇参考文献

7. 准备演讲幻灯片
   - 使用 paper-slide-deck 从综述生成幻灯片
```

**示例提示词**：
```
/medical-imaging-review

Write a systematic review on "Deep Learning for Lung Nodule Detection 
in CT Scans" covering:

1. Detection methods (R-CNN variants, U-Net, attention mechanisms)
2. Public datasets (LIDC-IDRI, LUNA16, NLST)
3. Performance metrics (sensitivity, specificity, FROC)
4. Clinical validation studies
5. Commercial products and FDA approvals
6. Future directions (federated learning, multimodal fusion)

Domain: Lung Imaging (CT)
Target venue: Radiology
Word Count: ~8,000 words
```

---

### 场景 3：论文答辩准备

**推荐技能组合**：`paper-slide-deck` + `research-proposal`

**工作流程**：
```
1. 从论文 PDF 生成答辩幻灯片
   /paper-slide-deck thesis.pdf --style academic-paper --slides 20

2. 准备开题报告（如果是中期答辩）
   /research-proposal

3. 准备 Q&A 环节
   - 使用 paper-slide-deck 生成补充幻灯片
   - 风格：minimal 或 blueprint
   - 包含方法细节、额外结果

4. 准备海报（可选）
   - 使用 paper-slide-deck 的 infographic 风格
```

**示例提示词**：
```
/paper-slide-deck ~/thesis/defense.pdf --style academic-paper --slides 20 --lang zh

生成中文答辩幻灯片，包括：
- 研究背景与动机
- 文献综述
- 研究方法
- 实验结果
- 贡献与未来工作
- 致谢
```

---

### 场景 4：课程教学材料

**推荐技能**：`paper-slide-deck`

**工作流程**：
```
1. 从课程笔记生成教学幻灯片
   /paper-slide-deck lecture-notes.md --style chalkboard --audience beginners

2. 生成教程材料
   /paper-slide-deck tutorial.md --style sketch-notes --lang zh

3. 创建概念解释图表
   /paper-slide-deck concept.md --style editorial-infographic
```

**示例提示词**：
```
/paper-slide-deck ~/teaching/machine-learning-basics.md --style chalkboard --audience beginners --slides 30

生成机器学习基础课程幻灯片，包括：
- 监督学习
- 无监督学习
- 模型评估
- 实践案例
```

---

## 常见问题

### Q1: 这三个技能可以一起使用吗？

**答**：可以！推荐工作流：
1. 用 `research-proposal` 生成开题报告
2. 用 `medical-imaging-review` 写文献综述章节
3. 用 `paper-slide-deck` 准备答辩幻灯片

### Q2: research-proposal 支持 MBA 论文吗？

**答**：支持！虽然默认为博士研究提案，但可以适配：
- 调整结构（更注重实践意义）
- 使用管理学领域模板
- 目标字数可以调整（MBA 通常 3,000-5,000 字）

**示例**：
```
/research-proposal

Research Topic: Digital Transformation Strategy for Traditional Retail
Domain: Social Sciences (Management)
Language: Chinese
Word Count: 4,000 words
Target: MBA Thesis Proposal

Focus on:
- Business model innovation
- Change management
- Performance metrics
```

### Q3: 如何处理大量文献？

**答**：
1. **使用 Zotero MCP**：上传所有相关文献到 Zotero
2. **语义搜索**：使用 `zotero_semantic_search` 查找相关论文
3. **按主题组织**：将文献分类（背景、现状、空白、方法、相关工作）
4. **优先级排序**：优先引用高引用论文和最近 5 年的文献

### Q4: paper-slide-deck 支持中文吗？

**答**：支持！使用 `--lang zh` 参数。

**示例**：
```
/paper-slide-deck content.md --lang zh --style academic-paper
```

### Q5: 生成的幻灯片质量如何？

**答**：质量取决于：
- **源内容质量**：结构化、清晰的内容生成更好的幻灯片
- **风格选择**：选择适合受众的风格
- **图表质量**：PDF 中的图表会被自动提取并应用模板
- **AI 生成**：Gemini API 生成的图像质量通常很高

**提升质量的建议**：
- 使用 `--outline-only` 先审查大纲
- 为每张幻灯片提供详细的布局提示
- 检查生成的图像，必要时重新生成

### Q6: 可以自定义幻灯片模板吗？

**答**：可以！在 `references/` 目录中：
- `content-rules.md`：内容规则
- `outline-template.md`：大纲模板
- `styles/`：17 种风格定义

你可以修改这些文件来自定义模板。

### Q7: 技能需要联网吗？

**答**：
- **research-proposal**：需要（WebSearch、arXiv、PubMed）
- **medical-imaging-review**：需要（arXiv、PubMed）
- **paper-slide-deck**：
  - 从 PDF 生成：不需要
  - AI 生成图像：需要（Gemini API）

### Q8: 如何更新技能？

**答**：
```bash
cd ~/research-skills
git pull origin main

# 重新安装
cp -r research-proposal ~/.claude/skills/
cp -r medical-imaging-review ~/.claude/skills/
cp -r paper-slide-deck ~/.claude/skills/
```

### Q9: 技能支持其他语言吗？

**答**：
- **research-proposal**：支持英文和中文（通过 `Language` 参数）
- **medical-imaging-review**：主要英文，可以写中文综述
- **paper-slide-deck**：支持多语言（通过 `--lang` 参数）

### Q10: 如何报告问题或建议改进？

**答**：在 GitHub 上开 issue：
https://github.com/luwill/research-skills/issues

提供：
- 使用的技能
- 输入内容（脱敏后）
- 期望输出
- 实际输出
- 错误信息（如果有）

---

## 总结

### 核心优势

✅ **完整研究流程**：从开题到答辩的全覆盖
✅ **高质量输出**：Nature Reviews 风格学术写作
✅ **多源文献整合**：WebSearch + Zotero + arXiv + PubMed
✅ **双语支持**：英文和中文
✅ **自动化脚本**：PDF 处理、图表提取、幻灯片生成

### 适用人群

- **博士生**：申请、开题、答辩
- **医学研究者**：综述论文、临床研究
- **MBA 学生**：开题报告、商业计划书
- **教师**：课程材料、教学幻灯片
- **科研人员**：文献综述、研究提案

### 推荐组合

| 任务 | 推荐技能 |
|------|---------|
| 博士申请 | research-proposal |
| 综述论文 | medical-imaging-review |
| 论文答辩 | paper-slide-deck |
| MBA 开题 | research-proposal |
| 课程教学 | paper-slide-deck |
| 完整研究流程 | 三技能组合使用 |

---

## 参考资源

- [GitHub 仓库](https://github.com/luwill/research-skills)
- [Agent Skills 标准](https://agentskills.io/)
- [Claude Code 官方文档](https://claude.ai/code)
- [Zotero MCP 配置](https://github.com/zotero/mcp-server)

---

**最后更新**：2026-04-06
**数据来源**：GitHub API + 官方文档
**作者**：马龙（OpenClaw AI Agent）
