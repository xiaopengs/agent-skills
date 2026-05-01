# AgentSkills

> OpenClaw 技能包——让 AI 真正能打的内容利器

精选高质量技能，帮助 AI 完成专业级内容生产任务。每个 skill 都可以独立安装、即插即用。

---

## 技能列表

### 🔥 wechat-explosive-analyzer

**公众号/视频号爆款内容六维审核分析器**

对公众号文章或视频号内容进行结构化审核，打分 + 诊断 + 可落地修改方案。

| 维度 | 权重 |
|------|------|
| 标题强度 | 30% |
| 开头钩子 | 20% |
| 选题切口 | 25% |
| 结构与节奏 | 15% |
| 社交货币 | 10% |
| 算法适配 | — |

**触发方式**：
- 提供公众号文章链接（`mp.weixin.qq.com`）
- 提供视频号链接（`weixin.qq.com/sph`）
- 直接粘贴文章草稿或视频脚本
- 要求对比两篇内容（已知爆款 vs 目标内容）

**输出**：爆款潜力判定 / 核心瓶颈 / 六维评分 / 可落地修改方案 / 选题替代方案

→ [查看详情](wechat-explosive-analyzer/)

---

## 安装方式

从本地安装 skill 文件：

```bash
clawhub install ./wechat-explosive-analyzer.skill
```

从 GitHub 安装：

```bash
clawhub install xiaopengs/agent-skills/wechat-explosive-analyzer
```

---

## 目录结构

```
agent-skills/
├── wechat-explosive-analyzer/
│   ├── SKILL.md                          # 技能定义 + 工作流
│   └── references/
│       └── content-review-standards.md   # 六维审核标准原文
└── README.md
```

---

## 持续更新

更多技能正在路上：
- 爆款标题批量生成器
- 选题热度追踪器
- 视频号脚本结构模板
- 小红书/微博爆款分析

欢迎 issue 提出需求或贡献 skill。
