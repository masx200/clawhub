# CodeBuddy Skills

CodeBuddy Code 技能集合，通过外部 API 集成扩展 CodeBuddy Code 的功能。

## 项目简介

这是一个自包含的技能包集合，每个技能都是一个独立的包，用于增强 CodeBuddy Code 的能力。

## 技能列表

| 技能 | 版本 | 语言 | 功能 |
|------|------|------|------|
| firecrawl-search | 1.0.0 | Python | 通过 Firecrawl API 进行网页搜索和抓取 |
| gitlab-api | 0.1.0 | Bash | GitLab REST API 用于仓库操作 |
| gitlab-manager | 1.0.0 | Node.js | GitLab 仓库/MR/问题管理 |
| openclaw-tavily-search | 0.1.0 | Python | 通过 Tavily API 进行网页搜索 |

## 目录结构

```
<skill-name>-<version>/
  SKILL.md        # 技能定义（含 frontmatter）
  _meta.json      # 元数据：ownerId, slug, version, publishedAt
  scripts/        # 实现脚本（Python、Bash 或 JavaScript）
  references/     # 可选：API 文档或参考文件
```

## 环境变量

技能需要以下环境变量：

| 变量 | 用途 |
|------|------|
| `FIRECRAWL_API_KEY` | firecrawl-search 技能使用 |
| `GITLAB_TOKEN` | gitlab-api 和 gitlab-manager 技能使用 |
| `TAVILY_API_KEY` | openclaw-tavily-search 技能使用（也支持 `~/.openclaw/.env`） |

## 添加新技能

1. 创建目录：`<skill-slug>-<version>/`
2. 编写 `SKILL.md`，包含 frontmatter 和文档
3. 在 `scripts/` 中添加实现
4. 创建 `_meta.json`，包含 ownerId、slug、version、publishedAt

## 技能规范

- 目录名使用 `<slug>-<version>` 格式（如 `gitlab-api-0.1.0`）
- SKILL.md 必须包含 YAML frontmatter，包含 `name` 和 `description` 字段
- 脚本应可执行并妥善处理错误
- 使用环境变量或配置文件存储 API 凭证（切勿硬编码）

## 脚本模式

- **Python 脚本**：使用 `argparse` 处理 CLI，使用 `urllib.request` 或 `requests` 处理 HTTP
- **Bash 脚本**：使用 `curl` 调用 API，使用 `jq` 解析 JSON
- **Node.js 脚本**：使用原生 `fetch`，无需外部依赖
