# 🏨 酒店集团舆情情报综合工具箱

> 通用版 | 支持任意酒店集团复用 | 无硬编码 | 可配置

适用于华住会、锦江、亚朵、首旅如家、德胧、开元等**所有酒店集团**。

## 🚀 快速安装

```bash
# 克隆
git clone https://github.com/chaoliuzhu65-tech/hotel-intelligence-suite.git

# 复制到OpenClaw skills
cp -r hotel-intelligence-suite/ ~/workspace/agent/skills/

# 重启
openclaw gateway restart
```

## ⚙️ 品牌配置（使用前必读）

```javascript
{
  brand: "德胧集团",        // 品牌名
  brands: ["开元名都", "钛唐"],  // 子品牌
  competitors: ["华住会", "锦江"],  // 竞品
  feishu_user_id: "ou_xxx",  // 推送目标
}
```

## 📦 核心能力

| 模块 | 功能 |
|------|------|
| miaoda搜索 | 网页舆情采集 + AI摘要 |
| BettaFish | 30+平台深度舆情分析 |
| 视频监控 | 抖音/快手/B站/小红书 |
| 飞书卡片 | 精美日报/预警卡片 |
| AI风险分析 | 5Why根因 + 防控预案 |

## 🔍 触发词

舆情、情报、网情、监控、风险分析、抖音监控、酒店日报、行业预警

## 📤 输出示例

使用 `<text_tag>` + bullet list 的飞书精美卡片格式。

## 📄 License

MIT - 可自由复用给任何酒店集团

---

**作者**：晁留柱的助手（小柱）
**版本**：v3.0 通用版 | 2026-04-19
