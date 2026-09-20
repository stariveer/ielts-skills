# IELTS Skills · 雅思备考 AI 私教系统（本地持久化版）

> 一套面向现代 AI Coding Agent（Claude Code、Antigravity、Cursor、Windsurf 等）的通用雅思备考私教系统。
> **基于标准 Agent Skills 规范构建，支持本地跨会话记忆、数据持久化、自动做题归档、Mochi/Anki 卡片生成与真题联动，零多余依赖。**

---

## 核心特性

- **跨会话持久化记忆**：所有目标、分数、练习历史全量保存在项目本地 `data/` 目录中，告别“每次对话独立”；
- **智能开场与考期倒计时**：每次唤醒 `/ielts`，AI 自动读取考生档案，智能汇报剩余备考天数与阶段战况；
- **写作批改自动归档**：使用 `/ielts-writing` 批改后，报告自动全文落盘保存至 `data/writing/`，并将分数和评语追加进流水账；
- **阅读同义替换自动沉淀**：使用 `/ielts-reading` 分析错题后，提炼的替换词对自动合并至 `data/paraphrases.md`；
- **错题与陷阱本沉淀**：高频逻辑陷阱、审题硬伤自动追加至 `data/mistakes.md`；
- **Mochi / Anki 记忆卡片生成**：批改或练习后自动生成单行 Anki 卡片代码块并沉淀入 `data/cards.md`，支持无缝导入 Mochi 每日刷题；
- **口语万能故事库**：使用 `/ielts-speaking` 生成的 5 大万能故事沉淀在 `data/speaking/`；
- **真题刷题明细追踪**：与 `data/mock-score.md` 剑桥听力/阅读做题表无缝联动；
- **轻量透明**：纯 Markdown + Git 管理，无需启动任何复杂的本地 Web 服务，无需数据库与 Node/Python 后端依赖。

---

## 目录结构（技能包纯净形态）

```text
ielts-skills/
├── skills/                     # 核心技能插件目录
│   ├── ielts/                  # 主教练入口（档案初始化、倒计时、战报复盘、智能路由）
│   ├── ielts-writing/          # 写作教练（四维评分、改写对比、自动落盘归档、生成 Anki 卡片）
│   ├── ielts-reading/          # 阅读精读（逻辑拆解、同义替换提取、自动沉淀）
│   └── ielts-speaking/         # 口语素材（5大万能故事、Part 3 预测、内置当季真题题库）
│       └── resources/          # 内置当季最新雅思口语题库
├── .agents/                    # 预置 Antigravity 工作区开箱即用配置 (skills -> ../skills)
├── .claude/                    # 预置 Claude Code 工作区开箱即用配置 (skills -> ../skills)
├── README.md                   # 安装指引与使用文档
└── LICENSE                     # MIT License
```



> **💡 关于数据持久化目录 `data/`（代码与状态彻底解耦）：**  
> 本技能包采用**「纯技能插件包（Plugin Bundle）」**架构，仓库内**零内置个人数据**。  
> 当你将技能安装至本地后，只需在**你的任意个人备考工作区**启动唤醒 `/ielts`，系统将自动在你当前工作区内初始化并维护专属的 `data/` 持久化资产目录（包含档案 `profile.md`、进度 `progress.md`、错题 `mistakes.md`、Anki 卡库 `cards.md` 等）。


---

## 4 个 Skill 分工

| Skill | 命令 | 核心功能 | 本地数据持久化动作 |
|---|---|---|---|
| **主教练** | `/ielts` | 档案初始化、考期倒计时、备考复盘看板、智能路由 | 读取并维护 `data/profile.md` 与 `data/progress.md` |
| **写作教练** | `/ielts-writing` | 四维评分 (TR/CC/LR/GRA)、句子级修改、目标分改写对比 | 报告归档至 `data/writing/`，流水追加至 `progress.md`，替换词写入 `paraphrases.md`，Anki 卡片追加至 `cards.md` |
| **阅读教练** | `/ielts-reading` | T/F/NG 逻辑拆解、Heading 排除、同义替换提取 | 提取词汇合并入 `data/paraphrases.md`，错因记录入 `data/mistakes.md` |
| **口语素材** | `/ielts-speaking` | 题库更新、话题聚类、5 大万能故事覆盖 80% Part 2、Part 3 预测 | 万能故事归档至 `data/speaking/`，口语卡片追加至 `cards.md` |


---

## 使用场景

### 场景 1：日常启动与私教问候
```text
你：/ielts
AI：欢迎回来！距离你的雅思考试（2026-11-20）还有 63 天。
    当前目标：总分 7.0（听 7.5 / 读 7.5 / 写 6.0 / 说 6.0）。
    目前写作已批改 3 篇（均分 6.0），同义替换库累计 86 组。
    今天想练什么？
    A. 批改/练习写作  B. 阅读精读分析  C. 口语万能故事  D. 查看备考战报
```

### 场景 2：查看备考全量战报与复盘
```text
你：查看进度（或输入「我的战报」「备考复盘」）
AI：自动读取 data/ 目录中的各项数据，输出当前进度、写作分数走势、阅读薄弱题型与下一步战略建议。
```

### 场景 3：批改作文并自动归档
```text
你：/ielts-writing [粘贴题目与作文]
AI：
1. 给出官方四维评分与逐句批注；
2. 输出高分重构改写版；
3. 自动将报告落盘保存为 data/writing/2026-09-18_Task2_technology.md；
4. 自动在 data/progress.md 追加流水并更新均分；
5. 自动输出 Mochi / Anki 单行卡片并同步追加至 data/cards.md。
```

### 场景 4：分析阅读错题与词汇沉淀
```text
你：/ielts-reading [粘贴文章与错题，或说明剑桥真题编号]
AI：
1. 逐题逻辑拆解与推导链；
2. 提取同义替换词对；
3. 自动将同义替换合并至 data/paraphrases.md；
4. 易混逻辑陷阱追加至 data/mistakes.md。
```

### 场景 5：换题季动态更新口语题库
```text
你：/ielts-speaking 这是新季度的口语题库 [上传 PDF 或粘贴题目]
AI：
1. 自动过滤水印与广告噪点，提取结构化题目与提示卡（You should say...）；
2. 自动落盘保存为你本地工作区的 data/speaking/question_bank_YYYY_MM.md；
3. 立即基于新题库重新进行 5 大万能故事映射与覆盖率测算。
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
> 首次唤醒 `/ielts` 后，系统会自动在当前工作区内初始化并维护属于你的私有 `data/` 目录（包含档案 `profile.md`、进度 `progress.md`、错题 `mistakes.md`、Anki 题库 `cards.md` 等），所有个人练习数据与隐私完全留存在当前工作区，不外泄、不全局污染。


---

## License

[MIT](./LICENSE)

随便用、随便改、随便商用。注明出处不强制但欢迎。

---

## 反馈与致谢

- 欢迎提交 [Issue](https://github.com/stariveer/ielts-skills/issues) 或 Pull Request。
- 本项目灵感与初始结构衍生自 [YANZHANLIN/ielts-claude-skills](https://github.com/YANZHANLIN/ielts-claude-skills)，在其基础上重构升级为支持**本地持久化记忆、全量归档、Anki/Mochi 卡片生成与真题联动**的完整备考系统。
