---
name: gen-image
description: AI 生图工具。需要生成/制作图片时使用——界面配图、网站 banner、图标、海报、占位图、任何视觉素材。说"生成一张图"、"做个图"、"生图"或 /gen-image 时触发。支持 seedream-image-v5.0-pro（写实/质感强）与 gpt-image-2（指令遵循好/图标风）两个模型。
---

# 生图技能

## 调用方式（唯一入口）

```bash
python C:/Users/Lizhuo4/.claude/skills/gen-image/gen_image.py \
  --prompt "<英文提示词，效果显著优于中文>" \
  --model <seedream-image-v5.0-pro|gpt-image-2> \
  --size <宽x高，默认 1024x1024> \
  --name <文件名，不含扩展名> \
  --out <输出目录>
```

成功后最后一行输出 `FILE: <绝对路径>`。图是本地的 jpg/png。

## 模型怎么选

| 场景 | 模型 | 理由 |
|---|---|---|
| 图标、UI 素材、扁平/极简、需要严格按描述构图 | gpt-image-2 | 指令遵循好，指令式风格稳 |
| 写实照片、氛围图、材质质感、大场景 | seedream-image-v5.0-pro | 质感与真实感强 |

## 使用注意

- **prompt 用英文**，描述具体（主体 + 风格 + 背景 + 构图），避免歧义词
- 尺寸常用：1024x1024（方图/图标）、1280x720（横幅）、720x1280（竖幅）、2048x2048（大图）
- API key 在脚本内，属私密凭据——**技能文档和对话里都不要再贴 key**
- 每张图消耗额度（seedream ~60000 tokens/张），批量生成前先出 1 张确认方向再放量
- 界面用图注意版权口径：生成的图别带已有 IP 的角色/商标（游戏角色形象尤其注意）
- 失败排查：公司网络 TLS 拦截时 curl 已带 --ssl-no-revoke；若仍失败看脚本抛的 RuntimeError 信息（含响应前 300 字符）

## 给 zhoform 用的特殊口径

本项目界面/网站需要配图时（天煞·劫主题的 banner、卡片底纹、宣传图等）：

1. 先出 1 张让用户确认方向（用户偏好：深色暗底、品红主色调 #E0399B、避免 AI 插画风——见 qss-design-review 技能的反 AI 味铁律）
2. 确认后按需批量；产出图放 `client/assets/images/`（客户端）或服务器 `shop_static/`（网站）
3. 用 PIL 检查尺寸/格式后再入库，坏图不入
