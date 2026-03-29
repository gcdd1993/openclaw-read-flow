# Source Policy

## 源分层

### 核心跟踪源

适用条件：

- 长期稳定更新
- 与重点主题持续相关
- 历史上稳定提供高价值内容

### 观察源

适用条件：

- 有价值，但输出不稳定
- 更适合作为补充，而不是主干

### 机会源

适用条件：

- 围绕短期主题临时加入
- 活动、热点、专项研究期间使用

## 推荐注册表字段

- `source_name`
- `source_url`
- `feed_url`
- `source_type`
- `theme`
- `priority`
- `update_frequency`
- `maintenance_notes`
- `fallback_plan`

## 接入决策

- 能直接用 RSS，就不用抓取脚本。
- 能用成熟转换工具，就不立刻自写抓取。
- 只有当现成方案不稳定或不可用时，再考虑自定义抓取。
- 若已有 FreshRSS，则优先把各源汇入 FreshRSS，再由下游统一读取 FreshRSS。

