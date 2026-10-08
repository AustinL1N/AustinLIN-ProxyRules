# Claude-Rules

个人维护的 Claude 分流规则，共 22 条，按用户提供的列表整理。

## 目录

```text
Claude-Rules/
├── QuantumultX/
│   └── Claude/
│       └── Claude.list
├── Clash/
│   └── Claude/
│       └── Claude.list
└── README.md
```

- [QuantumultX/Claude/Claude.list](QuantumultX/Claude/Claude.list)：使用 Quantumult X 风格的规则类型，每条规则只保留类型和匹配条件，策略组由订阅 App 设置。
- [Clash/Claude/Claude.list](Clash/Claude/Claude.list)：保留原始 `DOMAIN / DOMAIN-SUFFIX / DOMAIN-KEYWORD / IP` 格式及 `no-resolve` 参数，不写入策略组。

## Quantumult X 订阅

订阅地址：[Quantumult X Claude 规则](https://raw.githubusercontent.com/AustinL1N/Claude-Rules/main/QuantumultX/Claude/Claude.list)。

在订阅 App 中添加上述链接，并在 App 中选择所需策略组。规则文件不再指定 `AI` 或其他策略组。

`QuantumultX/Claude/Claude.list` 是独立规则资源，不包含 `[filter_local]`、`[filter_remote]` 或最终直连规则。

## Clash / Mihomo 订阅

规则地址：[Clash Claude 规则](https://raw.githubusercontent.com/AustinL1N/Claude-Rules/main/Clash/Claude/Claude.list)。

在支持该格式的 Clash / Mihomo 客户端中，将规则资源设为 `behavior: classical`、`format: text`，再在客户端配置中指定策略组。配置格式参考：[Mihomo 规则集合文档](https://wiki.metacubex.one/config/rule-providers/)。

## 地址迁移

仓库根目录的 `Claude.list` 已移到 `QuantumultX/Claude/Claude.list`，`Claude.rules` 已移到 `Clash/Claude/Claude.list`。已订阅旧地址的客户端需要替换为上面的新地址。

## 维护

编辑 GitHub 默认分支中对应客户端目录下的 `Claude/Claude.list` 并提交。在文件路径不变的情况下，订阅地址保持不变。客户端下次更新资源时获取新版本；需要立即生效时可手动更新资源。

两种客户端格式为分别维护的文件，修改匹配条件时应同步更新，两者没有自动转换流程。

## 格式与范围说明

- `anthropic.com` 的后缀规则已覆盖 `cdn / mcp / console / workbench.anthropic.com`，无需重复添加。
- `datadog` 和 `sift` 关键词规则保持启用，与原始列表一致；它们也可能匹配其他包含对应关键词的域名。
- Sentry、Statsig、Intercom 等属于共享第三方服务，规则也会影响其他使用这些服务的网站。
- IP 段和 ASN 按原始列表保留，本仓库未核实其当前归属。
- Quantumult X 文件使用原生 `ip-cidr / ip6-cidr / ip-asn` 格式，没有直接照搬原始格式的 `no-resolve` 参数；不保证跨客户端 DNS 行为一致。
- 格式参考：[Quantumult X 官方配置示例](https://github.com/crossutility/Quantumult-X/blob/master/sample.conf)。
