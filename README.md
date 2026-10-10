# AustinLIN-ProxyRules

个人维护的代理分流规则，按客户端和规则集分类：Claude 规则 22 条，Austin-PrivateRules 规则 55 条。

## 目录

```text
AustinLIN-ProxyRules/
├── QuantumultX/
│   ├── Claude/
│   │   └── Claude.list
│   └── Austin-PrivateRules/
│       └── Austin-PrivateRules.list
├── Clash/
│   └── Claude/
│       └── Claude.list
└── README.md
```

- [QuantumultX/Claude/Claude.list](QuantumultX/Claude/Claude.list)：使用 Quantumult X 原生三列格式：规则类型、匹配条件、策略。文件使用 `claude` 作为占位策略，订阅设置可覆盖为所需策略组。
- [QuantumultX/Austin-PrivateRules/Austin-PrivateRules.list](QuantumultX/Austin-PrivateRules/Austin-PrivateRules.list)：个人规则 55 条，保留提供时的匹配顺序和策略组。
- [Clash/Claude/Claude.list](Clash/Claude/Claude.list)：保留原始 `DOMAIN / DOMAIN-SUFFIX / DOMAIN-KEYWORD / IP` 格式及 `no-resolve` 参数，不写入策略组。

## Quantumult X Claude 订阅

订阅地址：[Quantumult X Claude 规则](https://raw.githubusercontent.com/AustinL1N/AustinLIN-ProxyRules/refs/heads/main/QuantumultX/Claude/Claude.list)。

```text
https://raw.githubusercontent.com/AustinL1N/AustinLIN-ProxyRules/refs/heads/main/QuantumultX/Claude/Claude.list
```

在 Quantumult X 中添加上述资源，并在资源设置中选择所需策略组（例如 `AI`），对应配置参数为 `force-policy=AI`。设置后将覆盖文件中的占位策略 `claude`。

Quantumult X 原生规则不能省略第三列策略字段；仅写 `HOST-SUFFIX,anthropic.com` 会出现 `Invalid Line`。文件保持 `HOST-SUFFIX,anthropic.com,claude` 格式，不固定绑定你的 `AI` 分组。

例如，在现有配置的 `[filter_remote]` 段添加：

```ini
https://raw.githubusercontent.com/AustinL1N/AustinLIN-ProxyRules/refs/heads/main/QuantumultX/Claude/Claude.list, tag=Claude, force-policy=AI, enabled=true
```

如果使用其他分组，请替换 `force-policy` 的值，并确保该分组已存在。

`QuantumultX/Claude/Claude.list` 是独立规则资源，不包含 `[filter_local]`、`[filter_remote]` 或最终直连规则。

## Quantumult X Austin-PrivateRules 订阅

订阅地址：[Austin-PrivateRules](https://raw.githubusercontent.com/AustinL1N/AustinLIN-ProxyRules/refs/heads/main/QuantumultX/Austin-PrivateRules/Austin-PrivateRules.list)。

```text
https://raw.githubusercontent.com/AustinL1N/AustinLIN-ProxyRules/refs/heads/main/QuantumultX/Austin-PrivateRules/Austin-PrivateRules.list
```

在 Quantumult X 中添加上述分流资源。该文件保留 `节点/规则更新`、`外网`、`AI` 和 `direct` 分组，使用文件内分组时请确保对应自定义策略组已存在。如需保留不同规则的原分组，不要为整个资源设置统一的 `force-policy`。

可将下面一行加入现有配置的 `[filter_remote]` 段：

```ini
https://raw.githubusercontent.com/AustinL1N/AustinLIN-ProxyRules/refs/heads/main/QuantumultX/Austin-PrivateRules/Austin-PrivateRules.list, tag=Austin-PrivateRules, enabled=true
```

## Clash / Mihomo 订阅

规则地址：[Clash Claude 规则](https://raw.githubusercontent.com/AustinL1N/AustinLIN-ProxyRules/refs/heads/main/Clash/Claude/Claude.list)。

```text
https://raw.githubusercontent.com/AustinL1N/AustinLIN-ProxyRules/refs/heads/main/Clash/Claude/Claude.list
```

在支持该格式的 Clash / Mihomo 客户端中，将规则资源设为 `behavior: classical`、`format: text`，再在客户端配置中指定策略组。配置格式参考：[Mihomo 规则集合文档](https://wiki.metacubex.one/config/rule-providers/)。

## 地址迁移

仓库根目录的 `Claude.list` 已移到 `QuantumultX/Claude/Claude.list`，`Claude.rules` 已移到 `Clash/Claude/Claude.list`。已订阅旧地址的客户端需要替换为上面的新地址。

## 维护

编辑 GitHub 默认分支中对应客户端及规则集目录下的 `.list` 文件并提交。在文件路径不变的情况下，订阅地址保持不变。客户端下次更新资源时获取新版本；需要立即生效时可手动更新资源。

Claude 的两种客户端格式为分别维护的文件，修改匹配条件时应同步更新，两者没有自动转换流程。Austin-PrivateRules 当前仅提供 Quantumult X 格式。

## 格式与范围说明

- `anthropic.com` 的后缀规则已覆盖 `cdn / mcp / console / workbench.anthropic.com`，无需重复添加。
- `datadog` 和 `sift` 关键词规则保持启用，与原始列表一致；它们也可能匹配其他包含对应关键词的域名。
- Sentry、Statsig、Intercom 等属于共享第三方服务，规则也会影响其他使用这些服务的网站。
- IP 段和 ASN 按原始列表保留，本仓库未核实其当前归属。
- Quantumult X 文件使用原生 `ip-cidr / ip6-cidr / ip-asn` 格式，没有直接照搬原始格式的 `no-resolve` 参数；不保证跨客户端 DNS 行为一致。
- 格式参考：[Quantumult X 官方配置示例](https://github.com/crossutility/Quantumult-X/blob/master/sample.conf)。
