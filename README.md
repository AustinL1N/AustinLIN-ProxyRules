# Claude-Rules

个人维护的 Claude 分流规则，共 22 条，按用户提供的列表整理。

## 文件

- [Claude.list](Claude.list)：Quantumult X 远程分流文件，默认策略组为 `AI`。
- [Claude.rules](Claude.rules)：保留原始 `DOMAIN / DOMAIN-SUFFIX / DOMAIN-KEYWORD / IP` 格式，供后续维护或转换。

## Quantumult X 订阅

订阅地址：[Claude.list 原始文件](https://raw.githubusercontent.com/AustinL1N/Claude-Rules/main/Claude.list)。

在 Quantumult X 的「分流 → 资源」中添加上述链接，策略选择 `AI`。本地配置中需要已有名为 `AI` 的策略组。

也可以把下面一行加入现有配置的 `[filter_remote]` 段：

```ini
https://raw.githubusercontent.com/AustinL1N/Claude-Rules/main/Claude.list, tag=Claude, force-policy=AI, enabled=true
```

`Claude.list` 是独立规则资源，不包含 `[filter_local]`、`[filter_remote]` 或最终直连规则。

## 维护

编辑 GitHub 默认分支中的 `Claude.list` 并提交，订阅地址保持不变。客户端下次更新资源时获取新版本；需要立即生效时可手动更新资源。

`Claude.rules` 与 `Claude.list` 为分别维护的文件，修改匹配条件时应同步更新，两者没有自动转换流程。

## 格式与范围说明

- `anthropic.com` 的后缀规则已覆盖 `cdn / mcp / console / workbench.anthropic.com`，无需重复添加。
- `datadog` 和 `sift` 关键词规则保持启用，与原始列表一致；它们也可能匹配其他包含对应关键词的域名。
- Sentry、Statsig、Intercom 等属于共享第三方服务，规则也会影响其他使用这些服务的网站。
- IP 段和 ASN 按原始列表保留，本仓库未核实其当前归属。
- Quantumult X 文件使用原生 `ip-cidr / ip6-cidr / ip-asn` 格式，没有直接照搬原始格式的 `no-resolve` 参数；不保证跨客户端 DNS 行为一致。
- 格式参考：[Quantumult X 官方配置示例](https://github.com/crossutility/Quantumult-X/blob/master/sample.conf)。
