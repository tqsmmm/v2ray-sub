# v2ray-sub

Daily tested free V2Ray / Clash subscription. Every day the free node lists
mailed by Grok are downloaded, de-duplicated and tested one by one with
mihomo (Clash Meta) against `http://www.gstatic.com/generate_204`. Only
nodes that actually connect are kept, sorted by measured delay, fastest 150.

## Subscription URLs (stable, updated daily)

- Generic subscription (base64 node links):
  `https://raw.githubusercontent.com/tqsmmm/v2ray-sub/main/sub.txt`
- Clash / mihomo config:
  `https://raw.githubusercontent.com/tqsmmm/v2ray-sub/main/clash.yaml`

## Files

- `sub.txt` — base64 list of node links, each named with its measured delay
- `clash.yaml` — mihomo config with the same nodes (`PROXY` select group,
  `AUTO` url-test group, `MATCH,PROXY`)
- `report.md` — per-source counts, latency distribution, top 10, failed sources

## Caveats

- Free nodes decay fast; delays are a snapshot from test time, some nodes
  may already be dead when you use them.
- Hysteria2 / TUIC nodes (QUIC/UDP) cannot be tested on the current test host
  (UDP egress is blocked), so they are excluded — not proven dead.
- Updated daily around 17:00 CST; the same files are overwritten in place,
  so the URLs never change.
