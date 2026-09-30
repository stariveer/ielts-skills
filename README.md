# IELTS Skills · 雅思备考 AI 私教系统（本地持久化 + 全科实战技能矩阵）

> 一套面向现代 AI Coding Agent（Claude Code、Antigravity、Cursor、Windsurf 等）的通用雅思备考私教系统。  
> **架构升级：融合「本地跨会话持久化记忆底座」与「源自真实备考演练的 18 个实战技能矩阵」，既有长周期的战报与资产沉淀，又有极速轻量的单项提分利器。**

---

## 核心特性

- **双轨架构设计 (Stateful + Stateless)**：核心中枢负责长周期记忆与资产沉淀，14 个专项实战技能开箱即用、即用即走，兼顾系统性与敏捷性；
- **跨会话持久化记忆**：所有目标、分数、练习历史全量保存在项目本地 `data/` 目录中，告别“每次对话独立”；
- **全科实战深度教练**：
  - **听力**：S1/S2 生活场景与干扰剖析 + S3/S4 极性降维法与长选项匹配；
  - **阅读**：P1-P3 梯度策略复盘 + 考点长难句“剔骨法”主干修饰层拆解；
  - **写作**：考官级四维评分 + 句子级诊断与改写对比 + 自动全文落盘归档；
  - **口语**：当季题库去噪沉淀 + 5 大万能故事高覆盖映射与 Part 3 预测；
- **专业 Anki 闪卡工坊**：针对词表、对话干货及听力 S2/S3/S4 场景提供专精制卡技能，严格输出**单行无空行**格式，一键导入 Anki/Mochi；
- **备考生产力工具**：一键清洗网页真题格式杂质（`ielts-exam-cleaner`）、辅导对话自动提炼结构化笔记（`ielts-note-summarizer`）；
- **轻量透明，零全局污染**：纯 Markdown + Git 管理，无需启动复杂外部服务与数据库。

---

## 目录结构

```text
ielts-skills/
├── skills/                            # 18 个核心技能插件目录
│   ├── ielts/                         # 【中枢】主教练入口（档案初始化、倒计时、战报复盘、智能路由）
│   ├── ielts-writing/                 # 【写作】写作教练（四维评分、改写对比、自动落盘归档）
│   ├── ielts-reading/                 # 【阅读】阅读精读（逻辑拆解、同义替换提取、自动沉淀）
│   ├── ielts-speaking/                # 【口语】口语素材（5大万能故事、Part 3 预测、内置当季真题题库）
│   │   └── resources/                 # 内置当季最新雅思口语题库
│   │
│   ├── ielts-l1-l2-coach/             # 【听力】S1/S2 预判与生活场景干扰复盘
│   ├── ielts-l3-l4-coach/             # 【听力】S3/S4 极性降维与长选项匹配复盘
│   │
│   ├── ielts-reading-coach/           # 【阅读】Passage 1-3 梯度策略复盘教练
│   ├── ielts-sentence-coach/          # 【阅读】考点长难句“剔骨法”分层拆解教练
│   │
│   ├── ielts-expression-coach/        # 【词汇】雅思核心考点与重难点表达精讲
│   ├── ielts-vocab-synonym-extractor/    # 【词汇】真题核心词汇与同义替换考点提取
│   ├── ielts-qa-expert/               # 【答疑】雅思专项答疑专家
│   │
│   ├── ielts-anki-maker/              # 【Anki】词汇列表 -> 3-5星级 Anki 卡片
│   ├── ielts-conv-anki-maker/         # 【Anki】辅导对话历史 -> 检索式防透题卡片
│   ├── ielts-l2-anki-maker/           # 【Anki】听力 Part 2 选项压缩与预判卡片
│   ├── ielts-l3-anki-maker/           # 【Anki】听力 Part 3 学术交互与长难选项卡片
│   ├── ielts-l4-anki-maker/           # 【Anki】听力 Part 4 独白路标与同义替换卡片
│   │
│   ├── ielts-exam-cleaner/            # 【工具】网页复制真题文本去噪与格式清洗
│   ├── ielts-note-summarizer/         # 【工具】辅导对话核心知识点与备考笔记总结
│   └── STANDARDS.md                   # 【规范】输出格式基准与 Anki 单行制卡纯净度规范
├── data/                              # 本地持久化备考资产目录（绝对私有）
│   ├── profile.md                     # 考生档案（目标分、考期、基线）
│   ├── progress.md                    # 进度看板与历史训练流水账
│   ├── mistakes.md                    # 薄弱点与逻辑错题本
│   ├── paraphrases.md                 # 高频同义替换库
│   ├── mock-score.md                  # 剑桥真题模考成绩单
│   ├── writing/                       # 历次写作批改报告全文归档
│   ├── speaking/                      # 口语万能故事与当季题库
│   ├── anki/                          # 导出的单行无空行 Anki CSV/TXT 制卡文件
│   └── ielts-mock-tests/              # 清洗后的真题与模考练习草稿
├── .agents/                           # 预置 Antigravity 工作区开箱即用配置 (skills -> ../skills)
├── .claude/                           # 预置 Claude Code 工作区开箱即用配置 (skills -> ../skills)
├── AGENTS.md                          # AI 协作共识与架构开发准则
├── README.md                          # 安装指引与使用文档
└── LICENSE                            # MIT License
```

