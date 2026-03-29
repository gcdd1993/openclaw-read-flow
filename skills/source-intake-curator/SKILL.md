---
name: source-intake-curator
description: "阅读流上游的信息源接入、RSS 归一、源分组、优先级分层与注册表维护。用于需要把博客、社区、GitHub、公众号、社交账号或任意更新页面转换为统一 feed 输入，或把这些源汇聚进 FreshRSS 作为 Digest 上游，并为后续 Digest 提供稳定候选池的场景。"
---

# Source Intake Curator

以简体中文工作。目标是把多种形态的信息源统一成可持续消费的 feed，而不是一次性抓一堆链接。若工作区已经搭建 FreshRSS，优先把 FreshRSS 视为唯一聚合池入口。

## 核心原则

- 优先 RSS，其次是可稳定转换为 feed 的方案。
- 上游可以多样，下游格式必须尽量统一。
- 为长期运行服务，不为单次抓取凑合。
- 若已接入 FreshRSS，不让 Digest 直接回源到每个站点，而是统一从 FreshRSS 的未读池读取。

## 处理步骤

1. 识别信息源类型：
   - 原生 RSS
   - 可转换源
   - 需要自定义抓取的页面
2. 选择接入方式：
   - 原生 RSS
   - RSSHub / RSS-Bridge
   - GitHub feed
   - wewe-rss
   - 自定义抓取
3. 记录注册表字段：
   - 名称
   - 原始地址
   - feed 地址
   - 类型
   - 主题
   - 更新频率
   - 优先级
   - 失败兜底方案
4. 执行源分组：
   - 核心跟踪源
   - 观察源
   - 机会源
5. 若使用 FreshRSS，同步记录聚合池接入信息：
   - FreshRSS 基础地址
   - API 地址
   - 用户名
   - API password 的配置方式
   - 未读列表是否作为 Digest 默认输入

## 输出要求

- 输出统一的源注册表。
- 标出不稳定来源和维护成本。
- 如果某来源无法稳定转换为 feed，要明确说明原因和替代方案。
- 若使用 FreshRSS，要明确“源列表”和“Digest 读取入口”是两层结构。

## 质量标准

- 不接受“只能手工偶尔看看”的伪接入。
- 不把临时测试链接误写成长期源。
- 不把源分组和主题分类混为一谈。

## 反例禁区

- 只给一串链接，不给接入方式和用途。
- 忽略更新频率，导致下游被高噪音源淹没。
- 为了多接入而接入，缺少长期维护意识。

## 参考文件

- 信息源分层与注册表规范：`references/source-policy.md`
- FreshRSS 聚合池接入说明：`references/freshrss-source-intake.md`

