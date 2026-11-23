# 免费订阅节点测试报告 — 2026-11-23 批次

测试时间：2026-11-23（北京时间）。订阅源为 2026-11-23 Grok 自动化邮件中的 14 个链接（13 个可下载，1 个截断无法补全）。
本次为家用代理测试：每个节点经家用代理拨号，口径为“在家宽下可用”。

## 方法

- 工具：mihomo v1.19.34（Clash Meta），逐个节点调用外部控制 API 做延迟测试；
- 测试目标：`http://www.gstatic.com/generate_204`，单个节点超时 5 秒；
- 测试中只请求 generate_204，不经过节点发送任何用户数据或凭证；
- 去重口径：(协议, 服务器, 端口, uuid/密码) 相同算同一个节点；
- 测试方式：家用代理测试——每个节点经 dialer-proxy（home-proxy）拨号，即本地转发器 → Tailscale 隧道 → NAS 上的家用代理，出口为家宽网络；口径为“在家宽下可用”，即节点必须从家宽网络连通才算可用；
- 两轮逐个测试：第一轮逐个测试复核出 531 个可用；对第一轮失败的 19783 个节点又单独复测一轮，新增 30 个可用；本报告以两轮逐个测试结果为准。
- 限制：本机禁止 UDP 出站（实测 UDP DNS 查询被拒绝），因此 hysteria2 / tuic（走 QUIC/UDP）无法在本机验证，本批 214 个 hysteria2 节点及 2 个 tuic 节点均未计入可用——不是证实已死，而是无法测试；如需用 hysteria2，请在支持 UDP 的客户端上自行测速。

## 总览

- 解析出唯一节点：**20653** 个（13 个源，去重后）
- 进入测试：**20314** 个（339 个因配置无效被排除：控制字符 125、未知 ss 加密方式 150、无效密钥 49、空密码 14、无效服务器 1）
- 实测可用：**561** 个（2.8%），其中第一轮 531 个、复测新增 30 个
- 可用节点共 561 个，超过 150 上限，只保留最快的 150 个

## 各源解析情况

| 来源 | 下载 | 新增节点数 |
|---|---|---|
| danmaifu v2ray-20261123.txt | ✅ | 837 条新增，18 条无法解析 |
| danmaifu clash-20261123.yaml | ✅ | 44 条新增，文件内共 1240 条 |
| mehrtat vless-collector sub.txt | ✅ | 60 条新增 |
| mfuu FreeProxies sub | ✅ | 32 条新增，65 条无法解析 |
| mfuu FreeProxies sub.yaml | ✅ | 0 条新增，文件内共 123 条 |
| clashv2ray-hub v2ray.txt | ❌ 下载失败（返回空文件） | 0 |
| free18 v.txt | ✅ | 147 条新增，181 条无法解析 |
| free18 c.yaml | ✅ | 43 条新增，文件内共 423 条 |
| Au1rxx free-vpn-subscriptions v2ray-base64.txt | ✅ | 367 条新增 |
| Au1rxx free-vpn-subscriptions clash.yaml | ✅ | 0 条新增，文件内共 1751 条 |
| MatinGhanbari v2ray-configs all_sub.txt | ✅ | 3426 条新增，28 条无法解析 |
| 10Dream sub-mod mix.txt | ✅ | 15695 条新增，5449 条无法解析 |
| v2raydog 20261123.txt | ✅ | 2 条新增 |

说明：多个源来自同一上游节点池（如 free18 的 raw 与 jsdelivr 镜像内容相同、danmaifu 与其他源高度重合），后解析的源新增为 0 是去重后的正常结果。

## 延迟分布（可用节点）

- 最快：1421 ms；中位数（保留的 150 个）：1858 ms；中位数（全部 561 个可用节点）：2527 ms；最慢（保留的）：2086 ms
- 按协议：{'ss': 55, 'trojan': 95}

## 最快的 10 个节点

| # | 名称 | 协议 | 服务器 | 延迟 |
|---|---|---|---|---|
| 1 | @DeltaKroneckerGithub | 1421ms | ss | 49.142.200.31:28017 | 1421 ms |
| 2 | @DeltaKroneckerGithub | 1534ms | ss | 172.67.70.92:443 | 1534 ms |
| 3 | @DeltaKroneckerGithub | 1600ms | ss | 104.18.43.174:443 | 1600 ms |
| 4 | @DeltaKroneckerGithub | 1624ms | trojan | ja262.magiclampcloud.cn:59443 | 1624 ms |
| 5 | @DeltaKroneckerGithub | 1628ms | ss | 188.114.99.137:443 | 1628 ms |
| 6 | @DeltaKroneckerGithub | 1634ms | ss | 188.114.99.137:2053 | 1634 ms |
| 7 | @DeltaKroneckerGithub | 1636ms | ss | 104.18.41.190:443 | 1636 ms |
| 8 | @DeltaKroneckerGithub | 1657ms | trojan | ja262.magiclampcloud.cn:59443 | 1657 ms |
| 9 | @DeltaKroneckerGithub | 1667ms | ss | 185.188.104.10:443 | 1667 ms |
| 10 | @DeltaKroneckerGithub | 1667ms | ss | 172.66.42.200:2083 | 1667 ms |

## 未纳入的节点

- `06_clashv2rayhub`（clashv2ray-hub/v2rayfree）下载返回空文件，两次重试均为 0 字节；
- 邮件第 14 个链接仅显示为 https://nodesub.v2raydog（截断），无法补全，未纳入；
- `05_mfuu_yaml` 源文件第 83 行等 2 行 YAML 格式损坏，改按逐行解析，其余 121 行均与已解析节点重复，未新增节点；
- hysteria v1、http、ssr、anytls 类型节点不在本次订阅口径内，未测试；
- 339 个节点因配置无效被排除（控制字符 125、未知 ss 加密方式 150、无效密钥 49、空密码 14、无效服务器 1）；
- 其余节点在 5 秒内无响应或握手失败。

## 输出文件

- `sub.txt`：base64 编码的节点链接列表（解码后每行一个节点链接，节点名带延迟）；
- `clash.yaml`：mihomo/Clash 配置，含全部可用节点、PROXY 手动选择组和 AUTO 自动测速组，规则 MATCH 走 PROXY；
- 免费节点随时可能失效，延迟为测试当时实测，仅供参考。
