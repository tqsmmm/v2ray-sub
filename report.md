# 免费订阅节点测试报告 — 2026-11-25 批次

测试时间：2026-11-25（北京时间）。订阅源为 2026-11-25 Grok 自动化邮件中的 16 个链接（15 个可下载，其中 1 个返回空文件；1 个截断无法补全）。
本次为家用代理测试：每个节点经家用代理拨号，口径为“在家宽下可用”。

## 方法

- 工具：mihomo v1.19.34（Clash Meta），逐个节点调用外部控制 API 做延迟测试；
- 测试目标：`http://www.gstatic.com/generate_204`，单个节点超时 5 秒；
- 测试中只请求 generate_204，不经过节点发送任何用户数据或凭证；
- 去重口径：(协议, 服务器, 端口, uuid/密码) 相同算同一个节点；
- 测试方式：家用代理测试——每个节点经 dialer-proxy（home-proxy）拨号，即本地转发器 → Tailscale 隧道 → NAS 上的家用代理，出口为家宽网络；口径为“在家宽下可用”，即节点必须从家宽网络连通才算可用；
- 两轮逐个测试：第一轮逐个测试复核出 108 个可用；对第一轮失败的 19845 个节点又单独复测一轮，新增 4 个可用；本报告以两轮逐个测试结果为准。
- 限制：本机禁止 UDP 出站（实测 UDP DNS 查询被拒绝），因此 hysteria2 / tuic（走 QUIC/UDP）无法在本机验证，本批 30 个 hysteria2 节点均未计入可用——不是证实已死，而是无法测试；如需用 hysteria2，请在支持 UDP 的客户端上自行测速。

## 总览

- 解析出唯一节点：**20067** 个（15 个源，去重后）
- 进入测试：**19953** 个（114 个因配置无效被排除，mihomo 无法加载）
- 实测可用：**112** 个（0.6%），其中第一轮 108 个、复测新增 4 个
- 输出上限 150 个，本批可用 112 个，全部保留，按延迟从低到高排序

## 各源解析情况

| 来源 | 下载 | 新增节点数 |
|---|---|---|
| clashv2ray-hub v2rayfree v2ray.txt | ❌ 下载失败（返回空文件） | 0 |
| free18 v2ray v.txt | ✅ | 272 条新增，50 条无法解析 |
| free18 v2ray c.yaml | ✅ | 42 条新增，文件内共 365 条 |
| mehrtat vless-collector sub.txt | ✅ | 61 条新增 |
| helmiau clashrules elsubs/all | ✅ | 19548 条新增，7621 条无法解析 |
| 0xRadikal Free-v2ray-Configs verified/configs.txt | ✅ | 6 条新增，2 条无法解析 |
| 0xRadikal Free-v2ray-Configs verified/clash.yaml | ✅ | 0 条新增，文件内共 997 条 |
| MatinGhanbari v2ray-configs super-sub.txt | ✅ | 1 条新增，6 条无法解析 |
| leidahub v2ray.txt | ✅ | 29 条新增，11 条无法解析 |
| leidahub clash.yaml | ✅ | 0 条新增，文件内共 497 条 |
| v2raydog 20261125.txt | ✅ | 0 条新增 |
| stairnode 20261125.yaml | ✅ | 0 条新增，文件内共 20 条 |
| clashfree v2ray.txt | ✅ | 16 条新增 |
| v2ssr.net 20261125 txt | ✅ | 78 条新增，68 条无法解析 |
| nodefree 20261125.txt | ✅ | 14 条新增 |

说明：多个源来自同一上游节点池（如 leidahub 的三个文件内容高度重合、zhulinghuanyu 与 0xRadikal 的 clash 文件与各自的 v2ray/base64 文件重复），后解析的源新增为 0 是去重后的正常结果。

## 延迟分布（可用节点）

- 最快：2136 ms；中位数：2807 ms；最慢（保留的）：4923 ms
- 按协议：{'ss': 14, 'trojan': 93, 'vless': 1, 'vmess': 4}

## 最快的 10 个节点

| # | 名称 | 协议 | 服务器 | 延迟 |
|---|---|---|---|---|
| 1 | 🇮🇹_意大利 (7) | 2136ms | ss | 202.50.253.81:19999 | 2136 ms |
| 2 | 🇮🇹_意大利 (8) | 2230ms | ss | 202.50.253.27:19999 | 2230 ms |
| 3 | 🇯🇵_日本 (11) | 2275ms | ss | 8.216.7.10:6666 | 2275 ms |
| 4 | trojan-1938650863 | 2352ms | trojan | 42.51.25.69:59443 | 2352 ms |
| 5 | trojan-1929356561 | 2355ms | trojan | tyy129.magiclampcloud.com:59443 | 2355 ms |
| 6 | trojan-1943700986 | 2371ms | trojan | ja304.magiclampcloud.cn:59443 | 2371 ms |
| 7 | trojan-1929357974 | 2377ms | trojan | ja262.magiclampcloud.cn:59443 | 2377 ms |
| 8 | trojan-1929354458 | 2424ms | trojan | ja262.magiclampcloud.cn:59443 | 2424 ms |
| 9 | trojan-1918521094 | 2448ms | trojan | ja262.magiclampcloud.cn:59443 | 2448 ms |
| 10 | trojan-1945995987 | 2451ms | trojan | ja304.magiclampcloud.cn:59443 | 2451 ms |

## 未纳入的节点

- 邮件第 16 个链接仅显示为 https://raw.githubusercontent.（截断），无法补全，未纳入；
- hysteria v1、http、ssr、anytls 类型节点不在本次订阅口径内，未测试；
- 114 个节点因配置无效被排除（bad-server 2 个、empty-password 12 个、invalid-blake3-key 80 个、invalid-reality-key 12 个、invalid-reality-short-id 1 个、unknown-ss-cipher 5 个、unsupported-vless-flow 2 个，mihomo 无法加载）；
- 其余节点在 5 秒内无响应或握手失败。

## 输出文件

- `sub.txt`：base64 编码的节点链接列表（解码后每行一个节点链接，节点名带延迟）；
- `clash.yaml`：mihomo/Clash 配置，含全部可用节点、PROXY 手动选择组和 AUTO 自动测速组，规则 MATCH 走 PROXY；
- 免费节点随时可能失效，延迟为测试当时实测，仅供参考。
