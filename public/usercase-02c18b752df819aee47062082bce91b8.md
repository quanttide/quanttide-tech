# Use Case 编写指南

## 定义

Use Case（用例）是**真实的工作成果示例**，用于展示某种文档类型的实际写法。

## 核心原则

### 1:1 映射

usercase 的目录结构应与被参考的源目录保持一致。

```
源目录结构          →    usercase 结构
report/default/     →    usercase/report/default/
```

### 内容纯净

- 只含报告正文 + YAML frontmatter
- 无"模板"、"说明"、"指南"等解释性文字
- 让读者" seeing is believing"

### 真实优先

复制实际完成的工作成果，而非为演示而编造。

## 更新流程

1. 选择已完成的工作文档
2. 按相同目录结构复制到 usercase
3. 提交到 usercase 子模块
