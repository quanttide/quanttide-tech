# 2026-03-18 学习 quanttide-founder 文件夹命名习惯

## 学习目标
了解上级目录 quanttide-founder 的文件夹命名和结构习惯，为优化 meta/bylaw 层次结构提供参考。

## 学习内容

### 1. quanttide-founder 目录结构
```
quanttide-founder/
├── archive/          # 归档目录
├── essay/            # 文章目录
├── handbook/         # 手册目录
├── journal/          # 日志目录
├── meta/             # 元数据目录
├── paper/            # 论文目录
├── platform/         # 平台目录
├── profile/          # 个人资料目录
├── report/           # 报告目录
├── specification/    # 规范目录
├── tutorial/         # 教程目录
└── usercase/         # 用户案例目录
```

### 2. 日志目录结构（关键发现）
quanttide-founder 使用**子目录分类**日志类型：
```
journal/
├── write/      # 写作日志
├── code/       # 代码日志
└── default/    # 默认日志
```

这种结构比平级文件更清晰，便于扩展。

### 3. Meta 目录结构



### 4. Handbook 目录结构



### 5. 命名习惯总结
- **目录命名**：使用英文小写，简洁明了
- **文件命名**：使用英文小写，用下划线连接
- **层级结构**：使用子目录而不是平级文件
- **分类方式**：按功能/类型分类（write, code, default 等）

## 学习发现：日志规范的层级处理

### 问题分析
在 quanttide-tech 仓库中，发现 `meta/bylaw` 目录存在层次感不足的问题：
- `journal.md`：通用日志规范（父级）
- `learn_journal.md`：学习日志专用规范（子级）

两者平级存放，未体现"通用→专用"的层级关系。

### 解决方案：降级为目录说明
参考 quanttide-founder 的模式，将日志规范从 bylaw 降级为目录 README：

**原方案（bylaw）：**
```
meta/bylaw/
├── journal.md           # 工作章程：日志规范
└── learn_journal.md     # 学习日志章程
```

**新方案（目录说明）：**
```
meta/journal/
├── README.md           # 日志规范主说明
└── learn/              # 学习日志
    └── README.md       # 学习日志规范说明
```

### 为什么不定义为 bylaw？

1. **语义层级不匹配**
   - bylaw 是 L5 工作章程，法律隐喻"宪法"
   - 日志规范是具体操作指南，不是最高级别章程
   - 日志规范应该属于具体实现层面，而不是宪法层面

2. **参考 quanttide-founder 的结构**
   - quanttide-founder 的 `meta/` 目录只有元数据文件
   - 没有复杂的 `meta/bylaw/` 结构
   - 日志规范放在 `journal/README.md` 中

3. **程序型记忆五层体系的适用范围**
   - L1 Paper：理论、原理
   - L2 Usecase：案例、示例
   - L3 Handbook：手册、指南
   - L4 Specification：工程标准
   - L5 Bylaw：工作章程
   
   日志规范更适合作为目录说明，而不是强行纳入五层体系。

4. **功能导向 vs 体系导向**
   - bylaw 方案：体系导向，强行纳入五层体系
   - journal 方案：功能导向，按实际功能组织

### 核心经验
> 日志规范是**具体的操作指南**，应该放在对应的日志目录中，而不是作为最高级别的 bylaw。

## 学习收获
1. **结构化知识管理**：通过记忆分类框架将零散知识系统化
2. **层次化知识体系**：程序型记忆五层体系提供了从原理到实践的完整路径
3. **人机协作规范**：明确的 Agent 指南确保了人机协作的高效性
4. **功能优先原则**：按实际功能组织文档，而不是强行纳入理论体系

## 下一步行动
1. 参考此框架设计公司的第二大脑结构
2. 建立相应的目录结构和文档规范
3. 制定人机协作的工作流程
