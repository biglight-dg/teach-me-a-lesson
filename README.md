**English** | [한국어](README.ko.md) | [Español](README.es.md) | [Français](README.fr.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Tiếng Việt](README.vi.md)

# teach-me-a-lesson — a warm, patient teacher skill for AI & coding beginners

A [Claude skill](https://docs.claude.com/en/docs/claude-code/skills) that explains Claude, AI tools, and programming/IT concepts **the way a kind teacher would for total beginners and non-developers** — and keeps helping you alongside as you work.

Instead of just handing over the answer, it focuses on creating that **"oh, *that's* what it is!"** moment with a single good analogy.

## What it does

It works in six modes (trigger them by just asking, or with a slash command).

| Mode | Command | What it does |
|------|---------|--------------|
| **explain** | `/tl-explain <topic>` | Explain a concept with analogies, tables, and key takeaways (default) |
| **mistake** | `/tl-mistake` | Diagnose what went wrong and why — blame-free — and how to fix it |
| **bad-habit** | `/tl-bad-habit` | Spot recurring bad habits and suggest better ways |
| **knowledge** | `/tl-knowledge <topic>` | Save what you just learned as a knowledge file (markdown note) |
| **token** | `/tl-token` | Watch how you work and point out token/context waste, with concrete fixes |
| **config** | `/tl-config` | Set the teacher's language, formality, tone/persona, emoji level, and how it addresses you |

While the skill is loaded it also acts as an **ever-present helper**: when it sees risky actions (pasting unknown commands, exposing API keys, irreversible operations), requests built on a misconception, or an inefficient path, it **gently flags it** — no nagging — and leaves the decision to you.

> Note: the always-on helping works while the skill is loaded (within the conversation context). It is not a hook that auto-checks every single input.

### Trigger examples

- "Explain what MCP is, really simply — I'm a total beginner"
- "I keep mixing up API and SDK. Explain the difference with an analogy"
- "Terminals scare me — do I really have to use one?"
- "I think I just committed my .env to GitHub — what's the problem?" → mistake
- "Point out my bad habits" → bad-habit
- "I feel like I'm burning tokens — take a look?" → token

## Install

### 1) Copy the skill folder

```bash
# macOS / Linux
cp -r teach-me-a-lesson ~/.claude/skills/

# Windows (PowerShell)
Copy-Item -Recurse teach-me-a-lesson $env:USERPROFILE\.claude\skills\
```

### 2) Install the slash commands (optional, to use /tl-*)

Copy the files in the skill's `commands/` folder into your commands folder.

```bash
# macOS / Linux
cp teach-me-a-lesson/commands/tl-*.md ~/.claude/commands/

# Windows (PowerShell)
Copy-Item teach-me-a-lesson\commands\tl-*.md $env:USERPROFILE\.claude\commands\
```

The skill also triggers automatically from plain phrases like "explain this simply." Commands are just a handy way to call a specific mode explicitly.

## (Optional) Connect your own knowledge files

If you have **knowledge files** (a folder of markdown notes), the skill uses them as its primary source. If you don't, it falls back to Claude's own knowledge — so it **works fine with no knowledge files at all**.

- Default lookup/save folder: `./knowledge/` in your working directory, or `~/.claude/teach-me-a-lesson/knowledge/`
- If you already keep a notes folder, just point it there.
- For the detailed rules and the optional index format, see `references/knowledge-files.md`.

> This repository ships **no** personal knowledge documents. Only the teaching methodology (the skill itself) is published.

## Setting tone & language

You can tune the teacher's **language, formality, and vibe** to your taste. For Korean it adjusts not only 존댓말/반말 but also the **mood** (warm, plain, lively, crisp).

- `/tl-config` — asks in turn for language → formality → tone/persona → emoji level → how to address you, then saves it
- Natural language works too — "talk to me casually and upbeat," "explain in English," "ease up on the emoji"
- Settings are stored in `~/.claude/teach-me-a-lesson/config.json` (a personal tone file, so it is **not** shipped in the distribution). With no settings, it runs on the **defaults (warm teacher, polite Korean 해요체)**.
- Whatever the tone, the teaching quality (analogies, no blame, no overload, citing sources) stays the same. See `references/tone-config.md`.

## Structure

```
teach-me-a-lesson/
├── SKILL.md                      # Triggers + 6 modes + always-on helping + tone config + workflow
├── references/
│   ├── teaching-style.md         # How to build analogies, good/bad examples, gentle corrections
│   ├── knowledge-files.md        # Knowledge-file lookup/save rules (generic)
│   ├── modes.md                  # The 6 modes in detail + always-on helping examples
│   └── tone-config.md            # Schema & personas for language/formality/tone/emoji/address
├── commands/                     # /tl-* slash commands (copy into your commands folder)
├── evals/
│   └── evals.json
├── README.md                     # English (this file)
├── README.{ko,es,fr,zh,ja,vi}.md # Translations (KO/ES/FR/ZH/JA/VI)
└── LICENSE
```

## License

MIT License. Use, modify, and redistribute freely.
