# IELTS Skills 输出格式基准与纯净度规范 (STANDARDS.md)

> **适用范围**：本规范定义了本仓库内所有技能（Skills）、提示词（Prompts）以及 AI Agent 生成内容的输出格式基线。  
> 凡涉及生成 Markdown 代码块、解析文本，特别是生成可直接导入 Anki / Mochi 等记忆软件的闪卡，**必须无条件严格遵循本文档的标准**。

---

## 1. 全局最高优先级红线：Markdown 代码块纯净直出

> ⚠️ **红线说明**：此规则不仅限于 Anki 卡片生成，**只要提示词要求模型输出 Markdown 代码块（如 ` ```md ... ``` `）或代码片段，都必须遵循此规则。**

1. **绝对禁止引用与来源标记**：
   - 严禁在输出的任何地方（包括代码块内部、首尾、注释中）包含类似 `[source: x]`、`[cite: x]`、`[^1]`、`[1]` 等任何形式的检索来源引用标记、脚注脚标或网页链接标记。
2. **纯净文本直出 (Clean Plain Text ONLY)**：
   - 输出内容必须是没有任何脚标污染的纯净文本，防止在用户直接复制、自动化脚本解析或导入第三方工具（如 Anki、Mochi、Obsidian 等）时发生解析错乱、字段错位或格式报错。
3. **零废话直接输出 (Zero Fluff / Direct Output)**：
   - 模型在接收到素材后**无需任何前置寒暄、过渡句或后置说明**（严禁“好的，这是为您生成的卡片：”等说明语），直接以指定代码块格式输出核心内容。

---

## 2. Anki / Mochi 闪卡输出格式规范（公共基准）

凡是涉及生成可直接导入 Anki / Mochi 等间隔重复记忆工具的卡片，所有提示词与技能均统一遵循以下输出标准：

### 严格格式六要素

| 规范要素                    | 严格要求                                                                                   | 避坑警示                                                                                          |
| :-------------------------- | :----------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| **1. 统一代码块包裹**       | 必须且只能使用单个 Markdown 代码块（` ```md ... ``` `）包裹输出所有卡片。                  | 禁止代码块外夹杂任何问候语或解释文字。代码块第一行直接开始输出首张卡片。                          |
| **2. 单行格式与唯一分隔符** | 采用 `正面                                                                                 | 背面`的单行格式。竖线`                                                                            | ` 是正面和背面的**唯一分隔符**。整张卡片全行必须且只能有【恰好一个】未转义竖线。 | 正反面内部如需列举、并列或举例，**一律使用逗号 `,` 或斜杠 `/` 代替**，严禁出现多余的 ` | `（避免 Anki 报 `Invalid Record Length` 字段错位错误）。严禁在卡片中使用 Markdown 表格。 |
| **3. 行内严禁真实换行**     | 一张卡片必须且只能占用**绝对的一行**，严禁在同一张卡片内部使用真实回车换行（Enter/`\n`）。 | 背面所有排版换行与段落间距**必须统一使用 HTML 标签 `<br>` 或 `<br><br>`**。长文本必须单行拉到底。 |
| **4. 卡片间绝对零空行**     | 每一行必须是一张有效的卡片。**绝对禁止在卡片与卡片之间输出任何空白行（Empty lines）**。    | 上一张卡片末尾换行后，下一行必须紧贴着下一张卡片，严禁连敲两次回车（`\n\n`）。                    |
| **5. 填空符统一规范**       | 题干或搭配语境中的填空/挖空处，统一使用连续下划线 `___` 表示。                             | 统一采用 3 个下划线 `___`，保持辨识度一致。                                                       |
| **6. 英式拼写统一**         | 针对雅思考试环境，卡片英文部分优先使用英式拼写（British English spelling）。               | 如：`colour`, `centre`, `analyse`, `programme`。                                                  |

---

## 3. 标准卡片格式示例

### 示例 A：词汇/词伙卡片

```md
remedy |/ˈrem.ə.di/ n. 补救办法，纠正方法<br><br>【真题搭配】a remedy for \_\_\_ (解决...的良方)<br>【近义替换】solution / cure / antidote<br>【典型例句】There is no simple remedy for the global energy crisis.
take toll on |对...产生严重不良影响，造成重大损失<br><br>【核心考点】通常作动词词组：take a heavy toll on sth<br>【近义替换】cause severe damage to / have a negative impact on<br>【真题例句】Years of heavy smoking had taken its toll on his health.
```

### 示例 B：听力 Part 3/4 题目与长选项降维卡片

```md
[C16T4L4 · Q31] An experiment on university students suggested that dance increases **_ .|正确答案：creativity<br><br>【3–5秒审题压缩】increases _** → [positive abstraction/ability?]<br>【审题重点】increases 后的宾语；锁定定位词 experiment on university students<br>【原文定位】Sentence 15: "The result showed that those who chose to dance showed much more creativity when doing problem-solving tasks."<br>【关键替换】increases → showed much more<br>【干扰逻辑】录音前文提到了 sit, listen, cycle，只有 chose to dance 对应的是 much more creativity，注意排除前面的前置干扰。<br>【训练重点】听懂长句主干，抓住 "showed much more" 这个表示增加的高频同义替换。
[C16T4L4 · Q32] 1638 – The Dutch established a **_ on the island.|正确答案：colony / settlement<br><br>【3–5秒审题压缩】established a _** → [singular concrete/social noun]<br>【审题重点】时间路标 1638；主语 The Dutch；谓语 established<br>【原文定位】Sentence 7: "However, in 1638 the Dutch arrived and set up a colony there."<br>【关键替换】established → set up<br>【干扰逻辑】听到 1638 必须立刻警觉发令枪，set up 之后紧跟的词就是答案，切勿犹豫滞后。<br>【训练重点】速记动词短语同义替换：set up ↔ establish。
```

---

## 4. 常见反模式清单 (Anti-Patterns Checklist)

制卡与输出时，严格核对以下 5 项避坑禁忌：

- ❌ **反模式 1：包含来源标记**：句末附带 `[source: 1]` 或 `[^1]`（会导致导入 Anki 后正反面充斥垃圾字符）。
- ❌ **反模式 2：使用了多余的竖线**：如背面写了 `搭配A | 搭配B`（会导致 Anki 导入时将第二个 `|` 后的内容识别为第三列，破坏卡片字段映射）。
- ❌ **反模式 3：卡内使用了真实回车**：在背面写完一行按下 Enter 换行（会导致 Anki 将回车后的一截误当作一张全新的卡片，造成整张卡片崩塌）。
- ❌ **反模式 4：卡片与卡片之间留了空行**：输出中每张卡片中间隔了一个空行（会导致导入时产生大量空白无意义卡片）。
- ❌ **反模式 5：输出带前置废话**：输出 `好的，以下是为您生成的 5 张卡片：\n```md ...`（破坏自动化脚本复制与批量管道流）。
