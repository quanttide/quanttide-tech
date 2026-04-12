# 数字资产契约

## 模块定位

本仓库是量潮科技工作手册系统的主仓库，采用多仓架构管理数字资产。

## 资产定义

| 资产 | 类型 | 分类 | 路径 | 描述 |
|------|------|------|------|------|
| 工作手册 | docs | handbook | docs/handbook | 量潮科技工作手册系统 |
| 案例画廊 | docs | gallery | docs/gallery | 企业实体案例展示框架 |
| 工程标准 | docs | specification | docs/specification | 量潮科技工程标准规范 |
| Agent 技能 | config | skill | .agents/skills | AI Agent 可复用技能 |
| 应用应用 | app | qtapp | apps/ | 量潮科技应用项目 |
| 静态资源 | asset | static | assets/ | 静态资源子模块 |

## 资产详情

### 工作手册 (docs/handbook)

- **类型**: docs
- **分类**: handbook
- **路径**: `docs/handbook`
- **描述**: 量潮科技工作手册系统，包含 AGENTS.md、CONTRIBUTING.md 等工程规范

### 案例画廊 (docs/gallery)

- **类型**: docs
- **分类**: gallery
- **路径**: `docs/gallery`
- **描述**: 企业实体案例展示框架，按职能板块（connect、execute、think、write）组织

### Agent 技能 (.agents/skills)

- **类型**: config
- **分类**: skill
- **路径**: `.agents/skills`
- **描述**: AI Agent 可复用技能，包含 commit、format 等常用技能

### 应用项目 (apps/*)

- **类型**: app
- **分类**: qtapp
- **路径**: `apps/*`
- **描述**: 量潮科技应用项目子模块集合

### 静态资源 (assets/*)

- **类型**: asset
- **分类**: static
- **路径**: `assets/*`
- **描述**: 静态资源子模块集合，如图书馆资源

## 概念定义

数字资产契约将隐性的工作流转化为显性的、可版本控制的、可迁移的数字资产契约。

## 核心价值

- 多仓分离：文档、应用、资产分离管理
- 子模块化：各资产独立版本控制
- 契约驱动：以 `.quanttide/` 目录作为契约事实源