> **💡 关于数据持久化目录 `data/`（代码与状态彻底解耦）：**  
> 本技能包采用**「纯技能插件包（Plugin Bundle）」**架构，开源发布时仓库内**零内置个人数据**。  
> 当你将技能安装至本地后，只需在**你的任意个人备考工作区**启动唤醒 `/ielts`，系统将自动在你当前工作区内初始化并维护专属的 `data/` 持久化资产目录。

---

## 18 个 Skill 完整矩阵与分工

本系统将技能划分为**「核心持久化体系」**与**「即时专项实战工具集」**两大层级：

### 一、 核心持久化体系 (Stateful Core System - 4 个)

深度联动 `data/` 目录，负责考期长效追踪、档案维护与资产落盘：

| Skill | 触发方式 | 核心功能 | 本地数据持久化动作 |
|---|---|---|---|
| **主教练** (`ielts`) | `/ielts`、「查看进度」「备考复盘」 | 档案初始化、考期倒计时、备考复盘看板、智能路由 | 读取并维护 `data/profile.md` 与 `data/progress.md` |
| **写作教练** (`ielts-writing`) | `/ielts-writing`、「批改作文」 | 四维评分 (TR/CC/LR/GRA)、逐句精修、高分重构对比 | 报告归档至 `data/writing/`，流水写入 `progress.md`，替换词入 `paraphrases.md`，短板入 `mistakes.md` |
| **阅读教练** (`ielts-reading`) | `/ielts-reading`、「分析阅读」 | T/F/NG 逻辑拆解、Heading 排除、同义替换提取 | 提取词汇合并入 `data/paraphrases.md`，错因记录入 `data/mistakes.md` |
| **口语素材** (`ielts-speaking`) | `/ielts-speaking`、「口语素材」 | 当季题库更新、话题聚类、5 大万能故事、Part 3 预测 | 万能故事与题库归档至 `data/speaking/`，流水追加至 `progress.md` |

---

### 二、 即时专项实战工具集 (Stateless Specialist Toolkit - 14 个)

> **💡 为什么这些技能保持“无状态（即用即走）”？**  
> 这 14 个技能直接移植自日常在大模型网页端（如 Gemini Web）经过高频真题演练打磨出的实用 Prompts。它们专注于特定单项的高质输出（如选项降维、剔骨拆解、单行制卡、真题清洗等）。**保持无状态能够实现零配置依赖、即用即走、不污染全局进度看板**；产出成果用户可在对话中即时消化，亦可按需复制或保存至 `data/anki/`、`data/ielts-mock-tests/` 等专属目录。

