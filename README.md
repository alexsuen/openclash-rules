# openclash-rules
# OpenClash 自定义分流规则集 (Rule-Providers)

本项目用于托管个人 OpenClash 模块化分流规则集。通过 GitHub 托管纯域名清单，实现多设备（主路由、便携路由等）规则自动同步，主配置文件无需频繁重启与修改。
配套使用的是我(https://github.com/alexsuen/openwrt-openclash-hub)  2026最新版yacd去广告版.yaml

---

## 规则集列表与说明

| 文件名 | 规则集名称 | 目标策略组 | 核心包含内容说明 |
| :--- | :--- | :--- | :--- |
| **DIRECT** | `direct.yaml` | 全球直连白名单：系统更新、下载 CDN、Wi-Fi Calling、PayPal中国、TikTok卖家后台 | `🎯 全球直连` | [直链](https://cdn.jsdelivr.net/gh/alexsuen/openclash-rules@main/direct.yaml) |
| **US-ONLY** | `us-only.yaml` | 纯美区业务：Google Voice、电话卡官网、Copilot 认证、Bing 网关 | `🇺🇸 美国节点` | [直链](https://cdn.jsdelivr.net/gh/alexsuen/openclash-rules@main/us-only.yaml) |
| **BANK-PH** | `bank-ph.yaml` | 菲律宾金融专线：GCash 电子钱包与 Mynt 官方 API（防异地风控） | `🇵🇭 菲律宾节点` | [直链](https://cdn.jsdelivr.net/gh/alexsuen/openclash-rules@main/bank-ph.yaml) |
| **FINANCE-GLOBAL** | `finance-global.yaml` | 国际金融与支付：PayPal 国际版全链路、Wise 官方接口与转账网关 | `🏦 金融银行` | [直链](https://cdn.jsdelivr.net/gh/alexsuen/openclash-rules@main/finance-global.yaml) |
| **SHOPEE** | `shopee.yaml` | 虾皮电商全家桶：Shopee 官方各站点（PH / MY / SG 等）及卖家后台 | `🟠 虾皮电商` | [直链](https://cdn.jsdelivr.net/gh/alexsuen/openclash-rules@main/shopee.yaml) |
| **AMAZON** | `amazon.yaml` | 亚马逊运营中心：Amazon 商城、Seller Central 卖家中心及后台媒体资源 | `📦 Amazon` | [直链](https://cdn.jsdelivr.net/gh/alexsuen/openclash-rules@main/amazon.yaml) |
| **GAMES** | `games.yaml` | Steam 游戏平台：商店、社区、好友网络加速（解决 101/105/118 访问异常） | `🎮 Steam` | [直链](https://cdn.jsdelivr.net/gh/alexsuen/openclash-rules@main/games.yaml) |
| **MY-MEDIA** | `my-media.yaml` | 海外特化影音：爱壹帆 (IYF) 影视鉴权与切片 CDN 调度 | `🇸🇬 新加坡节点` | [直链](https://cdn.jsdelivr.net/gh/alexsuen/openclash-rules@main/my-media.yaml) |
| **ASIA** | `asia.yaml` | 亚洲区域加速源：Google APK CDN、Docker Hub 镜像、AMD 驱动下载等 | `🌏 亚洲地区` | [直链](https://cdn.jsdelivr.net/gh/alexsuen/openclash-rules@main/asia.yaml) |
| **MICROSOFT** | `microsoft.yaml` | 微软办公套件：OneDrive 个人版（走代理防阻断）、Office 365 认证与登录 | `Ⓜ️ 微软服务` | [直链](https://cdn.jsdelivr.net/gh/alexsuen/openclash-rules@main/microsoft.yaml) |
| **APPLE** | `apple.yaml` | 苹果核心业务：iCloud 同步、苹果官方账户服务及基础定位体系 | `🍎 苹果服务` | [直链](https://cdn.jsdelivr.net/gh/alexsuen/openclash-rules@main/apple.yaml) |

---

## 维护规范与注意事项

1. **规则语法标准**：
   * 所有文件均为纯域名规则集，顶格声明 `payload:`。
   * 在本地主配置中，将以下 **规则声明** 与 **挂载规则** 放入对应区域即可（必须使用 `behavior: classical`）：
   * 下方规则缩进 2 个空格，严禁携带策略组后缀（如 `,DIRECT` 或 `,🇺🇸 美国节点`）。
2. **底层协议与端口分离**：
   * 本规则集仅管理域名流量。
   * 特殊底层逻辑（如 Wi-Fi Calling 的 `UDP 500/4500` 端口、APNs 推送的 `TCP 5223` 端口、淘宝系 `UDP 443` 拦截）直接在本地主 YAML 的 `rules` 顶部生效，不放入本仓库。
