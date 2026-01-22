# AGENTS.md

## 项目概述

Dify 是一个用于开发大语言模型（LLM）应用的开源平台，具有直观的界面，结合了智能体 AI 工作流、RAG（检索增强生成）管道、智能体能力和模型管理。

代码库分为：

- **后端 API**（`/api`）：使用领域驱动设计（Domain-Driven Design）组织的 Python Flask 应用程序
- **前端 Web**（`/web`）：使用 TypeScript 和 React 19 的 Next.js 15 应用程序
- **Docker 部署**（`/docker`）：容器化部署配置

## 后端工作流

- 阅读 `api/AGENTS.md` 了解详细信息
- 通过 `uv run --project api <command>` 运行后端 CLI 命令。
- 集成测试仅在 CI（持续集成）中运行，不应在本地环境中运行。

## 前端工作流

```bash
cd web                # 进入 web 目录
pnpm lint:fix         # 运行 ESLint 并自动修复代码问题
pnpm type-check:tsgo  # 运行 TypeScript 类型检查
pnpm test             # 运行测试
```

## 测试与质量实践

- 遵循测试驱动开发（TDD）：红（失败）→ 绿（通过）→ 重构。
- 使用 `pytest` 进行后端测试，采用 Arrange-Act-Assert（准备-执行-断言）结构。
- 强制使用强类型；避免使用 `Any`，优先使用显式类型注解。
- 编写自文档化代码；仅添加解释意图的注释。

## 语言风格

- **Python**：在函数和属性上保留类型提示，并实现相关的特殊方法（例如 `__repr__`、`__str__`）。
- **TypeScript**：使用严格配置，依赖 ESLint（首选 `pnpm lint:fix`）加上 `pnpm type-check:tsgo`，并避免使用 `any` 类型。

## 通用实践

- 优先编辑现有文件；仅在请求时添加新文档。
- 通过构造函数注入依赖，并保持整洁架构的边界。
- 在正确的层使用特定于域的异常处理错误。

## 项目约定

- 后端架构遵循领域驱动设计（DDD）和整洁架构原则。
- 异步工作通过 Celery 运行，使用 Redis 作为代理。
- 前端面向用户的字符串必须使用 `web/i18n/en-US/`；避免硬编码文本。
