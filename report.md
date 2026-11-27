# 免费订阅节点测试报告 — 2026-11-27 批次

测试时间：2026-11-27（北京时间）。订阅源为 2026-11-27 Grok 自动化邮件中的链接（主题称 30 个链接，正文实际只列出 14 条，其中 13 条完整可下载，第 14 条截断无法补全）。
本次为家用代理测试：每个节点经家用代理拨号，口径为“在家宽下可用”。

## 方法

- 工具：mihomo v1.19.34（Clash Meta），逐个节点调用外部控制 API 做延迟测试；
- 测试目标：`http://www.gstatic.com/generate_204`，单个节点超时 5 秒；
- 测试中只请求 generate_204，不经过节点发送任何用户数据或凭证；
- 去重口径：(协议, 服务器, 端口, uuid/密码) 相同算同一个节点；
- 测试方式：家用代理测试——每个节点经 dialer-proxy（home-proxy）拨号，即本地转发器 → Tailscale 隧道 → NAS 上的家用代理，出口为家宽网络；口径为“在家宽下可用”，即节点必须从家宽网络连通才算可用；
- 两轮逐个测试：第一轮逐个测试复核出 47 个可用；对第一轮失败的 4805 个节点又单独复测一轮，新增 17 个可用；本报告以两轮逐个测试结果为准。
- 限制：本机禁止 UDP 出站（实测 UDP DNS 查询被拒绝），因此 hysteria2 / tuic（走 QUIC/UDP）无法在本机验证，本批 79 个 hysteria2 节点均未计入可用——不是证实已死，而是无法测试；如需用 hysteria2，请在支持 UDP 的客户端上自行测速。

## 总览

- 解析出唯一节点：**4856** 个（13 个源，去重后）
- 进入测试：**4852** 个（4 个因配置无效被排除，mihomo 无法加载）
- 实测可用：**64** 个（1.3%），其中第一轮 47 个、复测新增 17 个
- 输出上限 150 个，本批可用 64 个，全部保留，按延迟从低到高排序

## 各源解析情况

| 来源 | 下载 | 新增节点数 |
|---|---|---|
| haiwanai free-nodes sub.yaml | ✅ | 160 条新增，文件内共 160 条 |
| haiwanai free-nodes sub.txt | ✅ | 0 条新增 |
| danmaifu mianfeijiedian v2ray-20261127.txt | ✅ | 822 条新增，36 条无法解析 |
| danmaifu mianfeijiedian clash-20261127.yaml | ✅ | 51 条新增，文件内共 1495 条 |
| free-nodes v2rayfree sub | ✅ | 25 条新增，2 条无法解析 |
| chenzhihan node-sub-zixf base64.txt | ✅ | 309 条新增，3 条无法解析 |
| mfuu FreeProxies sub | ✅ | 14 条新增，2 条无法解析 |
| mfuu FreeProxies sub.yaml | ✅ | 0 条新增，文件内共 194 条 |
| MatinGhanbari v2ray-configs all_sub.txt | ✅ | 3405 条新增，25 条无法解析 |
| MatinGhanbari v2ray-configs super-sub.txt | ✅ | 68 条新增，8 条无法解析 |
| Ruk1ng001 freeSub clash.yaml | ✅ | 2 条新增，文件内共 54 条 |
| Ruk1ng001 freeSub v2ray | ✅ | 0 条新增，15 条无法解析 |
| Ruk1ng001 freeSub singBox.json | ✅ | 0 条新增，文件内共 33 条 |

说明：多个源来自同一上游节点池（如 haiwanai 的 sub.yaml 与 sub.txt 内容相同、mfuu 的 sub.yaml 与前面源高度重合），后解析的源新增为 0 是去重后的正常结果。mfuu sub.yaml 因第 88 行 IPv6 名称未加引号导致整文件 YAML 解析失败，已改用逐行容错解析：194 行 flow 映射中 193 条可解析但全部为重复节点，1 行无法解析。

## 延迟分布（可用节点）

- 最快：1625 ms；中位数：3451 ms；最慢（保留的）：4988 ms
- 按协议：{'ss': 9, 'vless': 8, 'socks5': 45, 'trojan': 1, 'vmess': 1}

## 最快的 10 个节点

| # | 名称 | 协议 | 服务器 | 延迟 |
|---|---|---|---|---|
| 1 | 🇮🇹 意大利 08 | 1625ms | ss | 202.50.253.45:19999 | 1625 ms |
| 2 | 🇮🇹 意大利 07 | 1879ms | ss | 202.50.253.99:19999 | 1879 ms |
| 3 | 🇮🇹 意大利 11 | 1913ms | ss | 202.50.253.63:19999 | 1913 ms |
| 4 | 🇩🇪[www.v2nodes.com] ss-DE-1624... | 1953ms | ss | 47.254.167.157:443 | 1953 ms |
| 5 | 🇮🇹 意大利 09 | 2130ms | ss | 202.50.253.27:19999 | 2130 ms |
| 6 | 🇷🇺 俄罗斯 | RUS #1 | 2349ms | vless | 194.26.229.207:4100 | 2349 ms |
| 7 | 🇮🇹 意大利 06 | 2406ms | ss | 202.50.253.81:19999 | 2406 ms |
| 8 | 🇷🇺 俄罗斯 | RUS #2 | 2539ms | vless | 194.26.229.207:2200 | 2539 ms |
| 9 | 🇷🇺 俄罗斯 | RUS #4 | 2540ms | vless | 194.26.229.207:2200 | 2540 ms |
| 10 | 🇮🇩ID_4|522KB/s|R002-260618 [98ad7829bea3] | 2621ms | socks5 | 203.84.138.59:62000 | 2621 ms |

## 未纳入的节点

- 邮件第 14 个链接仅显示为 https://raw.githubus（截断），无法补全，未纳入；邮件主题称 30 个链接，但正文只列出 14 条，其余链接未在邮件中出现，未纳入；
- hysteria v1、http、ssr、anytls 类型节点不在本次订阅口径内，未测试；danmaifu clash.yaml 文件内 1495 条代理中有 609 条 http 类型被跳过；Ruk1ng001 clash.yaml 文件内 54 条代理中有 21 条 http/ssr 类型被跳过；Ruk1ng001 v2ray 文件 15 条均为 https:// 链接，不在口径内；Ruk1ng001 singBox.json 33 条 outbound 中 15 条 http 未纳入，其余 socks/shadowsocks 均为重复节点；
- 各源无法解析的行：danmaifu v2ray 36 条、MatinGhanbari all_sub 25 条、super-sub 8 条、chenzhihan base64 3 条、free-nodes 2 条、mfuu sub 2 条，合计 76 条；
- 其余节点在 5 秒内无响应或握手失败。

## 输出文件

- `sub.txt`：base64 编码的节点链接列表（解码后每行一个节点链接，节点名带延迟）；
- `clash.yaml`：mihomo/Clash 配置，含全部可用节点、PROXY 手动选择组和 AUTO 自动测速组，规则 MATCH 走 PROXY；
- 免费节点随时可能失效，延迟为测试当时实测，仅供参考。
