# 免费订阅节点测试报告 — 2026-11-26 批次

测试时间：2026-11-26（北京时间）。订阅源为 2026-11-26 Grok 自动化邮件中的 15 个链接（14 个可下载，其中 1 个返回空文件；1 个截断无法补全）。
本次为家用代理测试：每个节点经家用代理拨号，口径为“在家宽下可用”。

## 方法

- 工具：mihomo v1.19.34（Clash Meta），逐个节点调用外部控制 API 做延迟测试；
- 测试目标：`http://www.gstatic.com/generate_204`，单个节点超时 5 秒；
- 测试中只请求 generate_204，不经过节点发送任何用户数据或凭证；
- 去重口径：(协议, 服务器, 端口, uuid/密码) 相同算同一个节点；
- 测试方式：家用代理测试——每个节点经 dialer-proxy（home-proxy）拨号，即本地转发器 → Tailscale 隧道 → NAS 上的家用代理，出口为家宽网络；口径为“在家宽下可用”，即节点必须从家宽网络连通才算可用；
- 两轮逐个测试：第一轮逐个测试复核出 16 个可用；对第一轮失败的 722 个节点又单独复测一轮，新增 1 个可用；本报告以两轮逐个测试结果为准。
- 限制：本机禁止 UDP 出站（实测 UDP DNS 查询被拒绝），因此 hysteria2 / tuic（走 QUIC/UDP）无法在本机验证，本批 9 个 hysteria2 节点均未计入可用——不是证实已死，而是无法测试；如需用 hysteria2，请在支持 UDP 的客户端上自行测速。

## 总览

- 解析出唯一节点：**738** 个（14 个源，去重后）
- 进入测试：**738** 个（0 个因配置无效被排除，mihomo 无法加载）
- 实测可用：**17** 个（2.3%），其中第一轮 16 个、复测新增 1 个
- 输出上限 150 个，本批可用 17 个，全部保留，按延迟从低到高排序

## 各源解析情况

| 来源 | 下载 | 新增节点数 |
|---|---|---|
| clashv2ray-hub v2rayfree v2ray.txt | ❌ 下载失败（返回空文件） | 0 |
| shaoyouvip free all.yaml | ✅ | 13 条新增，文件内共 17 条 |
| shaoyouvip free base64.txt | ✅ | 0 条新增，1 条无法解析 |
| haiwanai free-nodes sub.yaml | ✅ | 120 条新增，文件内共 124 条 |
| haiwanai free-nodes sub.txt | ✅ | 0 条新增 |
| free-nodes v2rayfree sub | ✅ | 5 条新增 |
| mfuu FreeProxies sub.yaml | ✅ | 25 条新增，文件内共 109 条 |
| Ruk1ng001 freeSub clash.yaml | ✅ | 9 条新增，文件内共 53 条 |
| Ruk1ng001 freeSub v2ray | ✅ | 0 条新增，17 条无法解析 |
| Ruk1ng001 freeSub singBox.json | ✅ | 0 条新增，文件内共 28 条 |
| 0xRadikal Free-v2ray-Configs verified/configs_base64.txt | ✅ | 523 条新增，5 条无法解析 |
| mehrtat vless-collector sub.txt | ✅ | 21 条新增 |
| nodefree 20261126.yaml | ✅ | 21 条新增，文件内共 21 条 |
| v2rayshare 20261126.txt | ✅ | 1 条新增 |

说明：多个源来自同一上游节点池（如 haiwanai 的 sub.yaml 与 sub.txt 内容相同、shaoyouvip 的 base64.txt 与 all.yaml / free-nodes 的内容高度重合），后解析的源新增为 0 是去重后的正常结果。

## 延迟分布（可用节点）

- 最快：1679 ms；中位数：3182 ms；最慢（保留的）：4780 ms
- 按协议：{'vmess': 4, 'vless': 9, 'socks5': 4}

## 最快的 10 个节点

| # | 名称 | 协议 | 服务器 | 延迟 |
|---|---|---|---|---|
| 1 | CN 🇨🇳 | @Raydikalx | 89044A | 1679ms | vmess | 120.48.133.162:10086 | 1679 ms |
| 2 | RU 🇷🇺 | @Raydikalx | 9E313F | 2454ms | vless | vps3.nemnogogo.com:443 | 2454 ms |
| 3 | 🌐 其他 01 | 2737ms | vmess | 172.64.145.93:443 | 2737 ms |
| 4 | 🌐 其他 06 | 2791ms | vless | 196.196.149.81:443 | 2791 ms |
| 5 | CA 🇨🇦 | @Raydikalx | C9F20E | 2838ms | vmess | guanwang.awsno.com:443 | 2838 ms |
| 6 | D🔴🇸🇬hos_dokng.com_731ac5ff | 2865ms | socks5 | 47.236.168.243:1080 | 2865 ms |
| 7 | 🇺🇸 美国 22 | 3079ms | vmess | 104.18.42.163:443 | 3079 ms |
| 8 | 🇹🇼 台湾 01 | 3082ms | vless | free.fugui.lol:47396 | 3082 ms |
| 9 | A🟢🇲🇽res_dokng.com_1aa34d5e | 3182ms | socks5 | 94.194.164.203:62000 | 3182 ms |
| 10 | D🔴🇺🇸hos_dokng.com_a6052a43 | 3306ms | socks5 | 66.253.2.69:62000 | 3306 ms |

## 未纳入的节点

- 邮件第 15 个链接仅显示为 https://nodesub.stairnode.com/2026/11/stair-2（截断），无法补全，未纳入；
- hysteria v1、http、ssr、anytls 类型节点不在本次订阅口径内，未测试；
- Ruk1ng001 的 v2ray 文件 17 条、singBox.json 28 条均为 http 类型，未纳入；
- shaoyouvip base64.txt 中 1 条 hysteria:// 链接不在口径内；
- 0xRadikal 文件开头的 5 行 #profile-* 注释不是节点；
- 本批无节点因配置无效被排除；
- 其余节点在 5 秒内无响应或握手失败。

## 输出文件

- `sub.txt`：base64 编码的节点链接列表（解码后每行一个节点链接，节点名带延迟）；
- `clash.yaml`：mihomo/Clash 配置，含全部可用节点、PROXY 手动选择组和 AUTO 自动测速组，规则 MATCH 走 PROXY；
- 免费节点随时可能失效，延迟为测试当时实测，仅供参考。
