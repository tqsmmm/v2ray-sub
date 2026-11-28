# 免费订阅节点测试报告 — 2026-11-28 批次

测试时间：2026-11-28（北京时间）。订阅源为 2026-11-28 Grok 自动化邮件中的链接（正文列出 14 条，其中 13 条完整可下载，第 14 条截断无法补全）。
本次为家用代理测试：每个节点经家用代理拨号，口径为“在家宽下可用”。

## 方法

- 工具：mihomo v1.19.34（Clash Meta），逐个节点调用外部控制 API 做延迟测试；
- 测试目标：`http://www.gstatic.com/generate_204`，单个节点超时 5 秒；
- 测试中只请求 generate_204，不经过节点发送任何用户数据或凭证；
- 去重口径：(协议, 服务器, 端口, uuid/密码) 相同算同一个节点；
- 测试方式：家用代理测试——每个节点经 dialer-proxy（home-proxy）拨号，即本地转发器 → Tailscale 隧道 → NAS 上的家用代理，出口为家宽网络；口径为“在家宽下可用”，即节点必须从家宽网络连通才算可用；
- 两轮逐个测试：第一轮逐个测试复核出 53 个可用；对第一轮失败的 2986 个节点又单独复测一轮，新增 13 个可用；本报告以两轮逐个测试结果为准。
- 限制：本机禁止 UDP 出站（实测 UDP DNS 查询被拒绝），因此 hysteria2 / tuic（走 QUIC/UDP）无法在本机验证，本批 106 个 hysteria2 节点均未计入可用——不是证实已死，而是无法测试；如需用 hysteria2，请在支持 UDP 的客户端上自行测速。

## 总览

- 解析出唯一节点：**3087** 个（13 个源，去重后）
- 进入测试：**3039** 个（48 个因配置无效被排除，mihomo 无法加载）
- 实测可用：**66** 个（2.2%），其中第一轮 53 个、复测新增 13 个
- 输出上限 150 个，本批可用 66 个，全部保留，按延迟从低到高排序

## 各源解析情况

| 来源 | 下载 | 新增节点数 |
|---|---|---|
| mfuu FreeProxies sub | ✅ | 53 条新增，2 条无法解析 |
| mfuu FreeProxies sub.yaml | ✅ | 0 条新增，文件内共 123 条 |
| danmaifu mianfeijiedian v2ray-20261128.txt | ✅ | 789 条新增，26 条无法解析 |
| danmaifu mianfeijiedian clash-20261128.yaml | ✅ | 52 条新增，文件内共 1219 条 |
| free-nodes v2rayfree sub | ✅ | 10 条新增 |
| clashv2ray-hub v2rayfree v2ray.txt | ❌ 下载失败（返回空文件） | 0 |
| free18 v2ray v.txt | ✅ | 196 条新增，7 条无法解析 |
| free18 v2ray c.yaml | ✅ | 0 条新增，文件内共 337 条 |
| Alirewa V2ray-Configs config.txt | ✅ | 1665 条新增，249 条无法解析 |
| 0xRadikal Free-v2ray-Configs top100.txt | ✅ | 5 条新增 |
| MatinGhanbari v2ray-configs super-sub.txt | ✅ | 170 条新增，7 条无法解析 |
| barry-far V2ray-config Sub1.txt | ✅ | 144 条新增，2 条无法解析 |
| nodesub v2raysub-20261128.yaml | ✅ | 3 条新增，文件内共 22 条 |

说明：多个源来自同一上游节点池（如 mfuu 的 sub.yaml 与 sub 内容相同、free18 的 c.yaml 与 v.txt 高度重合），后解析的源新增为 0 是去重后的正常结果。mfuu sub.yaml 因 YAML 解析失败，已改用逐行容错解析：123 行 flow 映射中 122 条可解析但全部为重复节点，1 行无法解析。

## 延迟分布（可用节点）

- 最快：2640 ms；中位数：3927 ms；最慢（保留的）：4924 ms
- 按协议：{'ss': 13, 'socks5': 49, 'vless': 1, 'vmess': 1, 'trojan': 2}

## 最快的 10 个节点

| # | 名称 | 协议 | 服务器 | 延迟 |
|---|---|---|---|---|
| 1 | 🇩🇪 德国 阿里云 | 2640ms | ss | 47.254.128.109:443 | 2640 ms |
| 2 | 🇮🇹IT意大利丨yoyapai.com\r | 2790ms | ss | 202.50.253.90:19999 | 2790 ms |
| 3 | 🇻🇳VN_3|426KB/s|R002-260618 [1ed94f8d82c9] | 2939ms | socks5 | 103.184.113.190:62000 | 2939 ms |
| 4 | 🇹🇭TH_13|574KB/s|R002-260618 [4d7f4c48ed29] | 3033ms | socks5 | 87.84.49.245:62000 | 3033 ms |
| 5 | 🇹🇭TH_12|344KB/s|R002-260618 [744dddb58be2] | 3072ms | socks5 | 104.234.70.82:42000 | 3072 ms |
| 6 | 🇹🇭TH_7|316KB/s|R002-260618 [875ea96a51cf] | 3099ms | socks5 | 82.47.152.151:42000 | 3099 ms |
| 7 | 🇳🇱NL荷兰丨yoyapai.com\r | 3196ms | ss | 202.50.253.63:19999 | 3196 ms |
| 8 | 🇹🇭TH_3|363KB/s|R002-260618 [849ebc43c563] | 3216ms | socks5 | 192.204.15.135:42000 | 3216 ms |
| 9 | 🇹🇭TH_11|571KB/s|R002-260618 [ad775af2aefa] | 3249ms | socks5 | 87.84.49.140:62000 | 3249 ms |
| 10 | ❓未知丨yoyapai.com\r | 3272ms | ss | 202.50.253.99:19999 | 3272 ms |

## 未纳入的节点

- 邮件第 14 个链接仅显示为 https://static.v2rayshare.net/2026/11/（截断），无法补全，未纳入；
- 第 6 个源 clashv2ray-hub v2rayfree v2ray.txt 下载后为空文件（重试一次仍为空），记为下载失败，未纳入；
- hysteria v1、http、ssr、anytls 类型节点不在本次订阅口径内，未测试；danmaifu clash.yaml 文件内 1219 条代理中有 602 条 http、2 条 ssr 被跳过；free18 c.yaml 文件内 337 条代理全部为重复节点；
- 各源无法解析的行：Alirewa config.txt 249 条、danmaifu v2ray 26 条、free18 v.txt 7 条、MatinGhanbari super-sub 7 条、mfuu sub 2 条、barry-far Sub1 2 条，合计 293 条；

## 输出文件

- `sub.txt`：base64 编码的节点链接列表（解码后每行一个节点链接，节点名带延迟）；
- `clash.yaml`：mihomo/Clash 配置，含全部可用节点、PROXY 手动选择组和 AUTO 自动测速组，规则 MATCH 走 PROXY；
- 免费节点随时可能失效，延迟为测试当时实测，仅供参考。
