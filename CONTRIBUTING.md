# CONTRIBUTING

本项目是量潮科技工作手册系统，采用多仓架构管理数字资产。

## 项目结构

见 [README](./README.md)。

## SKILL 维护指南

本项目的 AI Agent 技能存储在 `.agents/skills/` 目录。

SKILL 维护遵循 [Agent Skills 规范](https://agentskills.io/specification)。

### SKILL 目录结构

```
.agents/skills/
├── <skill-name>/
│   └── SKILL.md
```

### SKILL 格式规范

```yaml
---
name: <skill-name>
description: 技能描述，说明使用场景
---
```

### 创建新 SKILL

1. 在 `.agents/skills/` 下创建技能目录
2. 编写 `SKILL.md`，包含 YAML 头和技能说明
3. 参考已有 SKILL 的结构和格式

### 同步 SKILL 到子仓库

稳定的 SKILL 可同步到 gallery 仓库：

```bash
# 复制到 gallery
cp .agents/skills/<skill>/SKILL.md docs/gallery/devops/<skill>/SKILL.md

# 在 gallery 子模块提交
cd docs/gallery
git add devops/<skill>/SKILL.md
git commit -m "docs: add <skill> skill"
git push

# 更新主仓库引用
cd ..
git add docs/gallery
git commit -m "chore: update gallery submodule"
git push
```

---

## .quanttide 配置维护

`.quanttide/` 目录是项目的契约事实源。

### 契约文件

| 文件 | 用途 |
|------|------|
| `.quanttide/asset/contract.yaml` | 数字资产契约 |
| `.quanttide/docs/contract.yaml` | 文档工程契约 |

### 添加新契约

1. 在 `.quanttide/` 下创建对应分类目录
2. 创建 `contract.yaml`，包含契约说明
3. 更新 `.quanttide/README.md` 添加契约索引
4. 提交并推送

### 契约格式

```yaml
# 契约名称
# 模块定位：简述契约用途

# 资产定义
assets:
  <asset-name>:
    title: 资产标题
    type: 资产类型
    path: 资产路径
    description: 资产描述
```

## 工作流程

1. 创建分支：基于 main 创建功能分支
2. 开发：在分支上进行开发
3. 提交：使用 Conventional Commits 格式提交
4. 推送：推送分支并创建 PR

## 文档门户

本项目通过 `docs/index.md` 提供文档中心门户，按记忆模型分类链接到各子模块仓库。

### 构建与部署

| 文件 | 作用 |
|------|------|
| `docs/index.md` | 门户首页，按记忆模型分类列出子模块链接 |
| `docs/myst.yml` | MyST 项目配置，声明 toc、exclude、site 模板 |
| `.github/workflows/deploy-docs.yml` | CI：推送 docs/ 变更时自动构建并部署到 GitHub Pages |

**构建命令**：`myst build --html`（输出到 `_build/html/`，生成静态 HTML）

**排除子模块**：`myst.yml` 中 `project.exclude` 列出所有子模块目录，避免 MyST 递归扫描。

**部署地址**：`https://quanttide.github.io/quanttide-tech/`

### 新增子模块时

1. 将新子模块路径加入 `docs/myst.yml` 的 `project.exclude`
2. 在 `docs/index.md` 添加对应链接

## 发布规范

### 子模块版本标注

CHANGELOG 中涉及子模块更新的条目，必须标注目标 tag 版本号：

```markdown
### 变更
- 更新子模块：qtadmin(v0.2.0)、tutorial(v0.0.3)、roadmap(v0.0.2)
```

版本号来源于子模块自身的 git tag。未发布的子模块用 commit SHA 前 7 位代替。

### 发布流程

详见 `.agents/skills/devops-release/SKILL.md`。

## AI Agent 操作规范

### 工具使用

- **新工具先跑 init**：使用不熟悉的 CLI 框架或配置文件，先执行 `tool init` 查看官方生成的模板，不凭经验臆造格式。
- **命令先求证**：CLI 参数使用前先 `tool --help` 或查阅官方文档确认。
- **部署用官方模板**：CI / Pages 部署对照官方示例工作流，优先复用而非自创。
- **Build 命令区分**：配置文件和构建命令的输出目录要对照确认。例如 MyST 中 `myst build` 输出 `_build/site/`（服务器用），`myst build --html` 输出 `_build/html/`（静态部署用）。

### CI / 部署

- **本地先跑通再推 CI**：工作流变更前在本地执行构建命令，确认产出物正确。
- **验证闭环**：CI 通过不等于可访问。部署后确认最终 URL 返回 200，检查产出物是否有 `index.html`。
- **试错上限**：同一问题试 3 次未解决，停下来检查：是否方向错了？是否偏离了原始意图？

## 更新流程

当发生错误或问题时，按以下流程处理：

1. **记录问题**：在 CHANGELOG.md 或 GitHub Issue 中记录问题
2. **分析原因**：找出问题根因
3. **修复问题**：提交修复
4. **更新文档**：更新 CONTRIBUTING.md、AGENTS.md 或相关 SKILL
5. **持续改进**：从错误中学习，优化工作流程