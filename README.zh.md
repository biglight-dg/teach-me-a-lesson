[English](README.md) | [한국어](README.ko.md) | [Español](README.es.md) | [Français](README.fr.md) | **中文** | [日本語](README.ja.md) | [Tiếng Việt](README.vi.md)

# teach-me-a-lesson — 面向 AI 与编程初学者的、耐心温和的老师 skill

一个 [Claude skill](https://docs.claude.com/en/docs/claude-code/skills)，它会**像一位好老师面对完全的新手和非开发者那样**，讲解 Claude、AI 工具以及编程/IT 概念，并在你工作时一直陪着你提供帮助。

它不只是直接抛出答案，而是专注于用一个好的比喻，创造那种**「哦，原来*是这样*！」**的瞬间。

## 它能做什么

它有六种模式（可以直接开口请求，也可以用斜杠命令触发）。

| 模式 | 命令 | 作用 |
|------|------|------|
| **explain** | `/tl-explain <主题>` | 用比喻、表格和要点讲解一个概念（默认） |
| **mistake** | `/tl-mistake` | 不带指责地诊断哪里出错、为什么出错，以及如何修复 |
| **bad-habit** | `/tl-bad-habit` | 找出反复出现的坏习惯并建议更好的做法 |
| **knowledge** | `/tl-knowledge <主题>` | 把你刚学到的内容保存为知识文件（markdown 笔记） |
| **token** | `/tl-token` | 观察你的使用方式，指出 token／上下文的浪费，并给出具体改进 |
| **config** | `/tl-config` | 设置老师的语言、语气正式度、语调/人设、表情符号数量，以及对你的称呼 |

skill 加载期间，它还会充当**随时在旁的帮手**：当它发现有风险的操作（粘贴来历不明的命令、暴露 API 密钥、不可逆的操作）、基于误解的请求或绕远路的低效做法时，会**温和地提醒**——不啰嗦——并把决定权留给你。

> 注意：这种随时提醒在 skill 加载期间（对话上下文内）有效。它不是一个会自动检查每一条输入的 hook。

### 触发示例

- 「用很简单的话讲讲 MCP 是什么——我是完全的新手」
- 「我总是分不清 API 和 SDK，用比喻讲讲区别」
- 「我有点怕终端——非用不可吗？」
- 「我好像刚把 .env 提交到 GitHub 了，这有什么问题？」 → mistake
- 「帮我指出我的坏习惯」 → bad-habit
- 「我感觉我在狂烧 token，能帮我看看吗？」 → token

## 安装

### 1）复制 skill 文件夹

```bash
# macOS / Linux
cp -r teach-me-a-lesson ~/.claude/skills/

# Windows (PowerShell)
Copy-Item -Recurse teach-me-a-lesson $env:USERPROFILE\.claude\skills\
```

### 2）安装斜杠命令（可选，用于使用 /tl-*）

把 skill 中 `commands/` 文件夹里的文件复制到你的命令文件夹。

```bash
# macOS / Linux
cp teach-me-a-lesson/commands/tl-*.md ~/.claude/commands/

# Windows (PowerShell)
Copy-Item teach-me-a-lesson\commands\tl-*.md $env:USERPROFILE\.claude\commands\
```

即使不用命令，像「简单讲讲这个」这样的话也会自动触发 skill。命令只是显式调用某个特定模式的便捷方式。

## （可选）连接你自己的知识文件

如果你有**知识文件**（一个装着 markdown 笔记的文件夹），skill 会优先把它们作为依据。如果没有，它会退而使用 Claude 自身的知识——所以**即使没有任何知识文件也能正常工作**。

- 默认的查找/保存文件夹：工作目录下的 `./knowledge/`，或 `~/.claude/teach-me-a-lesson/knowledge/`
- 如果你已经有一个笔记文件夹，直接指向它即可。
- 详细规则和可选的索引格式，见 `references/knowledge-files.md`。

> 本仓库**不**包含任何个人知识文档。公开的只有教学方法本身（即 skill）。

## 设置语气与语言

你可以按自己的喜好调整老师的**语言、正式度和风格**。例如在韩语中，它不仅能调整敬语/非敬语（존댓말/반말），还能调整**氛围**（温暖、平实、活泼、严谨）。

- `/tl-config` — 依次询问：语言 → 正式度 → 语调/人设 → 表情符号数量 → 对你的称呼，然后保存
- 自然语言也可以——「随意点、热情点」「用英语解释」「少用点表情符号」
- 设置保存在 `~/.claude/teach-me-a-lesson/config.json`（个人语气文件，因此**不**随发行版一起发布）。没有设置时，按**默认值（温暖的老师、礼貌的韩语 해요체）**运行。
- 无论何种语气，教学质量（比喻、不指责、不超载、注明出处）始终不变。详见 `references/tone-config.md`。

## 结构

```
teach-me-a-lesson/
├── SKILL.md                      # 触发条件 + 6 种模式 + 随时帮助 + 语气配置 + 工作流
├── references/
│   ├── teaching-style.md         # 如何构建比喻、好/坏示例、温和纠正
│   ├── knowledge-files.md        # 知识文件查找/保存规则（通用）
│   ├── modes.md                  # 6 种模式详解 + 随时帮助示例
│   └── tone-config.md            # 语言/正式度/语气/表情/称呼的结构与人设
├── commands/                     # /tl-* 斜杠命令（复制到你的命令文件夹）
├── evals/
│   └── evals.json
├── README.md                     # 英语（默认）
├── README.{ko,es,fr,zh,ja,vi}.md # 翻译版（韩/西/法/中/日/越）
└── LICENSE
```

## 许可证

MIT 许可证。可自由使用、修改和再分发。
