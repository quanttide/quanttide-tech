# CONTRIBUTING

项目结构见 [README](./README.md)。

## 使用场景

### 文档更新

修改 `docs/` 下的子模块内容，在子模块内提交并推送，然后更新主仓库引用。

1. 子模块内提交：`git -C docs/handbook commit -m "docs: update content"`
2. 子模块内推送：`git -C docs/handbook push`
3. 更新主仓库引用：`git add docs/handbook && git commit -m "chore: update handbook submodule"`

### 代码开发

修改 `src/` 下的子模块，遵循子模块内的 AGENTS.md 规范。

## 工作原则

1. 最小干预：仅在用户明确请求时操作
2. 原子提交：每次提交独立完整
3. 验证优先：修改后检查文件命名和内容
4. 明确命名：严格按照规范命名文件
5. 反思学习：从错误中学习并改进工作流程
6. 写作规范：遵循本文档中的文档写作标准

## 子模块操作

### 更新子模块

```bash
# 查看子模块状态
git submodule status

# 更新所有子模块
git submodule update --init --recursive

# 在子模块中提交并推送
git -C <子模块路径> commit -m "message"
git -C <子模块路径> push
```

### 提交子模块更新

1. 在子模块中提交并推送
2. 在主仓库提交子模块引用更新

```bash
git -C docs/handbook add -A
git -C docs/handbook commit -m "feat: update content"
git -C docs/handbook push

git add docs/handbook
git commit -m "chore: update handbook submodule"
git push
```

## 工作流程

1. 创建分支：基于 main 创建功能分支
2. 开发：在分支上进行开发
3. 提交：使用 Conventional Commits 格式提交
4. 推送：推送分支并创建 PR

---

## 文档写作标准

遵循 [Google 文档风格指南](https://google.github.io/styleguide/docguide/style.html)和[量潮科技写作格式标准](../specification/write/format.md)。

### 写作原则

- 删：删除不必要的格式元素，优先用段落和标题
- 简：能用列表就不表格，能用文字就不列表
- 少：全文格式元素（分隔线、表格、加粗）尽量少
- 一：同一概念全程使用相同名称

### 核心原则

- 简洁：删除冗余词汇，用词简洁
- 一致：全文术语统一，格式一致
- 主动：使用主动语态，直接表达
- 具体：提供具体示例，避免模糊表述

### 具体规范

1. 语言简洁：删除不必要的修饰词，避免"非常"、"简单的"、"也就是"
2. 主动语态：优先使用主动句，如"Agent 创建文件"而非"文件被 Agent 创建"
3. 术语统一：同一概念全程使用相同术语
4. 标题层级：最多使用三级标题
5. 列表一致性：无序列表用 `-`，有序列表用 `1.`
6. 代码块标注：必须标注语言类型

```bash
git status
```

```python
def hello():
    print("Hello")
```