#### 1. 听力专项复盘教练
| Skill | 触发场景 | 核心提分机制 |
|---|---|---|
| **S1/S2 预判教练** (`ielts-l1-l2-coach`) | 提供 S1/S2 题目、原文及复盘笔记 | 专攻生活场景独白/对话。指导词性场景预判、方位追踪，剖析拼写陷阱与“自我纠正”干扰。 |
| **S3/S4 降维教练** (`ielts-l3-l4-coach`) | 提供 S3/S4 题目、原文及复盘笔记 | 专攻学术研讨与学术讲座。运用“极性降维法”和“认知负荷管理”，指导长选项压缩与路标词前置追踪。 |

#### 2. 阅读与长难句教练
| Skill | 触发场景 | 核心提分机制 |
|---|---|---|
| **阅读复盘教练** (`ielts-reading-coach`) | 提供阅读篇章、题目作答与原文 | 针对 Passage 1 到 Passage 3 的难度梯度，提供动态定位词抓取、逐题同义替换剖析与考场做题策略。 |
| **长难句教练** (`ielts-sentence-coach`) | 提供阅读真题篇章或难句 | 独创“剔骨法”——将复杂句分层剥离为主干与修饰层，锁定真正影响题目的核心考点句。 |

#### 3. 考点表达与答疑
| Skill | 触发场景 | 核心提分机制 |
|---|---|---|
| **考点精讲** (`ielts-expression-coach`) | 提供词汇、短语、搭配或错题 | 7.0+ 目标导向，一针见血精讲雅思考法、同义替换与避坑指南。 |
| **同义替换提取** (`ielts-vocab-synonym-extractor`) | 提供题干、选项与听读原文 | 精准抓取题干与原文的映射关系，结构化提炼高频同义替换考点对。 |
| **答疑专家** (`ielts-qa-expert`) | 针对雅思词汇、语法或错题发问 | 专业、精准且平易近人，聚焦具体疑问加深印象，不层层加码或过度发散。 |

#### 4. Anki 记忆卡片生成工坊（严格单行无空行）
| Skill | 触发场景 | 制卡特色（均适配 Anki/Mochi 一键导入） |
|---|---|---|
| **词表 Anki** (`ielts-anki-maker`) | 提供生词/词伙列表 | 3-5 星级考点评级、语境填空构建与速记卡片。 |
| **对话 Anki** (`ielts-conv-anki-maker`) | 要求根据刚才的辅导对话制卡 | 基于“检索式提取”与“防透题原则”，将对话知识点提炼为记忆卡。 |
| **听力 P2 Anki** (`ielts-l2-anki-maker`) | 提供听力 Part 2 复盘材料 | 专项训练 3-5 秒快读题、选项压缩与陷阱定位肌肉记忆。 |
| **听力 P3 Anki** (`ielts-l3-anki-maker`) | 提供听力 Part 3 复盘材料 | 专攻长难选项降维、观点匹配与学术交互逻辑提炼。 |
| **听力 P4 Anki** (`ielts-l4-anki-maker`) | 提供听力 Part 4 复盘材料 | 强化前置路标词识别、同义替换秒反应，攻克一气呵成掉队痛点。 |

#### 5. 格式清洗与总结工具
| Skill | 触发场景 | 核心价值 |
|---|---|---|
| **试卷清洗** (`ielts-exam-cleaner`) | 粘贴网页复制的真题杂乱文本 | 过滤广告、解析弹窗、多余按钮（如“收藏本题”），转化为标准 Markdown 真题。 |
| **对话总结** (`ielts-note-summarizer`) | 要求整理复盘对话笔记 | 提炼对话中的核心词伙、同义替换、错题逻辑与避坑纪律，生成系统笔记。 |

---

## 典型实战协作工作流

