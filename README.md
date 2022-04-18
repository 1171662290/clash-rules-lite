<p align="center">
 <img width="100px" src="https://github.com/Dreamacro/clash/raw/master/docs/logo.png" align="center" alt="GitHub Readme Stats" />
 <h2 align="center">Clash Rules Lite</h2>
 
 <p align="center">🍒 自定义代理规则，精简匹配规则，适合学生和开发者使用。</p>
 
 <p align="center">
  <a href="https://github.com/zhanyeye/clash-rules-lite/blob/master/.github/workflows/release.yml">
   <img src="https://github.com/zhanyeye/clash-rules-lite/actions/workflows/release.yml/badge.svg" />
  </a>
 </p>
 
 <p>
  <pre align="center">https://cdn.jsdelivr.net/gh/zhanyeye/clash-rules-for-dev@release/rules.txt</pre>
 </p>
</p>


#### 使用方法
1. 拷贝一份订阅脚本到 `local file`。
<div align=center>
    <img width="750" src="https://user-images.githubusercontent.com/35565811/147398760-17324346-2fa3-4390-ad80-3d830ec8c58d.png">
</div>

2. 在 `local file` 脚本中，修改配置如下，保留你的 `proxies` 和 `proxy-groups`
```
mixed-port: 7890
allow-lan: true
bind-address: '*'
mode: rule
log-level: info
external-controller: '127.0.0.1:9090'
proxies:
    - { name: 'S-101 | 香港', type: ****, server: ****, port: ****, cipher: ****, password: ****, udp: true }
    - { name: 'S-102 | 香港', type: ****, server: ****, port: ****, cipher: ****, password: ****, udp: true }
proxy-groups:
    - { name: 'PROXY', type: select, proxies: ['S-101 | 香港', 'S-102 | 香港'] }
rules:
  - RULE-SET,pac,PROXY
rule-providers:
  pac:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/zhanyeye/clash-rules-for-dev@release/rules.txt"
    path: ./rules/pac.yaml
    interval: 86400
script:
  code: |
    def main(ctx, metadata):
        keywords = ["google", "github"]
        for key in keywords:
            if key in metadata["host"]:
                return "PROXY"
        if ctx.rule_providers["pac"].match(metadata):
            return "PROXY"
        else:
            return "DIRECT"

```
3. 运行修改后的 `local file`，再切换成 `Rule` 或 `Script` 模式。
<div align=center>
    <img width="750" src="https://user-images.githubusercontent.com/35565811/147398721-88a75d2b-ce4d-4605-80a1-60871907f64d.png">
</div>
