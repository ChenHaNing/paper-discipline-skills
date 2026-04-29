# Claude Code 论文写作纪律 Skill 集

11 个面向中文科研写作的 Claude Code Skill。把《Claude Code 科研手记》一书里的踩坑教训，固化成 AI 在动手前必须执行的检查点。

## 来源与定位

本 Skill 集从《Claude Code 科研手记》一书的 11 条核心纪律提炼而成。书是一名管理学硕士用 Claude Code 写论文的真实记录——27 个项目、1000+ 次会话、12 万条对话——其中反复出现的踩坑场景，被抽象为可在 AI 上下文中自动触发的纪律。

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

安装完成后开新会话，11 个 Skill 会出现在 Claude Code 的系统提示里，按各自的 description 自动触发。

## 使用方式

不需要主动调用。AI 会按 Skill 的 description 自动判断何时触发。例如：

- 你说「帮我把第三章润色一下」 → `paper-confirm-before-doing` 触发，AI 先和你确认方案，再动手
- 你说「改一下 论文.docx」 → `paper-backup-before-word` 触发，AI 先 `cp` 备份再改
- 你说「改完了发我」 → `paper-verify-before-handoff` 触发，AI 跑 9 项硬清单后才宣告完成

如果某次没按预期触发，可以显式说「按 paper-confirm-before-doing 走一遍」或者用 `/<skill-name>` 强制调用。

## 与原书的关系

|  | 本仓库 | 《Claude Code 科研手记》一书 |
| --- | --- | --- |
| 形式 | Markdown Skill 文件 | LaTeX 排版 PDF |
| 内容 | 11 条可执行纪律 | 15 章 + 5 附录，含背景、案例、实操 |
| License | 开源 | 闭源 |
| 适用 | 已经在用 Claude Code 想立刻装上纪律的人 | 想系统了解为什么这么做、怎么从零开始的人 |

Skill 装上后会在该触发的时候自动提醒你；书读完后你会知道为什么这些纪律值得。两者互补。

完整书稿（PDF 排版版本，含全部 15 章 + 附录）请见下方「关于作者」一节。

## 致谢

设计模式参考 Anthropic 社区的 superpowers 项目——Iron Law、Rationalization Table、Red Flags、RED-GREEN-REFACTOR for skills 等概念均来自该项目。本仓库把这些概念适配到了中文科研写作场景，并加入了从《Claude Code 科研手记》一书中提炼的具体踩坑案例。

## 关于作者

作者是一名管理学硕士，业余在小红书分享科研工具使用经验。

- 小红书：搜索 **chanw**——Claude Code 科研手记系列、科研自动化系列等。
- 书稿《Claude Code 科研手记》的 PDF 版本：小红书私信。

## 关于 AI 辅助科研写作的立场

AI 辅助科研写作的目的是帮你把已有的研究成果更高效地呈现出来，不是从零编论文。研究问题、实验数据、学术判断，这些必须是你自己的。本 Skill 集的所有纪律都建立在这一前提上——它们让 AI 协助你把活儿做干净，而不是替你做研究。

## License

本 Skill 集采用 MIT License。书的内容（PDF / LaTeX 源码）保留所有权利。
