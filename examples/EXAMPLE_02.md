# EXAMPLE_02: 反面案例 — 锻造失败：把 G1-G6 footer 当 R3

## 反例
```
声称: "skill-forge 成功将 dbs-hook 从 STUB 升级到 R3"
实际操作: 只在文件末尾加了 G1-G6 表格
git diff 显示: +8 行（全在文件末尾，纯 footer）
body 零改动
```

## 为什么是反例
1. **没有走锻造流程**: 跳过了 Step 2（提取模式）和 Step 3（锻造 description）
2. **冒充 RICH**: 加了 footer 但 body 仍然是 STUB
3. **不可验证**: 没有 references/ 保存升级前的原始版本
4. **虚假对比**: 声称 "456B→4.8KB" 但文件大小只增加了 200B

## 正确做法
- 必须走完 6 Step 完整流程
- git diff 必须显示 body 的实质性改动（不只是 footer）
- references/ 中保留升级前版本作为对比证据
- 优化后大小至少增长 3x（靠实质内容，非灌水）

## skill-overseer 检测方式
```powershell
# 检测伪 R3
git diff HEAD~1..HEAD --stat | grep SKILL.md
# 如果只 +10 行左右 → 疑似只加 footer
# 必须检查 diff 内容确认
```
