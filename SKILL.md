---
name: hotel-intelligence-suite
description: |
  🏨 酒店集团舆情情报综合工具箱（通用版）
  
  适用于任何酒店集团、品牌、酒店的舆情监控、风险分析、竞品情报、AI防控预案生成。
  完全解耦，无硬编码，可配置化。
  
  触发词：舆情、情报、网情、监控、风险分析、抖音监控、酒店风险、竞品动态、行业预警、酒店日报
  
  三大核心：
  1. 外网信息采集（miaoda搜索主力 + BettaFish扩展 + 视频平台监控）
  2. 精美飞书卡片输出（可视化日报/预警）
  3. AI风险分析+防控预案（舆情驱动决策）
override-tools:
  - web_search
---

# 🏨 酒店集团舆情情报综合工具箱

> 通用版 | v3.0 | 支持任意酒店集团复用
> 适配：华住会/锦江/亚朵/首旅如家/德胧/开元/及其他酒店集团
> 无硬编码 | 可配置 | 可开源

---

## ⚙️ 配置（使用前必读）

### 品牌配置化

所有品牌相关配置通过 `BRAND_CONFIG` 变量传入，**无需修改代码**：

```javascript
// 示例配置（德胧版）
{
  brand: "德胧集团",
  brands: ["开元名都", "钛唐", "开元酒店"],
  competitors: ["华住会", "锦江集团", "亚朵", "首旅如家"],
  feishu_user_id: "ou_xxxxxxxx",  // 日报推送目标
}

// 示例配置（华住会版）
{
  brand: "华住会",
  brands: ["汉庭", "全季", "桔子", "海友", "漫心", "美居"],
  competitors: ["锦江集团", "亚朵", "首旅如家", "德胧"],
  feishu_user_id: "ou_yyyyyyyy",
}
```

### 关键词配置

| 类型 | 用途 | 示例 |
|------|------|------|
| `brand_keywords` | 品牌词 | 德胧/开元名都/钛唐 |
| `competitor_keywords` | 竞品词 | 华住/锦江/亚朵 |
| `event_keywords` | 事件类型 | 隐私泄露/卫生投诉/强制好评 |
| `video_keywords` | 视频平台 | 抖音+酒店名/快手+投诉 |

---

## 🏗️ 系统架构

```
酒店舆情情报综合工具箱
│
├── 数据源层
│   ├── miaoda-web-search（主力搜索）
│   │   └── 关键词搜索 + AI摘要
│   ├── BettaFish 扩展（深度舆情）
│   │   └── 30+平台结构化采集
│   └── 视频平台专项（抖音/快手/B站/小红书）
│       └── 视频舆情 + 含品牌关键字
│
├── 分析层
│   ├── 舆情分类（投诉/安全/服务/运营/AI）
│   ├── 风险评级（🔴高危/🟠中危/🟡低危）
│   ├── 5Why根因分析
│   └── 防控预案生成
│
├── 输出层
│   ├── 飞书精美卡片（日报/突发/预警）
│   └── 结构化数据
│
└── 自动化层
    ├── Cron: 每日日报（可配置时间）
    └── Cron: 突发预警（可配置间隔）
```

---

## 🚀 快速使用

### 舆情采集（传入品牌配置）

```bash
# 通用命令格式
miaoda-studio-cli search-summary --query "{brand} {brand_keyword} 投诉 2026" \
  --instruction "提取投诉内容、媒体来源、传播范围、情感倾向"

# 示例（德胧）
miaoda-studio-cli search-summary --query "开元名都 德胧 投诉 2026" \
  --instruction "提取投诉内容、酒店名称、处理结果"

# 示例（华住会）
miaoda-studio-cli search-summary --query "桔子水晶 华住 隐私泄露 2026" \
  --instruction "提取投诉内容、媒体曝光、官方回应"
```

### 竞品动态采集

```bash
miaoda-studio-cli search-summary --query "华住 AI动态定价 2026" \
  --instruction "提取AI覆盖数据、效果指标、竞品对比"

miaoda-studio-cli search-summary --query "锦江 锦鲲 AI 酒店 2026" \
  --instruction "提取AI激活率、覆盖门店数、效果数据"
```

### 视频平台舆情

```bash
miaoda-studio-cli search-summary --query "抖音 {酒店品牌} 投诉 差评" \
  --instruction "重点关注视频内容，提炼视频核心观点、播放量估算、评论情绪"

# 示例
miaoda-studio-cli search-summary --query "抖音 开元名都 酒店 投诉" \
  --instruction "重点关注视频内容，提取博主观点、评论情绪"
```

---

## 🛠️ 工具一：miaoda-web-search（主力）

