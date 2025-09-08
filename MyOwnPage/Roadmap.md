# 个人知识与任务管理系统框架 (PKM & Task Management Framework)

本框架旨在整合学术研究、项目管理、个人成长和日常记录，构建一个高效、可追溯、可输出的个人管理系统。

## 1. 学术研究中心 (Academic Research Hub)

目标：高效管理文献，并实时追踪学科前沿动态。

### 1.1. 文献知识库 (Literature Knowledge Base)

用于系统性地整理和消化所阅读的文献。

**结构/属性:**

*   **论文标题 (Title):** `[Text]`
*   **作者 (Authors):** `[Text]`
*   **年份 (Year):** `[Number]`
*   **期刊/会议 (Journal/Conference):** `[Text]`
*   **研究领域 (Field):** `[Tag]` (e.g., `LLM`, `Econometrics`, `Causal Inference`)
*   **标签 (Tags):** `[Multi-select]` (e.g., `Methodology`, `Survey`, `SOTA`, `Key-Reference`)
*   **阅读状态 (Status):** `[Select]` (e.g., `待读 (To Read)`, `在读 (Reading)`, `已读 (Finished)`, `精读 (Deep-Dive)`)
*   **PDF 附件 (File):** `[File]`
*   **引用链接 (URL):** `[URL]`
*   **关联项目 (Related Project):** `[Relation]` (关联到 `2. 任务与项目管理`中的项目)

**核心内容 (模板):**

```markdown
### 摘要 (Abstract)
> [粘贴或转述论文摘要]

### 核心贡献 (Core Contribution)
- **解决了什么问题：**
- **提出了什么方法/观点：**
- **主要结论是什么：**

### 方法论 (Methodology)
- **数据/环境：**
- **关键技术/模型：**
- **实验设计/论证过程：**

### 我的思考与启发 (My Thoughts & Inspirations)
- **这篇文章的优点和局限性？**
- **对我当前的研究有何借鉴意义？**
- **未来可以 follow 的工作方向？**
```

### 1.2. 前沿动态追踪 (Cutting-Edge Tracker)

用于快速捕获和筛选最新的工作论文（Working Papers）。

**工作流:**

1.  **订阅源 (Sources):**
    *   **arXiv:** 订阅关键领域的邮件提醒 (e.g., `cs.AI`, `cs.CL`, `econ.EM`)。
    *   **Google Scholar Alerts:** 设置关键词（如特定学者、理论、技术）的提醒。
    *   **SSRN / NBER:** 针对经济学、社会科学领域。
    *   **专业社区/博客:** `Hugging Face`, `Papers with Code`, ` distill.pub` 等。
2.  **聚合与筛选 (Aggregation & Filtering):**
    *   使用 RSS 阅读器 (如 Feedly, Inoreader) 聚合所有信息源。
    *   每天/每周固定时间快速浏览标题和摘要。
3.  **处理 (Action):**
    *   **丢弃 (Discard):** 不相关或不感兴趣的。
    *   **存档 (Archive):** 觉得可能有用但非急需的，添加标签后存入文献库，状态为 `待读`。
    *   **立即处理 (Process):** 高度相关的，立即下载并存入文献库，状态设为 `在读`，并关联到具体任务。

## 2. 任务与项目管理 (Task & Project Management)

目标：清晰地追踪不同助研（RA）工作和其他任务的进度、约束和下一步计划。

### 2.1. 项目看板 (Project Kanban Board)

宏观视角管理所有并行的项目。

**看板列:**
*   **构思中 (Ideas):** `[Project Card]`
*   **进行中 (In Progress):** `[Project Card]`
*   **已完成 (Completed):** `[Project Card]`
*   **搁置/等待 (On Hold/Waiting):** `[Project Card]`

**项目卡片属性 (Project Card Properties):**

*   **项目名称 (Project Name):** `[Text]` (e.g., `导师A-项目X`)
*   **负责人/导师 (Supervisor):** `[Tag]`
*   **截止日期 (Deadline):** `[Date]`
*   **优先级 (Priority):** `[Select]` (e.g., `High`, `Medium`, `Low`)
*   **当前状态概述 (Status Summary):** `[Text]` (一句话描述当前进展)

### 2.2. 任务清单与日志 (Task List & Log)

微观视角管理每个项目的具体任务和日常进展。

**结构/属性:**

*   **任务名称 (Task Name):** `[Text]`
*   **所属项目 (Project):** `[Relation]` (关联到 `2.1. 项目看板`)
*   **DDL:** `[Date]`
*   **状态 (Status):** `[Checkbox or Select]` (e.g., `To-Do`, `Doing`, `Done`, `Blocked`)
*   **进展日志 (Progress Log):** `[Text Block]` (核心部分)

**进展日志格式 (Progress Log Format):**

```markdown
---
**YYYY-MM-DD**
- **已完成:** [具体完成的事项，如：完成了数据清洗的前半部分]
- **遇到的约束:** [遇到的困难或阻碍，如：API 访问受限，需要等待授权]
- **下一步计划:** [明确的、可执行的下一步，如：明天上午9点前，邮件联系管理员申请权限]
---
```

