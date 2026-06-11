# ai-overseas-daily

> 8源聚合 + 三门控质检 + 双端自动分发的海外 AI 情报管线，日报从采集到推送全自动。

## 它做什么

每个工作日自动从 8 个海外数据源采集 AI/LLM 领域情报，经 LLM 按三板块结构化分析后，分发到飞书知识库（完整报告）和如流群（精简摘要）。

## 三板块 & 质量门控

| 板块 | 聚焦 | 门控 |
|------|------|------|
| 海外商业化与竞争格局 | 模型厂商如何赚钱、如何竞争 | 商业关联检验：必须有定价/营收/市场份额信息 |
| 数据工程与模型能力突破 | 数据策略如何驱动模型能力提升 | 先进性门控：必须对比已有方法论证突破点 |
| 应用创新与工程前沿 | AI 原生应用创新与工程落地方法 | 创新性门控：必须说明解决了什么新问题 |

## 8 个数据源

| # | 来源 | 类型 |
|---|------|------|
| 1 | Twitter List | 精选 AI 账号动态 |
| 2 | Twitter Global Search | 全网 AI 热门推文 |
| 3 | Hacker News | 硅谷技术风向 |
| 4 | Reddit | 硬核 AI 社区讨论 |
| 5 | Product Hunt | AI 新产品 |
| 6 | 博查搜索 | 中英文 AI 资讯 |
| 7 | ArXiv | 数据工程前沿论文 |
| 8 | HuggingFace Daily Papers | 热门 AI 研究 |

## 快速开始

```bash
# 1. 安装依赖
pip install -r scripts/requirements.txt

# 2. 配置环境变量（复制模板并填入你的 API Key）
cp assets/.env.example .env

# 3. 运行（仅生成报告，不分发）
python3 scripts/daily_report.py --no-distribute

# 4. 完整运行（生成 + 分发到飞书/如流）
python3 scripts/daily_report.py
```

## 环境配置

必填项：

| 变量 | 说明 |
|------|------|
| `RAPIDAPI_KEY` | RapidAPI 密钥（Twitter/Reddit/ProductHunt） |
| `LLM_API_KEY` | LLM API Key |
| `LLM_BASE_URL` | LLM 接口地址（OpenAI 兼容） |
| `LLM_MODEL` | 模型名称 |
| `FEISHU_APP_ID` / `FEISHU_APP_SECRET` | 飞书应用凭证 |
| `FEISHU_WIKI_SPACE_ID` | 飞书知识库空间 ID |
| `RULIU_WEBHOOK_URL` / `RULIU_GROUP_ID` | 如流群配置 |

完整配置说明见 [assets/.env.example](assets/.env.example)。

## 定时调度

```bash
# crontab 示例：工作日 9:03 AM
3 9 * * 1-5 cd /path/to/project && python3 scripts/daily_report.py >> cron.log 2>&1
```

## 输出样例

**如流推送格式：**

```
一、海外商业化与竞争格局
1. **OpenAI与微软延长收入分成协议至2030年**
2. **Anthropic pre-IPO估值达1万亿美元**

二、数据工程与模型能力突破
1. **fchollet团队开源ARC-AGI-3人类基准数据集**

三、应用创新与工程前沿
1. **Cursor推出Background Agent实现异步编程**
```

## 项目结构

```
├── SKILL.md                     # Skill 完整说明
├── README.md
├── assets/.env.example          # 环境配置模板
├── references/system_prompt.md  # LLM 报告生成 Prompt
├── scripts/
│   ├── daily_report.py          # 主管线（采集→清洗→LLM→分发）
│   ├── distribute.py            # 分发模块（飞书+如流）
│   └── requirements.txt         # Python 依赖
└── evals/evals.json             # 测试用例
```

## License

MIT