### 简介
妙搭内置网页搜索，通过 `miaoda-studio-cli search-summary` 调用。

### 命令格式
```
miaoda-studio-cli search-summary --query "关键词" [--instruction "AI指令"] [--output text|json]
```

### 通用搜索模板

```bash
# 品牌舆情
miaoda-studio-cli search-summary --query "{品牌名} {事件关键词} 2026"

# 竞品对比
miaoda-studio-cli search-summary --query "{竞品名} {AI/运营/服务} 2026"

# 行业趋势
miaoda-studio-cli search-summary --query "酒店行业 {趋势关键词} 2026"

# 视频舆情
miaoda-studio-cli search-summary --query "抖音 {品牌名} {投诉/曝光} {年份}"
```

---

## 🛠️ 工具二：BettaFish 微舆系统

### 简介
GitHub最强开源舆情分析系统（666ghj/BettaFish），支持30+平台。

### 仓库信息
```
GitHub: https://github.com/666ghj/BettaFish
Star: 17k+
语言: Python3
```

### 核心能力

| 能力 | 支持平台 |
|------|----------|
| 舆情采集 | 微博/小红书/抖音/快手/B站/知乎/公众号等30+ |
| 情感分析 | NLP + LLM 95%+准确率 |
| 视频解析 | 多模态突破，深度解析短视频 |
| 风险评级 | 自动高/中/低危分级 |
| 报告生成 | 专业舆情分析报告 |

### 安装步骤

```bash
# 方式1：pip
pip install bettafish

# 方式2：源码（SSH克隆）
git clone git@github.com:666ghj/BettaFish.git /tmp/BettaFish
cd /tmp/BettaFish && pip install -r requirements.txt

# 方式3：Docker（推荐）
docker pull bettafish/bettafish:latest
```

### 使用示例

```bash
# 品牌舆情分析
bettafish analyze --keyword "{品牌名}" --platforms weibo,xiaohongshu,douyin

# 竞品对比
bettafish compare --brands {品牌A},{品牌B} --metric reputation

# 风险报告
bettafish report --type risk --output json

# 视频专项
bettafish analyze --keyword "{品牌}" --platforms douyin,kuaishou,bilibili --video-only
```

---

## 🛠️ 工具三：视频平台专项监控

### 支持平台

| 平台 | 重点监控内容 |
|------|-------------|
| 抖音 | 短视频投诉、曝光视频、博主评测 |
| 快手 | 老铁文化、区域传播 |
| B站 | UP主深度测评、行业揭秘 |
| 小红书 | 素人笔记、避坑指南 |
| 微博 | 热搜话题、媒体跟进 |
| 知乎 | 行业分析、深度问答 |

### 视频舆情分级

| 级别 | 特征 | 响应时间 |
|------|------|----------|
| 🔴 P0 | 播放>10万、负面评论>1000 | 30分钟 |
| 🟠 P1 | 播放>1万、负面评论>100 | 2小时 |
| 🟡 P2 | 播放>1000、有扩散趋势 | 4小时 |
| 🔵 P3 | 普通投诉视频 | 24小时 |

### 视频舆情关键词

```bash
# 通用模板
"抖音 {品牌名} {投诉/曝光/差评/卫生/安全}"
"快手 {品牌名} {酒店} {投诉/事件}"
"B站 {品牌名} {酒店评测/行业揭秘}"
"小红书 {品牌名} {体验/避坑/投诉}"
```

---

## 🛠️ 工具四：飞书精美卡片生成器

### 飞书Markdown语法要点

| 要素 | 语法 | 注意 |
|------|------|------|
| 标题 | `**加粗文字**` | ❌ 不支持 `# ## ###` |
| 标签 | `<text_tag color='red'>` | red/orange/yellow/green/blue/purple |
| 链接 | `[文本](url)` | - |
| 分割线 | `---` | - |
| 列表 | `• 项目` | bullet list最稳定 |
| 彩色文本 | `<font color='red'>` | - |

### 日报卡片模板（通用版）

```json
{
  "config": {"wide_screen_mode": true},
  "header": {
    "template": "red",
    "title": {"content": "🏨 酒店舆情日报 | {日期}", "tag": "plain_text"}
  },
  "elements": [
    {"tag": "markdown", "content": "**<text_tag color='red'>🔴 超级热点</text_tag> {事件标题}**\n\n{事件摘要}\n\n**官方回应**：{回应内容}"},
    {"tag": "markdown", "content": "**<text_tag color='orange'>🟠 投诉数据</text_tag>**\n\n{投诉列表}"},
    {"tag": "markdown", "content": "**<text_tag color='green'>🟡 竞品动态</text_tag>**\n\n{竞品信息}"},
    {"tag": "hr"},
    {"tag": "markdown", "content": "**<text_tag color='blue'>📎 原文链接</text_tag>**\n{链接列表}"},
    {"tag": "note", "content": "🦞 酒店舆情情报工具箱 | {品牌名} | {时间}", "quoteless": false}
  ]
}
```