## 3. 个人成长引擎 (Personal Growth Engine)

目标：系统性地提升写作、技术和知识广度。

### 3.1. 写作样本库 (Writing Portfolio)

**结构/属性:**

*   **标题 (Title):** `[Text]`
*   **类型 (Type):** `[Tag]` (e.g., `课程论文`, `摘要`, `研究计划`, `博客文章`)
*   **版本号 (Version):** `[Number]`
*   **状态 (Status):** `[Select]` (e.g., `草稿`, `待修改`, `已完成`, `已发表`)
*   **反馈记录 (Feedback Log):** `[Text Block]` (记录导师、同行的关键修改意见)

### 3.2. 技术精进模块 (Tech Enhancement Module)

#### 3.2.1. AI 动向观察哨 (AI Trends Watchlist)

*   **来源:** 复用 `1.2. 前沿动态追踪` 的信息流。
*   **形式:** 一个专门的页面或数据库，记录对个人有启发的关键技术、模型或开源项目。
*   **记录项:** `技术/模型名称`, `核心思想`, `潜在应用`, `相关链接`。

#### 3.2.2. 编程风格与代码库 (Coding Style & Snippet Library)

*   **个人代码风格指南 (Personal Style Guide):** 一个 `style_guide.md` 文件，记录自己的编码规范（变量命名、函数设计、注释风格、项目结构等）。在实践中不断完善。
*   **代码片段库 (Code Snippet Library):** 按语言或功能分类，存储可复用的代码块。
*   **项目复盘 (Project Post-mortems):** 完成一个编程项目后，进行复盘，记录 `做得好的地方`, `可以改进的地方`, `学到的新技能`。

### 3.3. 泛读记录 (Extracurricular Reading Log)

**结构/属性:**

*   **书名/文章名 (Title):** `[Text]`
*   **作者 (Author):** `[Text]`
*   **类型 (Genre):** `[Tag]` (e.g., `历史`, `科幻`, `传记`, `科普`)
*   **状态 (Status):** `[Select]` (e.g., `想读`, `在读`, `已读`)
*   **评分 (Rating):** `[Stars, 1-5]`
*   **素材库 (Material for Reviews):**
    *   **金句摘录 (Key Quotes):** `[Text Block]`
    *   **核心观点 (Core Ideas):** `[Bulleted List]`
    *   **个人感悟/读后感草稿 (Reflections/Draft):** `[Text Block]`

### 3.4. 结构化学习追踪 (Structured Learning Tracker)

**结构/属性:**

*   **课程/学习资料 (Course/Material):** `[Text]`
*   **来源 (Source):** `[URL/Text]` (e.g., `Coursera`, `fast.ai`, `经典教材`)
*   **领域 (Field):** `[Tag]`
*   **学习进度 (Progress):** `[Percent or Text]` (e.g., `75%` or `Chapter 5/12`)
*   **笔记链接 (Link to Notes):** `[Internal Link]`
*   **产出物 (Deliverable):** `[Text]` (e.g., `完成的项目`, `撰写的博客`, `GitHub Repo`)

## 4. 日常记录与输出 (Daily Logging & Output)

目标：建立日常工作的可追溯性，并为个人主页提供内容。

### 4.1. 个人 Commit Log (Personal Commit Log)

模仿 GitHub 提交记录，以极简形式记录每日有效投入。

**格式 (在一个`log.md`文件或专用页面中):**

```
### 2023-10-27
- **[ACADEMIC]** 精读了 "Attention Is All You Need" 并完成笔记。
- **[PROJECT]** 为 RA 项目 X 修复了数据预处理脚本中的一个 bug。
- **[GROWTH]** 学习了 `fast.ai` 课程的第 4 讲，并完成了练习。
- **[WRITING]** 起草了个人主页中 "About Me" 页面的初稿。
```

### 4.2. 个人主页内容池 (Personal Homepage Content Pool)

这是一个“发布”中心，所有面向公众展示的内容都从这里筛选和润色。

**工作流:**

1.  在 `2.1`、`3.1`、`3.4` 等模块中，增加一个 `[Checkbox]` 属性，名为 **“发布至主页 (Publish to Homepage)”**。
2.  创建一个看板或页面，筛选出所有勾选了“发布至主页”的项目。
3.  对这些筛选出的内容进行二次加工和润色，使其适合公开展示。
4.  最终将这些内容更新到你的个人主页。

---

**建议工具启动方案:**

*   **All-in-One 方案:** 使用 **Notion**。它可以完美地实现上述所有数据库、关联和模板功能。
*   **本地化 & Geek 方案:** 使用 **Obsidian** + 插件 (Dataview, Kanban)。文件以 Markdown 本地存储，方便用 Git 进行版本控制。
*   **混合方案:** **Zotero** (文献管理) + **Notion/Trello** (任务管理) + **Obsidian/VS Code** (笔记与代码)。

从一个模块开始，比如 `2. 任务与项目管理`，逐步搭建和完善，避免一开始就追求完美系统而难以启动。

