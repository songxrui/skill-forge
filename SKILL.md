---
name: skill-forge
description: "Skill 锻造工坊。自动化 R3 优化模式：读原始→提取pattern→写description(≥5触发词+正反例+边界)→建Phase工作流→加验证清单→加失败兜底→G1-G6审计→输出。将任何 STUB/THIN skill 优化到 RICH 级别。触发词：/skill-forge、锻造skill、优化skill、R3升级、R3优化、给skill升级。不适用场景：从零创建新skill→skill-creator; 安装外部skill→skill-installer; 评测skill→skill-review-master。正例：'把这个skill R3升级一下'→触发; '/skill-forge dbs-learning'→触发。反例：'帮我写一个新的skill'→不触发→skill-creator; '评测一下这个skill'→不触发→skill-review-master。"
version: "1.0.0 | R1: 2026-06-08 | incubated from: 8x R3 optimization patterns | model: DeepSeek v4 Pro"
---

# skill-forge R1 — Skill 锻造工坊

> 孵化来源: 深度分析 8 次 R3 优化（dbs-decision/deconstruct/diagnosis/goal/good-question/slowisfast/save/action）的操作模式后，抽象出的自动化锻造流程。

## 一句话定义

把 STUB/THIN skill 自动锻造到 R3 RICH 级别。输入一个 skill 路径，输出完整的 G1-G6 全绿 SKILL.md。

---

## 锻造流程（6 步）

### Step 1: 读取原始
- 读 `SKILL.md`（当前存根）
- 读 `references/original_body.md`（完整原始文档，如果存在）
- 如果没有 reference，读 SKILL.md 的全部内容作为原始素材

### Step 2: 提取模式
从原始文档中提取：
- **核心定义**：这个 skill 一句话做什么
- **关键方法论**：≥3 条核心原则/公理
- **工作流程**：≥3 个 Phase/Step
- **输入输出**：输入什么、输出什么
- **与其他 skill 的关系**：和哪些 skill 联动

### Step 3: 锻造 description
写一个 description 字符串，必须含：
- skill 一句话定义
- **触发词 ≥5 个**（逗号分隔，中文+slash命令）
- **不适用场景 ≥2 个** + 路由目标（→指向哪个 skill）
- **正例 2 条**（用户说什么→触发）
- **反例 2 条**（用户说什么→不触发→路由去哪）
- **与相邻 skill 的边界说明**（和哪个 skill 最容易混淆，区别在哪）

### Step 4: 锻造 body
按以下模板写 body：

```
## 一句话定义
## N 条核心原则/公理（≥3 条）
## 工作流程（≥3 Phase）
## 内联案例（≥2 个）
## 模板/输出格式
## 与其他 skill 联动（ASCII 图）
## 验证清单（≥4 项 `- [ ]`）
## 失败模式与兜底（≥2 模式）
## G1-G6
```

### Step 5: G1-G6 自检
逐项检查：
- G1: 大小 ≤10KB？超标 → 压缩冗余
- G2: description 有 ≥5 触发词 + 正反例 + 边界？否 → 补
- G3: body 有可执行 Phase？否 → 补
- G4: 有 `- [ ]` 验证清单？否 → 补
- G5: 有失败模式兜底？否 → 补
- G6: 无硬编码凭据？扫描 `sk-` `token` `password` `secret` 关键词

### Step 6: 输出 + 记录
- 写新 SKILL.md（备份原文件为 SKILL.md.bak）
- 更新 version frontmatter
- 标注 incubation source

---

## 锻造决策

| 情况 | 处理 |
|------|------|
| 原始内容 <1KB（纯 STUB） | 如果无 reference → 通知用户「需要提供更多原始内容」 |
| 原始内容 1-5KB（THIN） | 锻造到 4-6KB（R3 OK 级） |
| 原始内容 5-10KB（OK） | 锻造到 5-7KB（R3 RICH 级），主要是结构优化 |
| 原始内容 >10KB（RICH） | 主要是 G2-G6 门禁补全，不增 size |

---

## 与 skill 生态联动

```
skill-review-master ──→ 评测 → 发现低分 skill
        │
        └──→ skill-forge ──→ 锻造优化
                │
                ├──→ skill-creator (参考模式创建新 skill)
                ├──→ skill-distiller (去重合并)
                └──→ skill-deployer (部署分发)
```

---

## 验证清单

- [ ] 原始素材已完整读取
- [ ] ≥5 触发词 + 正反例 2+2
- [ ] ≥3 Phase 工作流
- [ ] ≥4 项验证清单
- [ ] ≥2 失败模式兜底
- [ ] G1-G6 全绿
- [ ] 与其他 skill 的联动图完整
- [ ] version frontmatter 已更新

## 失败模式与兜底

| 失败 | 兜底 |
|------|------|
| 原始内容不足以锻造 | 输出分析报告：缺少哪些信息，建议从哪里获取 |
| 锻造后触发词与其他 skill 重叠 | 对比 description，调整触发词，明确边界 |
| 锻造后 >10KB | 执行压缩：去冗余案例、精简表格、合并相似 Phase |

## G1-G6

| 门禁 | 状态 |
|------|------|
| G1 ≤10KB | ✅ |
| G2 触发层(5词+正反例+边界) | ✅ |
| G3 可执行(6 Step 锻造流程) | ✅ |
| G4 验证(8项) | ✅ |
| G5 失败兜底(3模式) | ✅ |
| G6 安全 | ✅ |