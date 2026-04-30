# CONTRIBUTING

quanttide-tech 项目的子模块，教程模块，涵盖管理、生成式 AI、Git 等领域的实战指南。

## 使用场景

### 文档更新

修改子模块内容后，推送更新并同步到主仓库。

1. 子模块内提交：`git commit -m "docs: update content"`
2. 子模块内推送：`git push`
3. 更新主仓库引用：`git add docs/tutorial && git commit -m "chore: update tutorial submodule"`

## 提交规范

使用 [Conventional Commits](https://www.conventionalcommits.org/) 规范：`<type>: <description>`

### 提交类型

- feat：新功能
- fix：修复 bug
- docs：文档更新
- test：测试相关
- refactor：代码重构
- chore：构建/工具

## 工作原则

1. 最小干预：仅在用户明确请求时操作
2. 原子提交：每次提交独立完整
3. 验证优先：修改后检查文件命名和内容
4. 明确命名：严格按照规范命名文件
5. 反思学习：从错误中学习并改进工作流程
6. 写作规范：遵循本文档中的文档写作标准

## 文档写作标准

遵循 [Google 文档风格指南](https://google.github.io/styleguide/docguide/style.html)。

### 写作原则

- 删：删除不必要的格式元素，优先用段落和标题
- 简：能用列表就不表格，能用文字就不列表
- 少：全文格式元素（分隔线、表格、加粗）尽量少
- 一：同一概念全程使用相同名称

### 具体规范

1. 语言简洁：删除不必要的修饰词，避免"非常"、"简单的"、"也就是"
2. 主动语态：优先使用主动句，如"Agent 创建文件"而非"文件被 Agent 创建"
3. 术语统一：同一概念全程使用相同术语
4. 标题层级：最多使用三级标题
5. 列表一致性：无序列表用 `-`，有序列表用 `1.`
6. 代码块标注：必须标注语言类型

## 发布规范

### 版本标签格式

使用 `v<version>` 格式：

```bash
git tag v0.0.1
git push origin v0.0.1
```

### 发布流程

1. **更新 CHANGELOG.md** - 添加新版本和变更内容
2. **提交 CHANGELOG.md**
3. **创建标签** - `git tag v<version>`
4. **推送标签** - `git push origin v<version>`
5. **创建 GitHub Release** - 使用 CHANGELOG 内容作为 release notes

### 版本规范

遵循语义化版本（SemVer）：
- alpha: `v0.0.1-alpha.1`
- beta: `v0.0.1-beta.1`
- release: `v0.0.1`
