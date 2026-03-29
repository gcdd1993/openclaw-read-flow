# OpenClaw Read Flow

基于“漏斗式阅读流”思路实现的一套 OpenClaw / FreshRSS 阅读处理工作区。

目标不是把信息流直接写成“看起来很聪明”的终稿，而是把阅读流程拆成稳定的几个阶段：

1. 从 FreshRSS 聚合池抓取未读条目
2. 默认切出“昨天”这个自然日窗口
3. 构建 Digest：去重、抓正文、质量检查、噪音过滤、摘要、排序
4. 产出 Daily Review：按固定栏目重组为可快速阅读的日报
5. 视需要再接知识库、笔记或后续自动化

## 目录结构

```text
openclaw-read-flow/
  execution-plan.md
  README.md
  digests/
  reviews/
  skills/
```

- `execution-plan.md`
  工作流执行计划与阶段拆分。
- `digests/`
  Digest 阶段的中间产物和输出目录。
- `reviews/`
  Daily Review 输出目录。
- `skills/`
  OpenClaw 可直接使用的技能定义。

## 当前技能

- `read-flow-orchestrator`
  负责总控、阶段判断和输入输出契约。
- `source-intake-curator`
  负责信息源接入与 FreshRSS 聚合池定位。
- `digest-builder`
  负责未读抓取、日期切片、Digest 构建。
- `daily-review-editor`
  负责将 Digest 重组为固定栏目日报。
- `knowledge-distiller`
  负责后续知识沉淀模板。
- `profile-feedback-optimizer`
  负责反馈信号与轻量排序建议。

## Digest 流程

Digest 默认处理顺序：

1. FreshRSS 全量未读抓取
2. 昨天窗口切片
3. URL 精确去重
4. 相似内容聚类去重
5. 正文抓取
6. 质量检查
7. 噪音过滤
8. 摘要生成
9. 初步排序
10. JSON / Markdown 输出

对应脚本：

- `skills/digest-builder/scripts/fetch_freshrss_unread.py`
- `skills/digest-builder/scripts/slice_freshrss_by_date.py`
- `skills/digest-builder/scripts/build_digest.py`

## Daily Review 固定栏目

Daily Review 默认固定为 6 个栏目，顺序不变：

1. `今日大事`
2. `变更与实践`
3. `安全与风险`
4. `开源与工具`
5. `洞察与数据点`
6. `主题深挖`

不再使用“产业与公司动态”“云与基础设施”“研究与治理”“今日观察”这类题材型栏目替代固定栏目体系。

## 快速开始

### 1. 配置 FreshRSS

复制示例配置并填写你自己的实例信息：

```json
{
  "base_url": "https://your-freshrss.example.com",
  "username": "your-freshrss-username",
  "api_password": "replace-with-api-password"
}
```

建议使用环境变量或本地配置文件，不要把真实凭据写进仓库。

### 2. 抓取未读

```powershell
python .\skills\digest-builder\scripts\fetch_freshrss_unread.py --config .\skills\digest-builder\scripts\freshrss.config.json
```

### 3. 切昨天窗口

```powershell
python .\skills\digest-builder\scripts\slice_freshrss_by_date.py `
  --source-json .\digests\raw-freshrss.json `
  --output-json .\digests\freshrss-yesterday.json `
  --output-md .\digests\freshrss-yesterday.md `
  --timezone Asia/Shanghai
```

### 4. 构建 Digest

```powershell
python .\skills\digest-builder\scripts\build_digest.py `
  --source-json .\digests\freshrss-yesterday.json `
  --output-json .\digests\YYYY-MM-DD-digest.json `
  --output-md .\digests\YYYY-MM-DD-digest.md
```

## 发布说明

这个仓库按公开发布做了默认收敛：

- `.gitignore` 默认忽略 `digests/` 和 `reviews/` 中的生成产物
- 示例配置不包含真实实例地址和真实凭据
- 不提交本地 FreshRSS API password
- 不提交 IMA / 知识库相关密钥或用户私有 ID

如果要提交到 GitHub 或 ClawHub，建议只提交：

- `execution-plan.md`
- `README.md`
- `skills/`
- 必要的示例模板和参考文档

不建议提交：

- 原始抓取 JSON / Markdown
- 每日生成的 Digest 和 Review 成品
- 本地配置文件
- 任何含真实账号、实例域名、知识库 ID 的文件

## 当前状态

已完成：

- FreshRSS Google Reader API 抓取
- 昨天窗口切片
- 结构化 Digest 构建脚本
- 固定 6 栏 Daily Review 模板

待继续工程化的部分：

- 更高质量的英文文章中文摘要
- 从 Digest 自动生成 Daily Review 的脚本化流程
- 知识库 / 笔记系统的稳定发布链路
