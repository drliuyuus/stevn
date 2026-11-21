# Shadowrocket — Gemini 修复

## 用哪个

**请用 `shadowrocket_v11_gemini.conf`**（修了 v10 的 1002）。

| 版本 | 现象 |
|------|------|
| v9 | 地区不可用（域名不全 / 可能换 IP） |
| v10 | 1002 连不上（`AI=select` 不切换 + UDP REJECT 过严） |
| **v11** | `AI=fallback` + 去掉 UDP REJECT + 保留补全域名 |

## v11 要点

1. `AI` 用 **fallback**：自建美区优先，挂了自动切，避免整站 Google 1002  
2. **去掉** `udp-policy-not-supported-behaviour = REJECT`（Gemini iOS 对 QUIC 回落差）  
3. 请在节点上开 **UDP 转发**，让 QUIC 走代理  
4. 保留 Gemini/Google 域名钉美国 `AI`

## 小火箭怎么用

1. 导入并启用 `shadowrocket_v11_gemini.conf`（和 v9 同一 uploads 目录）  
2. 全局路由 = **配置**  
3. 确认自建节点（Vmiss / Zoro）测速能通，并开 **UDP 转发**  
4. 强杀 Gemini 再开  
5. Safari 打开 `https://ipinfo.io` 确认非 CN；再试 `https://gemini.google.com`

## 若还不行

- **仍 1002**：小火箭里看 `AI` 当前节点是否超时；先手动连 Vmiss-443 测连通  
- **又变地区不可用**：账号中国区可能性大；或节点 IP 被标，只留自建 Reality  
- 网页能开、App 不行：优先换支持地区 Google 账号

## 文件

| 文件 | 说明 |
|------|------|
| `shadowrocket_v11_gemini.conf` | **当前推荐** |
| `shadowrocket_v10_gemini.conf` | 已弃用（易 1002） |
| `shadowrocket_v9_68fe.conf.bak` | 原版备份 |
