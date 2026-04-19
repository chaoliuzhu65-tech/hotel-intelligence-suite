# 🏨 酒店集团舆情情报综合工具箱

> 通用版 | v3.1 | 支持任意酒店集团复用

适用于华住会、锦江、亚朵、首旅如家、德胧、开元等**所有酒店集团**。

## 🚀 快速安装

```bash
git clone https://github.com/chaoliuzhu65-tech/hotel-intelligence-suite.git
cp -r hotel-intelligence-suite/ ~/workspace/agent/skills/
openclaw gateway restart
```

## ⚙️ 品牌配置（使用前必读）

```javascript
{
  brand: "德胧集团",
  brands: ["开元名都", "钛唐", "曼居"],
  competitors: ["华住会", "锦江"],
  feishu_user_id: "ou_xxx",
  // 两层架构
  risk: { schedule: "0 */2 * * *" },
  ota: { schedule: "0 10 * * *", bitable_id: "xxx" }
}
```

## 🏗️ 两层架构

```
【舆情风险层】← 每2小时扫描 ← 黑猫/微博/抖音
        ↓ P0/P1
   飞书预警卡片 → 私信

【差评维度层】← 每日10点 ← 携程/美团/小红书
        ↓ 12维度分类
   飞书多维表格 → 周报统计
```

## 📦 核心能力

| 模块 | 功能 |
|------|------|
| miaoda搜索 | 网页舆情 + AI摘要 |
| BettaFish | 30+平台深度分析 |
| 视频监控 | 抖音/快手/B站/小红书 |
| 飞书卡片 | 日报/预警卡片 |
| AI风险分析 | 5Why + 防控预案 |
| 差评12维度 | 内部OTA管理 |

## ⚡ 随时可调整

告诉龙虾你想要什么调整：

```
「调低舆情扫描频率」
「增加竞品监控」
「切换推送目标」
「暂停舆情扫描」
「增加视频平台」
「调整差评阈值」
```

## 📄 License

MIT - 可自由复用给任何酒店集团

---

**作者**：晁留柱的助手（小柱）
**版本**：v3.1 两层架构版 | 2026-04-19
