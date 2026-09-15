# objective-eval

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
![Claude Code Skill](https://img.shields.io/badge/Claude%20Code-Skill-D97757)

> 一个让 AI 对任何人、事、物都**用同一把尺子**做评价的 Claude Code Skill。

评价类回答最容易出的问题不是"知道得太少"，而是**标准不一致**：对喜欢的东西宽容，对反感的东西苛刻；只列一方的缺点，不列另一方的；只算受益者，忘了受害者。这个 Skill 把"客观"拆成可执行的检查项，让模型每次评价都走同一套流程。

---

## 它解决什么问题

| 常见毛病 | 这个 Skill 的约束 |
|---------|------------------|
| 因为话题敏感就拒绝回答 | 用"**有没有事实依据**"判断能不能评，不用"敏不敏感"判断 |
| 对不同对象双重标准 | 强制标准一致性，发现双标立即修正 |
| 把能力和道德混为一谈 | 能力是事实，用能力做了什么才是道德判断，分开列 |
| 只分析直接受害者 | 逐层拆到间接受害者、后代、社会整体 |
| 只看短期效果 | 加入时间维度，分析短期获利者的长期代价 |
| 遗漏经济维度 | 优先检查财富转移、资产重分配、就业机会释放 |

## 安装

### 方式一：用户级（所有项目可用）

```bash
git clone https://github.com/DDykarc/objective-eval.git ~/.claude/skills/objective-eval
```

Windows PowerShell：

```powershell
git clone https://github.com/DDykarc/objective-eval.git "$env:USERPROFILE\.claude\skills\objective-eval"
```

### 方式二：项目级（仅当前项目）

```bash
git clone https://github.com/DDykarc/objective-eval.git .claude/skills/objective-eval
```

安装后在 Claude Code 中执行 `/skills` 应能看到 `objective-eval`。

## 使用

技能通过触发词自动激活，直接提问即可：

```
评价一下 Kubernetes 的优缺点
你怎么看微服务架构
远程办公的利弊是什么
客观评价一下某个历史人物
```

也可以显式调用：

```
/objective-eval 微信小程序云开发
```

### 支持的触发词

`客观评价` · `优缺点` · `公正评价` · `怎么看` · `评价一下` · `你怎么看` · `说说优缺点` · `的优点` · `的缺点` · `evaluate` · `pros and cons` · `strengths and weaknesses`

## 输出能力

Skill 内置 5 套评价模板，按提问方式自动选择：

| 模板 | 适用场景 |
|------|---------|
| A · 完整评价 | 优缺点都要 |
| B · 单方向评价 | 只要优点 / 只要缺点 |
| C · 具体方面评价 | 限定某一维度（如"只看成本"） |
| D · 群体对比评价 | 多对象横向对比，要求每项有依据 |
| E · 利益相关者全景分析 | 事件/制度类，拆解谁获利谁受害 |

其中模板 E 是核心，强制覆盖五个分析步骤：**确定范围 → 逐层分析受益者 → 逐层分析受害者 → 交叉分析 → 时间维度**，并单独检查经济流向。

## 设计原则

1. **标准一致性最关键** —— 发现双标就修正，不找借口
2. **区分事实与争议** —— 有据可查的直接陈述，有争议的标注立场
3. **不预判用户意图** —— 不因为话题敏感就揣测动机并拒答
4. **诚实面对不舒服的结论** —— 不用模糊语言包装
5. **用户指出问题时立即承认** —— 指出具体哪里不一致，给出修正版

## 结构

```
objective-eval/
└── SKILL.md    # 技能定义：原则、分析框架、5 套模板、自检清单、历史教训
```

## 说明

Skill 的"历史教训"一节记录的是开发过程中实际踩过的坑，用于避免同类偏差重复出现。这些条目针对的是**推理过程的偏差**，不代表任何特定立场的倾向性。

## 许可证

[MIT](LICENSE) © 2026 DDykarc
