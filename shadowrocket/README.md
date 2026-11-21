# Shadowrocket v10 — Gemini 地区限制修复

## 改了什么

相对 `shadowrocket_v9_68fe.conf`：

1. **防 QUIC 泄漏**：`udp-policy-not-supported-behaviour = REJECT`  
   Google/Gemini 大量走 HTTP/3。节点不支持 UDP 时若 UDP 直连，真实国内 IP 会暴露，直接弹 *isn't available in this country*。
2. **AI 出口改固定**：`AI` 从 `url-test` 改为 `select`，默认钉自建美区，避免自动换 IP 触发风控。
3. **补全 Gemini / Google AI 域名**，并把 `google.com` / `googleapis.com` / `gstatic.com` 等钉到 `AI`（美国），避免漏到直连或非美区。

## 小火箭怎么用

1. 把 `shadowrocket_v10_gemini.conf` 传到手机，用 Shadowrocket **打开/导入**。
2. **配置 → 选中该配置 → 启用**。
3. 首页 **全局路由 = 配置**（不要用「代理」或「直连」）。
4. 打开策略组 **AI**，手动选 **Vmiss-443** 或 **Zoro-VLESS**（自建美区），不要用订阅里脏的美国 IP。
5. 确认节点开启 **UDP 转发**（Reality / VLESS / Hy2 一般可以）。
6. 强杀 Gemini App → 重新打开；用 Safari 打开 `https://gemini.google.com` 试一次。

## 若仍弹地区不可用

按概率排查：

1. Safari 打开 `https://ipinfo.io`，确认是美国（或至少非 CN）。
2. Google 账号若是中国区注册/中国付款档案，App 仍可能拦——换支持地区账号，或只用网页版试。
3. 订阅美国节点 IP 被标记时，只保留自建 Reality。
4. iOS「本地网络 / VPN」权限正常；小火箭连上且隧道图标在。

## 文件

| 文件 | 说明 |
|------|------|
| `shadowrocket_v10_gemini.conf` | 可导入的修复版 |
| `shadowrocket_v9_68fe.conf.bak` | 你上传的原版备份 |