### 工作流 1：听力真题“清洗 -> 极性降维复盘 -> Anki 制卡”闭环
```text
1. 【清洗真题】从练习网站复制杂乱题面 -> 使用 `ielts-exam-cleaner` 一键输出规范 Markdown 真题；
2. 【错题复盘】做完 S3/S4 后将题目与原文发给 `ielts-l3-l4-coach` -> 获得选项极性降维分析与干扰陷阱拆解；
3. 【制卡沉淀】输入「根据刚才的复盘材料生成 Anki 卡片」-> 唤起 `ielts-l3-anki-maker` 生成严格单行卡片；
4. 【导入复习】将单行卡片追加保存至 `data/anki/merged_listening_*.csv` 并导入 Anki 强化刷卡。
```

### 工作流 2：阅读错题“精读诊断 -> 长难句剔骨拆解”
```text
1. 【错题分析】向 `/ielts-reading` 或 `ielts-reading-coach` 提交错题段落与题目 -> 拆解 T/F/NG 判定链；
2. 【剔骨长难句】遇到卡壳长难句，调用 `ielts-sentence-coach` -> 分离主干与修饰层，锁定破题关键点；
3. 【词汇自动落盘】核心替换词自动沉淀至 `data/paraphrases.md`，逻辑陷阱追加进 `data/mistakes.md`。
```

### 工作流 3：作文批改与资产沉淀
```text
1. 【提交批改】在对话中输入 `/ielts-writing [粘贴题目与作文]`；
2. 【考官点评】获得四维评分、逐句诊断与目标分重构版本；
3. 【自动落盘】报告全文落盘至 `data/writing/YYYY-MM-DD-*.md`，均分流水追加至 `data/progress.md`。
```

### 工作流 4：答疑探讨与对话干货归纳
```text
1. 【即时解惑】向 `ielts-qa-expert` 提问生词辨析或审题疑问；
2. 【笔记总结】交互完成后唤起 `ielts-note-summarizer` 提炼结构化笔记；
3. 【对话制卡】调用 `ielts-conv-anki-maker` 将本次会话的核心考点直接转成 Anki 卡片。
```

---

## 快速开始（工作区开箱即用）

本项目专为**个人雅思独立备考工作区**设计，核心原则是**数据留在当前工作区，不污染系统全局环境**。仓库已内置各主流智能体的工作区自动发现配置，**Clone 本仓库后即可直接就地使用，无需任何安装配置**：

### 1. 克隆仓库并作为你的专属备考目录
```bash
git clone https://github.com/stariveer/ielts-skills.git my-ielts-study
cd my-ielts-study
```

### 2. 唤醒私教系统
- **Google Antigravity 用户**：直接在 IDE 聊天窗口中输入 `/ielts`（仓库已内置 `.agents/` 工作区配置，原生秒级唤起）；
- **Claude Code 用户**：在终端启动 `claude` 并输入 `/ielts`（仓库已内置 `.claude/` 工作区配置，就地秒级唤起）；
- **Cursor / Windsurf / Aider 用户**：在对话中通过 `@skills/ielts/SKILL.md` 直接调用；
- **GitHub Copilot / OpenAI 用户**：在 `.github/copilot-instructions.md` 中引用 `skills/` 即可。

> **💡 关于个人数据（data/）**：  
> 首次唤醒 `/ielts` 后，系统会自动在当前工作区内初始化并维护属于你的私有 `data/` 目录（包含档案 `profile.md`、进度 `progress.md`、错题 `mistakes.md`、同义替换库 `paraphrases.md` 等），所有个人练习数据与隐私完全留存在当前工作区，不外泄、不全局污染。

---

## License

[MIT](./LICENSE)

随便用、随便改、随便商用。注明出处不强制但欢迎。

---

## 反馈与致谢

- 欢迎提交 [Issue](https://github.com/stariveer/ielts-skills/issues) 或 Pull Request。
- 本项目灵感与初始结构衍生自 [YANZHANLIN/ielts-claude-skills](https://github.com/YANZHANLIN/ielts-claude-skills)，在其基础上重构升级为**本地持久化记忆中枢 + 18 个全科实战技能矩阵**的完整备考系统。
