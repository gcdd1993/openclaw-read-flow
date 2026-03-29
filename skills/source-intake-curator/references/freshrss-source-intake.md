# FreshRSS Source Intake

## 角色定位

当工作区已经有 FreshRSS 时：

- FreshRSS 是聚合池。
- 各种 RSS / RSSHub / GitHub Feed / 其他转换源 是上游信息源。
- Digest 不直接抓单个源，而是统一从 FreshRSS 的未读列表读取。

## 推荐记录字段

- `freshrss_base_url`
- `freshrss_api_url`
- `username`
- `api_password_config`
- `default_digest_input`

其中：

- `freshrss_api_url` 一般为 `<base_url>/api/greader.php`
- `default_digest_input` 推荐写为 `unread-reading-list`
- `api_password_config` 只记录配置方式，不记录明文密码

## 使用建议

- 在源注册表中区分“原始信息源”和“Digest 读取入口”。
- 不把 API password 直接写进文档；只写环境变量名或配置文件路径。
- 若 FreshRSS 失效，再回退到直接源抓取。
