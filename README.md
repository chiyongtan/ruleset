# ruleset

自用 mihomo / OpenClash rule-providers（classical + yaml）。

## 文件

| 文件 | 用途 | 主配置引用 |
|---|---|---|
| `selfhost.yaml` | 重要自建站点 | `RULE-SET,my-selfhost,自建` |
| `direct.yaml` | 自定义直连（含抖音/手心/夸克/IP） | `RULE-SET,my-direct,DIRECT` |

> `GEOSITE,bytedance` 不放在本仓库，请写在主配置 `rules` 中。

## Raw 链接

```text
https://raw.githubusercontent.com/chiyongtan/ruleset/main/selfhost.yaml
https://raw.githubusercontent.com/chiyongtan/ruleset/main/direct.yaml
```

jsDelivr（国内可备用）：

```text
https://cdn.jsdelivr.net/gh/chiyongtan/ruleset@main/selfhost.yaml
https://cdn.jsdelivr.net/gh/chiyongtan/ruleset@main/direct.yaml
```

## 主配置示例

```yaml
rule-providers:
  my-selfhost:
    type: http
    behavior: classical
    format: yaml
    interval: 86400
    path: ./ruleset/my-selfhost.yaml
    url: https://raw.githubusercontent.com/chiyongtan/ruleset/main/selfhost.yaml

  my-direct:
    type: http
    behavior: classical
    format: yaml
    interval: 86400
    path: ./ruleset/my-direct.yaml
    url: https://raw.githubusercontent.com/chiyongtan/ruleset/main/direct.yaml

rules:
  - RULE-SET,my-selfhost,自建
  - RULE-SET,my-direct,DIRECT
  - GEOSITE,bytedance,DIRECT
  # ... 其余规则（广告拦截等）...
```

建议把上述两条 `RULE-SET` 放在广告规则之前。