### 预警卡片模板

```json
{
  "config": {"wide_screen_mode": true},
  "header": {
    "template": "orange",
    "title": {"content": "🚨 突发舆情预警 | {日期}", "tag": "plain_text"}
  },
  "elements": [
    {"tag": "markdown", "content": "**<text_tag color='red'>🔴 风险评级：{高危/中危/低危}</text_tag>**"},
    {"tag": "markdown", "content": "**事件**：{事件标题}\n\n**平台**：{平台}\n**传播**：{传播范围}"}
  ]
}
```

### 风险分析卡片模板

```json
{
  "config": {"wide_screen_mode": true},
  "header": {
    "template": "purple",
    "title": {"content": "📊 AI风险分析报告 | {日期}", "tag": "plain_text"}
  },
  "elements": [
    {"tag": "markdown", "content": "**<text_tag color='red'>🔴 风险评级</text_tag>** {高危/中危/低危}"},
    {"tag": "markdown", "content": "**<text_tag color='orange'>⚠️ 根因分析（5Why）</text_tag>**\n{5Why分析内容}"},
    {"tag": "markdown", "content": "**<text_tag color='green'>✅ 防控预案</text_tag>**\n• 预防措施：{内容}\n• 监控指标：{内容}\n• 应急预案：{内容}"}
  ]
}
```

---

## 🛠️ 工具五：AI风险分析与防控预案

### 分析流程

```
舆情数据输入
    ↓
① 舆情分类
    ├─ 投诉类（服务/卫生/退改）
    ├─ 安全类（隐私/消防/事故）
    ├─ 服务类（态度/效率/承诺）
    ├─ 运营类（加盟/关店/业绩）
    └─ AI类（定价/隐私/自动化）
    ↓
② 风险评级
    ├─ 🔴 高危（媒体>5家/投诉>100）
    ├─ 🟠 中危（媒体>2家/投诉>30）
    └─ 🟡 低危（个别投诉）
    ↓
③ 5Why根因分析
    ↓
④ 防控预案生成
    ├─ 预防措施（可执行）
    ├─ 监控指标（可量化）
    ├─ 应急预案（触发+处置）
    └─ 规避建议
    ↓
⑤ 飞书卡片输出
```

### 通用风险分析Prompt

````
请分析以下舆情事件，生成风险报告：

## 舆情内容
{粘贴舆情内容}

## 品牌信息
- 品牌：{品牌名}
- 涉事门店：{门店名}
- 事件类型：{类型}

## 分析要求
1. 风险评级（🔴高危/🟠中危/🟡低危）
2. 风险归因（5Why法）
3. 防控预案：
   - 预防措施（具体可执行）
   - 监控指标（可量化阈值）
   - 应急预案（触发条件+处置流程）
4. 同类舆情规避建议

## 输出格式
飞书Markdown格式
````

### 防控预案模板（通用）

| 类别 | 预防措施 | 监控指标 | 应急预案 |
|------|----------|----------|----------|
| 隐私泄露 | 回访需授权、话术标准化 | 投诉>5/月 | 立即停回访+合规培训 |
| 卫生投诉 | SOP增加抽查频次 | 差评率>2% | 深度清洁+公开道歉 |
| 强制好评 | 禁止强制、投诉零容忍 | 投诉>3/月 | 涉事员工追责+品牌澄清 |
| 价格欺诈 | 定价透明、差价可退 | 投诉>5/月 | 差价退款+价格审计 |
| 安全事故 | 定期消防/安全检查 | 隐患>0 | 立即停业+政府报备 |

---

## 📋 通用关键词库

### 企业监控模板

| 类型 | 关键词组合 |
|------|------------|
| 品牌词 | {品牌A}/{品牌B}/{品牌C} |
| 投诉词 | 投诉、差评、卫生、隐私、泄露 |
| 安全词 | 安全、消防、隐患、事故 |
| 服务词 | 态度、强制、虚假、服务差 |

### 视频平台关键词模板

```bash
"抖音 {品牌名} {投诉/曝光/差评}"
"快手 {品牌名} {酒店} {投诉/事件}"
"B站 {品牌名} {酒店评测/行业揭秘}"
"小红书 {品牌名} {体验/避坑/投诉}"
```

### 事件类型关键词

