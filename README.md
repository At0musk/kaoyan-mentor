# kaoyan-mentor · 考研规划导师

一个 [Agent Skill](https://agentskills.io)（兼容 Claude Code / ZCode / Codex 等任何 skills 兼容 runtime）：
**长期陪伴型考研规划导师** —— 不只是回答考研问题，而是运行一个完整闭环：

> 建立画像 → 研究招生事实 → 择校决策 → 制定可执行计划 → 执行与测评 → 数据复盘 → 动态调整 → 再规划

## 它做什么

- **考研画像与长期档案**：首次接触先收集画像（禁止大而空计划），用 `kaoyan-profile.md` 维护跨会话档案，每次周/月复盘、出分、择校变化后更新
- **择校研究与信息实时核验**：S/A/B/C 来源分级、关键事实双源交叉验证、数据强制标注【来源+年份】、区分计划招生/推免/统考名额、禁止伪精确（查不到就直说）
- **四科导师**：英语/数学/政治/专业课分别建体系——错题五类归因、真题反向驱动、掌握分级检验（不接受"看过了"当"学会了"）
- **规划与复盘循环**：任务八要素（时间+科目+内容+动作+数量+输出+标准+复盘）、周/月复盘、严重落后做减法（A/B/C 分类）而非盲目加时间、间隔复习 D0→D30
- **安全边界**：首次回复输出边界硬约束、画像齐备 STOP 门、换校/砍任务/阶段切换三处显性确认检查点、联网失败等 5 类异常降级路径

## 安装

```bash
# Claude Code
git clone https://github.com/At0musk/kaoyan-mentor.git ~/.claude/skills/kaoyan-mentor

# ZCode
git clone https://github.com/At0musk/kaoyan-mentor.git ~/.zcode/skills/kaoyan-mentor

# 其他 skills 兼容 runtime：克隆到对应 skills 目录即可
```

## 使用

装好后直接用自然语言触发，例如：

- 「我大三，想考 2027 研究生，帮我做个考研规划」→ 触发画像收集
- 「东南大学计算机专硕好考吗？」→ 触发择校研究 + 招生信息实时核验（需联网工具）
- 「数学强化卡了两个月，正确率上不去，坚持不下去了」→ 触发诊断 + 做减法调整

之后每次会话自动读取 `kaoyan-profile.md` 续接上下文。

## 文件结构

```
kaoyan-mentor/
├── SKILL.md                      # 主文件：会话协议 / 信息真实性 / 分诊路由 / 通用原则
├── references/
│   ├── intake-profile.md         # 画像收集模板 + 档案模板与维护规则
│   ├── school-selection.md       # 择校研究流程 + 三档候选池 + 动态重评
│   ├── subject-coaching.md       # 四科导师模式 + 真题分析 + 能力雷达
│   ├── planning-loop.md          # 阶段规划 / 周月复盘 / 动态调整 / 风险雷达
│   └── info-integrity.md         # 必查清单 / 来源分级 / 交叉验证 / 禁止伪精确
└── test-prompts.json             # 3 组典型测试 prompt（画像 / 择校 / 执行力危机）
```

## 质量说明

本 skill 经 [darwin-skill](https://github.com/alchaincyf/darwin-skill) 优化流程验证（两轮）：
每轮均为「带/不带 skill 的真实子 agent 对比测试（3+ 组场景）」+「每轮改动由 3 个独立 judge paired 评审」（全部 3-0 一致通过，0 回滚）。
第一轮修复"首次接触输出全年计划"短板（计划跨度 15 个月 → 当前阶段 2-4 周，并加输出边界硬约束）；
第二轮修复"建档流程挤薄救急内容"（科目求助先救急、建档问卷收敛到末尾 2 问、周复盘强制档案数据对照）、软化措辞清零、首次接触流程去重（单一事实源）。

**注意**：招生数据相关回答会要求联网核验官方来源（研招网/院校官网），无联网能力时明确标注降级，不编造数据。

## License

[MIT](LICENSE)
