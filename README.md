# ruleset

自用 mihomo / OpenClash rule-providers。

域名和 IP 已拆分，便于 IP 规则集统一加 `no-resolve`。

## 文件

| 文件 | behavior | 用途 | 主配置引用 |
|---|---|---|---|
| `selfhost.yaml` | domain | 重要自建站点 | `RULE-SET,my-selfhost,自建` |
| `direct-domain.yaml` | classical | 自定义直连域名/关键字 | `RULE-SET,my-direct-domain,DIRECT` |
| `direct-ip.yaml` | ipcidr | 自定义直连 IP | `RULE-SET,my-direct-ip,DIRECT,no-resolve` |

> `GEOSITE,bytedance` 不放在本仓库，请写在主配置 `rules` 中。

## Raw 链接

```text
https://raw.githubusercontent.com/chiyongtan/ruleset/main/selfhost.yaml
https://raw.githubusercontent.com/chiyongtan/ruleset/main/direct-domain.yaml
https://raw.githubusercontent.com/chiyongtan/ruleset/main/direct-ip.yaml
```

jsDelivr（国内可备用）：

```text
https://cdn.jsdelivr.net/gh/chiyongtan/ruleset@main/selfhost.yaml
https://cdn.jsdelivr.net/gh/chiyongtan/ruleset@main/direct-domain.yaml
https://cdn.jsdelivr.net/gh/chiyongtan/ruleset@main/direct-ip.yaml
```

## 主配置示例

```yaml
rule-providers:
  my-selfhost:
    type: http
    behavior: domain
    format: yaml
    interval: 86400
    path: ./ruleset/my-selfhost.yaml
    url: https://raw.githubusercontent.com/chiyongtan/ruleset/main/selfhost.yaml

  my-direct-domain:
    type: http
    behavior: classical
    format: yaml
    interval: 86400
    path: ./ruleset/my-direct-domain.yaml
    url: https://raw.githubusercontent.com/chiyongtan/ruleset/main/direct-domain.yaml

  my-direct-ip:
    type: http
    behavior: ipcidr
    format: yaml
    interval: 86400
    path: ./ruleset/my-direct-ip.yaml
    url: https://raw.githubusercontent.com/chiyongtan/ruleset/main/direct-ip.yaml

rules:
  - RULE-SET,my-selfhost,自建
  - RULE-SET,my-direct-domain,DIRECT
  - RULE-SET,my-direct-ip,DIRECT,no-resolve
  - GEOSITE,bytedance,DIRECT
  # ... 其余规则（广告拦截等）...
```

建议把上述自制 `RULE-SET` 放在广告规则之前。
