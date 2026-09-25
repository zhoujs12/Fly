# Work Agent 起飞观测指标跟踪

**目的**:判断通用「work agent」(面向非工程职能的知识工作 agent)是否会复制 coding agent 2025–2026 的起飞曲线。

**建立日期**:2026-09-25
**复查频率**:每月一次(对齐 Ramp AI Index 发布节奏);AEI 指标每次新版发布时更新
**维护方式**:每次复查在「快照记录」表追加一行,不覆盖历史行

---

## 参照系:coding agent 的起飞曲线

作为"什么才算起飞"的基准线:

| 产品 | $100M → $500M | 后续 |
|---|---|---|
| Cursor | 5 个月(2025-01 → 2025-06) | 2025-11 $1B;2026-02 $2B;2026-05 $4B |
| Claude Code | 公开发布 6 个月内破 $1B(2025-05 → 11) | 2026-02 $2.5B;2026-05 约 $8B |

**特征签名**:单一产品在 12–18 个月内做到十亿美元级 ARR,期间约每 2 个月翻一倍。
**判据**:work agent 侧若出现同等形状,即可确认"起点已到"。

---

## 六项观测指标

### I1 — 非工程职能 agent 周活增速 / 工程职能
- **基线(2026-06,OpenAI 企业口径,自 2026-02 起算)**:法务 108×、销售 41×、招聘 41×、市场 26×,工程 5×
- **确认阈值**:该比值连续 2–3 个季度维持 ≥3×(当前 5–20×,但基数极低,关键看可持续性)
- **数据源**:OpenAI enterprise / signals 系列文章;Anthropic 同类披露
- **频率**:季度
- **注意**:这一数据是"coding agent(Codex)被非工程岗位拿去用",不是独立 work agent 产品。渠道复用 vs 新品类,要分开看。

### I2 — 单个 work agent 产品 $100M → $500M ARR 用时
- **基线(2026-09)**:尚无产品达成。最快者 Glean,2026-05-28 宣布破 $300M,距 $100M 用了 15 个月;Harvey $300M ARR($11B 估值);Sierra 2026-05 $200M(2024 年底仅 $26M)
- **确认阈值**:≤12 个月
- **数据源**:公司公告、Sacra、TechCrunch
- **频率**:月度

### I3 — pilot → production 转化率
- **基线(2026 年中)**:约 12%(即约 88% 的 agent 试点进不了生产)。主要卡点:评估缺失 64%、治理摩擦 57%、模型可靠性 51%。Gartner 预计 2027 年底前 40%+ agentic AI 项目被取消
- **确认阈值**:≥30%
- **数据源**:Gartner、各家企业调研
- **频率**:季度
- **数据质量**:⚠️ 基线数字来自二手转引,可信度中等,复查时优先找一手报告

### I4 — 长程多步任务成功率(瓶颈中的瓶颈)
- **基线(2026 年中)**:单轮任务 80–90%;跨应用持续多步工作流掉到 **18–24%**;上下文保持超过约 35 分钟开始崩,失败率随时长指数上升
- **确认阈值**:≥50%
- **数据源**:GAIA / OSWorld / τ-bench 等 agentic benchmark 榜单;各实验室 model card
- **频率**:月度
- **重要性**:★★★ 这条是物理约束。它一旦突破,I1–I3 会自动跟上;它不破,其余指标都是虚的。

### I5 — 定价模式:seat → outcome / per-task
- **基线(Ramp,2026-09 号)**:采用面仍在扩(更多企业在付费),但重度用户的 spend-per-seat 在软化;有效 token 价格自 2026-03 已跌 **41%**;买方主动把流量从最贵的模型上挪走。前沿模型(Opus/Fable/Sol)token 份额 45%,低于 8 月 53% 的峰值
- **确认阈值**:outcome-based / per-task 合同成为主流形式
- **数据源**:Ramp AI Index(月度)、厂商定价页
- **频率**:月度
- **解读**:seat 制软化 + token 价格下跌,既可能是"价值未兑现"的坏信号,也可能是"从卖席位转向卖完成量"的过渡期。需要结合 I2 一起读。

### I6 — AEI 运营类话题 vs 编码类话题占比(自建复合指标)
基于 Anthropic Economic Index 的 top_request_topics 自建两个 bundle:

| Bundle | 构成 | 2026-05 占比 |
|---|---|---|
| **运营/知识工作** | Business Process & Operations 4.70 + Document Processing & Extraction 4.32 + Data Analysis & BI 3.83 + Knowledge Retrieval & Enterprise Search 3.61 + Sales & Revenue Ops 1.10 + Compliance & Regulatory 1.06 + Customer Support 0.60 + Conversation & Meeting Intelligence 0.26 | **19.48%** |
| **编码** | Software Development 11.51 + DevOps & Infrastructure Ops 2.82 | **14.33%** |
| | **比值** | **1.36** |

