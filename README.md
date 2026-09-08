# claude-skills

个人 Claude Code 技能库。所有用户级技能统一放在这个仓库里，不再为单个技能开新仓库；技能积累到一定数量后，会把相关的整合成"专家"级技能。

## 技能清单

| 技能 | 触发方式 | 说明 |
|---|---|---|
| [refine-prompt](refine-prompt/SKILL.md) | `/refine-prompt`、"帮我完善提示词" | 先对齐请求类型，再按软件工程顺序多轮追问挖清需求，最后产出精炼的完整提示词 |
| [pm](pm/SKILL.md) | `/pm`、"我有个想法" | 需求梳理成文档，拆成多份任务派发到后台会话 |
| [handover](handover/skill.md) | `/handover`、"交接" | 上下文接近上限时写现状报告、更新记忆、生成交接提示词 |
| [skills](skills/SKILL.md) | `/skills`、"我有哪些技能" | 列出并管理所有已安装技能 |

## 使用方式

把本仓库克隆到 Claude Code 的用户级技能目录：

```bash
git clone https://github.com/bigzhuodan/claude-skills.git ~/.claude/skills
```

Windows 下路径为 `%USERPROFILE%\.claude\skills`。Claude Code 启动时会自动扫描该目录下每个子文件夹的 `SKILL.md`。

## 技能格式

每个技能一个文件夹，内含 `SKILL.md`，frontmatter 只有两个字段：

```yaml
---
name: kebab-case-name      # 只能小写字母、数字、连字符
description: 中文描述，写清什么话、什么场景下触发
---
```

正文是给 Claude 看的执行指令，用中文写。

## 相关仓库

- [claude-skill-qt-design](https://github.com/bigzhuodan/claude-skill-qt-design) — PySide6/QSS 界面视觉审查（项目级技能，单独维护）