| 类型 | 关键词组合 |
|------|------------|
| 隐私安全 | 隐私泄露、信息泄露、摄像头、入住记录 |
| 服务质量 | 卫生差、前台态度、虚假宣传 |
| 会员权益 | 积分清零、会员降级、权益缩水 |
| 价格问题 | 临时涨价、差价、取消扣款 |
| 安全事故 | 消防隐患、安全事故、食物中毒 |

---

## ⏰ 自动化配置

### Cron模板（通用）

```javascript
// 每日舆情日报
{
  "name": "{品牌}舆情日报",
  "schedule": {"kind": "cron", "expr": "0 9 * * *", "tz": "Asia/Shanghai"},
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "执行{品牌}舆情日报采集：\n1. miaoda搜索今日舆情（{品牌关键词}）\n2. 视频平台专项搜索（抖音/快手/B站）\n3. 竞品动态采集\n4. AI风险分析（高危舆情生成防控预案）\n5. 生成飞书精美卡片\n6. 发送私信到 {feishu_user_id}"
  }
}

// 突发舆情预警
{
  "name": "{品牌}突发舆情预警",
  "schedule": {"kind": "cron", "expr": "0 */2 * * *", "tz": "Asia/Shanghai"},
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "执行{品牌}突发舆情检查：\n1. 搜索最新视频平台舆情（含{品牌}关键字）\n2. 检查P0/P1级风险\n3. 如有突发高危舆情，立即生成预警卡片发送私信"
  }
}
```

---

## 🔧 品牌配置示例

### 德胧集团配置

```javascript
{
  brand: "德胧集团",
  short_name: "德胧",
  brands: ["开元名都", "钛唐", "开元酒店", "曼居"],
  competitors: ["华住会", "锦江集团", "亚朵", "首旅如家"],
  keywords: {
    brand: ["德胧", "开元名都", "钛唐", "曼居"],
    event: ["隐私泄露", "卫生投诉", "强制好评", "关店"],
    video: ["开元名都投诉", "钛唐差评", "德胧酒店卫生"]
  },
  feishu_user_id: "ou_fc1e75d64fec6e10ce94a51adc6f6409",
  cron_daily: "0 9 * * *",
  cron_alert: "0 */2 * * *"
}
```

### 华住会配置

```javascript
{
  brand: "华住会",
  short_name: "华住",
  brands: ["汉庭", "全季", "桔子酒店", "海友", "漫心", "美居"],
  competitors: ["锦江集团", "亚朵", "首旅如家", "德胧"],
  keywords: {
    brand: ["华住", "汉庭", "全季", "桔子", "漫心"],
    event: ["隐私泄露", "卫生投诉", "强制好评", "金会员"],
    video: ["汉庭投诉", "全季卫生", "桔子酒店差评"]
  },
  feishu_user_id: "ou_xxxxxxxx",
  cron_daily: "0 8 * * *",
  cron_alert: "0 */1 * * *"
}
```

### 亚朵配置

```javascript
{
  brand: "亚朵",
  short_name: "亚朵",
  brands: ["亚朵", "Atour"],
  competitors: ["华住会", "锦江集团", "首旅如家", "德胧"],
  keywords: {
    brand: ["亚朵", "Atour"],
    event: ["服务", "卫生", "退改", "会员"],
    video: ["亚朵酒店体验", "亚朵投诉"]
  },
  feishu_user_id: "ou_yyyyyyyy",
  cron_daily: "0 9 * * *",
  cron_alert: "0 */3 * * *"
}
```

---

## 📦 安装指南

```bash
# 1. 克隆
git clone https://github.com/chaoliuzhu65-tech/hotel-intelligence-suite.git

# 2. 复制到OpenClaw skills目录
cp -r hotel-intelligence-suite/ ~/workspace/agent/skills/

# 3. 重启
openclaw gateway restart

# 4. 使用 - 传入品牌配置即可
miaoda-studio-cli search-summary --query "{品牌名} 舆情 2026"
```

---

## 🔄 版本历史

| 版本 | 日期 | 更新 |
|------|------|------|
| v3.0 | 2026-04-19 | 通用版，去除硬编码，支持任意酒店集团 |
| v2.0 | 2026-04-19 | 整合BettaFish + 抖音监控 + AI风险分析 |
| v1.0 | 2026-04-18 | 德胧专版，基础舆情搜索 |

---

## ⚠️ 注意事项

1. **配置驱动**：使用前传入 `BRAND_CONFIG` 变量
2. **频率控制**：搜索间隔>3秒
3. **数据合规**：采集内容仅内部分析
4. **视频舆情**：抖音等平台可能需要Cookie
5. **内容审核**：AI分析结果需人工核实

---

**作者**：晁留柱的助手（小柱）
**版本**：v3.0 通用版 | 2026-04-19
**GitHub**：github.com/chaoliuzhu65-tech/hotel-intelligence-suite