配套读数(同期,全球):
- automation 48.62% / augmentation 51.38%
- work 43.36% / personal 40.20% / coursework 16.45%
- 产物类型:document or report 14.91% vs app or website 4.21%
- 分类器估计:独自需约 5 小时的任务,与 Claude 对话约 40 分钟完成

- **确认阈值**:比值持续上升,**且** automation_pct 突破 55%(委托深度实质提升)
- **数据源**:Anthropic Economic Index(MCP 工具可直接查,或 https://www.anthropic.com/economic-index)
- **频率**:每次新版发布(约季度)

#### ⚠️ AEI 使用限制(必读)
1. **数据集本身没有趋势序列**。2026-09 时点的 temporal_coverage 只有 2026-04 → 2026-05,服务的是**最新一期快照**。官方明确说明:这份数据无法显示份额在上升或下降。→ 所以 I6 的趋势必须靠我们**逐期抓取快照、自己记录**来构建。
2. 口径是 **Claude chat + Cowork**,**不含 Claude Code**。因此 I6 的"编码 bundle"严重低估了真实编码用量,两个 bundle **不能当作公平的正面对比**;I6 的价值在于看它自己随时间的变化,而不是绝对高低。
3. 数据是把对话内容匹配到 O*NET 职位任务,**不是**用户职业。正确表述是"用于法务类任务的对话",而非"法务人员在用"。
4. 该数据不支持任何关于就业、岗位替代或职业安全的推论,也不能用来论证 AI 用量是岗位自动化的先行指标。

---

## 当前总体判断(2026-09-25)

work agent 大致处在 coding agent 2024 年底 / 2025 年初的位置。曲线是真的,但尚未进入斜率垂直段。

**形态差异**:不是"新品类从 0 垂直起飞",而是"沿已铺好的渠道横向扩散"——分发层(Microsoft Agent 365 两个月注册约 4000 万 agent;OpenAI Frontier 2026-02-05 发布;Claude Cowork 2026-01 发布)已经就位,缺的是可靠性和可验证性。

**关键窗口**:2026 下半年 – 2027。

**四条结构性约束**(决定能否复制曲线):

| 因素 | coding | knowledge work | 行业正在补的东西 |
|---|---|---|---|
| 可验证性 | 编译器/测试/CI = 免费 ground truth,可自纠错 | 无 verifier | evals、人在环审批 |
| 环境标准化 | 文件系统+git+terminal 通用 | SaaS 孤岛 | MCP、Agent 365、Frontier |
| 用户是否 builder | 开发者能自己 debug harness | 业务用户不能 | Skills / Plugins |
| 错误可逆性 | `git revert` | 发错邮件/改错账目不可逆 | 权限、审计、沙箱 |

---

## 快照记录

每次复查追加一行。`—` 表示本期无新数据。

| 日期 | I1 非工程/工程增速比 | I2 最快 $100M→$500M | I3 pilot→prod | I4 长程成功率 | I5 定价信号 | I6 运营/编码比值 · automation% | 触发阈值? | 备注 |
|---|---|---|---|---|---|---|---|---|
| 2026-09-25 | 5–20×(法务 108× / 工程 5×,2026-02 起算) | 未达成(Glean 15 个月到 $300M) | ~12% | 18–24% | spend-per-seat 软化;token 价 -41% since 03 | 1.36 · 48.62%(期:2026-05) | 否 | 基线建立 |

---

## 复查操作手册

1. **AEI**:调用 Economic Index MCP(`econ_index_get_dataset_overview` 取 `latest_period`;若 period 比上次记录新,则 `econ_index_get_global_usage` 重算 I6 两个 bundle 与 automation_pct)
2. **Ramp AI Index**:搜 `Ramp AI Index <月份> 2026`,取整体采用率、厂商份额、spend-per-seat、token 价格走向 → I5
3. **ARR 里程碑**:搜 Glean / Harvey / Sierra / Decagon / Cowork + `ARR` → I2
4. **benchmark**:搜 agentic benchmark 长程任务成功率最新榜 → I4
5. **调研报告**:搜 pilot-to-production / Gartner agentic → I3
6. **OpenAI / Anthropic 企业披露**:季度性,搜企业职能维度的使用增长 → I1
7. 在「快照记录」**追加**一行(不改历史行),标注是否有阈值被触发
8. commit + push 到 `claude/claude-cowork-differences-t4km04`

## 数据质量约定

- 一手来源(ramp.com、anthropic.com、openai.com、公司公告、benchmark 官方榜)标 ✅
- 二手 SEO 聚合站转引标 ⚠️,并在备注里写明
- 本环境网络出口受限,无法直接抓取 ramp.com / anthropic.com 页面(WebFetch 与 curl 均被代理拦截),多数外部数字来自搜索摘要。**AEI 是例外**——MCP 工具是一手直连。
