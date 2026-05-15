# Claude Code 论文写作纪律 Skill 集

![License](https://img.shields.io/badge/License-MIT-blue.svg)
![Skills](https://img.shields.io/badge/Skills-12-orange.svg)
![For](https://img.shields.io/badge/For-Claude%20Code-7C3AED.svg)
![Language](https://img.shields.io/badge/Language-%E4%B8%AD%E6%96%87-red.svg)

12 个面向中文科研写作的 Claude Code Skill。把《Claude Code 科研手记》一书里的踩坑教训，固化成 AI 在动手前必须执行的检查点。

## 三个特点

- **可操作**：每条 Skill 都有强制流程图和标准回复模板，AI 不需要"理解"就能直接套用。
- **抗合理化**：每条 Skill 都配 Rationalization Table（"念头 vs 现实"对照），把 AI 在赶时间、累了、觉得这次不一样时会跳过流程的借口逐一封掉。
- **来自真实踩坑**：不是想象出来的最佳实践。每条 Skill 对应书里一段具体的翻车案例，标注了书的章节出处。

## 来源与定位

本 Skill 集从《Claude Code 科研手记》一书的 12 条核心纪律提炼而成。这套纪律针对中文科研场景下 Claude Code 工具使用中常见的踩坑——术语被同义替换、文件被覆盖、批量任务失控、模糊指令被自由发挥等——抽象为可在 AI 上下文中自动触发的检查点。

设计模式参考 Anthropic 社区的 superpowers 项目，但针对中文科研写作场景做了重写：触发词、举例、Rationalization Table 全部对应中国研究生与青年科研学者的工作习惯。

## 核心理念

科研写作翻车，不是因为不知道，是因为知道但累了、赶时间、觉得这次不一样而跳过。本系列把"踩过坑后才悟出来的动作"，变成 AI 在动手前必须先执行的检查点。

> 当你觉得"这次不用走流程也行"，那就是必须走流程的时候。

## Skill 清单

| Skill | 触发场景 | 防什么灾 |
| --- | --- | --- |
| `paper-using-skills` | 任何科研写作开场 | 入口与触发对照表 |
| `paper-claude-md-bootstrap` | 新论文项目第一次开会话 | AI 反复要你解释研究背景 |
| `paper-confirm-before-doing` | 「改一下 / 整理下 / 润色」等模糊任务 | AI 自由发挥跑偏 |
| `paper-one-session-one-task` | 一次会话提了多件事 | 上下文污染、决策劣化 |
| `paper-protect-terminology` | 跨多文件批改、术语统一 | 专业术语被同义替换 |
| `paper-backup-before-word` | 编辑 .docx / Word 文件 | XML 损坏、原文被覆盖 |
| `paper-pilot-before-batch` | 处理 ≥ 30 条目的批量任务 | 全量跑炸了改不回来 |
| `paper-parallel-audit` | 大批量引用 / 术语 / 格式核查 | 串行慢 + 中间挂了从头来 |
| `paper-translate-advisor-feedback` | 拿到导师录音、便条、口头反馈 | AI 听不懂学术口语 |
| `paper-logical-consistency` | 改动核心声明 / 研究问题 / 主要结论 | 改一处忘了改其他章节，论证穿帮 |
| `paper-verify-before-handoff` | 准备发给导师 / 提交 | AI 写得太流畅让人放松警惕 |
| `paper-writing-discipline` | 想加一条新规则到 skill | 按 4 个判断题筛选新坑 |

每个 Skill 都包含统一的六个栏目：核心理念、触发条件、强制流程、标准回复模板、Rationalization Table（封掉合理化借口）、Red Flags（自检停止信号）。

## 安装

Claude Code 默认从 `~/.claude/skills/` 加载 Skill。两种安装方式：

**软链接安装**（推荐，以后改一次同步两边）：

```bash
git clone https://github.com/ChenHaNing/paper-discipline-skills.git
cd paper-discipline-skills
ln -sf "$(pwd)/paper-"* ~/.claude/skills/
```

**复制安装**（不跟随 upstream 更新）：

```bash
git clone https://github.com/ChenHaNing/paper-discipline-skills.git
cp -r paper-discipline-skills/paper-* ~/.claude/skills/
```

安装完成后开新会话，12 个 Skill 会出现在 Claude Code 的系统提示里，按各自的 description 自动触发。

## 使用方式

不需要主动调用。AI 会按 Skill 的 description 自动判断何时触发。例如：

- 你说「帮我把第三章润色一下」 → `paper-confirm-before-doing` 触发，AI 先和你确认方案，再动手
- 你说「改一下 paper.docx」 → `paper-backup-before-word` 触发，AI 先 `cp` 备份再改
- 你说「改完了发我」 → `paper-verify-before-handoff` 触发，AI 跑 10 项硬清单后才宣告完成

如果某次没按预期触发，可以显式说「按 paper-confirm-before-doing 走一遍」或者用 `/<skill-name>` 强制调用。

## 使用示例

下面 3 个例子展示装与不装 Skill 时 AI 行为的差别。

### 示例 1：模糊润色任务

**用户输入**：「帮我把第三章润色一下。」

**触发的 Skill**：`paper-confirm-before-doing`

**AI 的行为变化**：

- 没装 Skill 时：直接调用 Edit 改 1500 字，结果作者特意保留的口语化表达被改没了，导师让保留的引文被改写。
- 装了 Skill 后：先回复「我准备按学术正式度统一术语、压缩冗余、保留段落结构。先改 §3.2.1 第一段给你看效果，确认后推全章——可以吗？」等用户点头才动手。

### 示例 2：编辑 Word 文件

**用户输入**：「改一下 paper.docx 的第二段。」

**触发的 Skill**：`paper-backup-before-word`

**AI 的行为变化**：

- 没装 Skill 时：直接 Edit 写回原文件，遇到 XML 损坏或误覆盖时无法回滚。
- 装了 Skill 后：先 `cp "paper.docx" "paper.bak.$(date +%Y%m%d-%H%M%S).docx"` 创建带时间戳的备份，改完提醒用户先打开 Word 验证完整性。

### 示例 3：交付前自查

**用户输入**：「改完了，发我吧。」

**触发的 Skill**：`paper-verify-before-handoff`

**AI 的行为变化**：

- 没装 Skill 时：回复「改完了，文件已保存」——后续可能被导师发现引用 [12] 不在参考文献里。
- 装了 Skill 后：跑 10 项硬清单（术语 / 引用 / 数据 / 图表 / 交叉引用 / 字数 / Todo 残留 / AIGC / 论证一致性 / 改动概要），列出每项的具体检查结果才宣告完成。

## 与原书的关系

|  | 本仓库 | 《Claude Code 科研手记》一书 |
| --- | --- | --- |
| 形式 | Markdown Skill 文件 | LaTeX 排版 PDF |
| 内容 | 12 条可执行纪律 | 15 章 + 5 附录，含背景、案例、实操 |
| License | 开源 | 闭源 |
| 适用 | 已经在用 Claude Code 想立刻装上纪律的人 | 想系统了解为什么这么做、怎么从零开始的人 |

Skill 装上后会在该触发的时候自动提醒你；书读完后你会知道为什么这些纪律值得。两者互补。

完整书稿（PDF 排版版本，含全部 15 章 + 附录）请见下方「关于作者」一节。

## 致谢

设计模式参考 Anthropic 社区的 superpowers 项目——Iron Law、Rationalization Table、Red Flags、RED-GREEN-REFACTOR for skills 等概念均来自该项目。本仓库把这些概念适配到了中文科研写作场景，并加入了从《Claude Code 科研手记》一书中提炼的具体踩坑案例。

## 安全声明

Skill 能让 AI agent 执行代码、修改文件、读写网络。本仓库的 12 个 Skill 是纯 Markdown 文件，不包含可执行代码——但它们会让 AI 主动调用 Edit / Write / Bash 等工具改你的文件。例如 `paper-backup-before-word` 会让 AI 在编辑 .docx 前自动跑 `cp` 命令；`paper-parallel-audit` 会让 AI 派多个子 Agent 同时跑核查。

安装前请自行阅读每个 SKILL.md，确认它要做的动作符合你的预期，不要不看就装。

如果你要修改或派生本仓库的 Skill 用到自己的项目里，请审查改动后再分发。如果发现任何 Skill 行为异常或与文档不符，欢迎在 [Issues](https://github.com/ChenHaNing/paper-discipline-skills/issues) 反馈。

## License

本 Skill 集采用 MIT License。书的内容（PDF / LaTeX 源码）保留所有权利。
