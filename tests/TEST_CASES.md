# skill-forge 测试用例

## TC01: STUB→RICH 完整锻造
**输入**: dbs-learning (456B, STUB)
**预期**: 走完 6 Step，产出 ≥4KB 的 RICH skill
**通过条件**: git diff 显示 body 有实质性改动（非仅 footer）

## TC02: 锻造 description — 触发词 ≥6
**输入**: 任何 STUB skill
**预期**: 新 description 含 ≥6 触发词 + 正反例各 2 + 边界说明
**通过条件**: description 符合 G2 规范

## TC03: 检测伪 R3 — 只加 footer
**输入**: skill 声称 R3 但 git diff 只显示 +8 行
**预期**: 识别为伪 R3，拒绝通过
**通过条件**: G1-G6 不全是 GREEN，body 无改动 = 非 R3

## TC04: 从 references/ 恢复原始版本
**输入**: skill 有 references/original_body.md
**预期**: 从 reference 读取原始素材作为锻造输入
**通过条件**: 锻造基于原始素材，非凭空生成

## TC05: 锻造失败兜底 — 至少 3 种场景
**输入**: 任何 skill
**预期**: 新版本含 ≥3 种失败场景 + 兜底处理
**通过条件**: 失败兜底表非模板复制
