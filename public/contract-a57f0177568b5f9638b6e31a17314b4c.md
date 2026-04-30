# 数据契约

数据契约（Data Contract）是数据生产方与消费方之间的约定，定义数据的结构、质量、时效和安全。

## 适用范围

适用于数据清洗、数据集成、数据服务等涉及数据交付的项目。一次性和持续服务均可使用，区别在于时效承诺的表达方式。

## 契约元数据

| 字段 | 说明 |
|------|------|
| `contract_version` | 契约版本号 |
| `schema_version` | Schema 版本号 |
| `id` | 资产唯一标识 |
| `name` | 资产名称 |
| `description` | 资产描述 |

## 契约双方（parties）

| 角色 | 字段 | 说明 |
|------|------|------|
| 提供方 | `provider.name` / `provider.contact` / `provider.reviewer` | 数据生产方 |
| 消费方 | `consumer.name` / `consumer.contact` | 数据使用方 |

## 时效承诺（sla）

| 场景 | 字段 | 说明 |
|------|------|------|
| 一次性项目 | `delivery_deadline` | 交付截止日期 |
| 一次性项目 | `project_duration` | 项目工期 |
| 一次性项目 | `delivery_mode` | 交付方式 |
| 持续服务 | `update_frequency` | 更新频率（如"每日"） |
| 持续服务 | `freshness` | 数据新鲜度要求 |
| 通用 | `penalty` | 违约条款 |

## 安全与保密（security）

| 字段 | 说明 |
|------|------|
| `classification` | 密级：公开 / 内部 / 机密 / 绝密 |
| `policies` | 安全策略列表（如加密存储、禁止外传等） |

## 数据资产

分为 `raw_assets`（原始数据）和 `cleaned_assets`（产出数据）两类。

### 必填字段

| 字段 | 说明 |
|------|------|
| `id` | 资产唯一标识 |
| `name` | 资产名称 |
| `path` | 文件路径 |
| `format` | 文件格式（xlsx / csv / dta / json 等） |
| `source` | 数据来源 |
| `description` | 资产描述 |
| `schema.fields` | 字段级 Schema 定义 |

### 可选字段

| 字段 | 说明 |
|------|------|
| `quality` | 质量验收规则（cleaned_assets 推荐） |
| `owners` | 数据负责人列表 |
| `count` | 文件数量 |
| `notes` | 备注 |

### 字段级 Schema（schema.fields）

| 字段 | 说明 |
|------|------|
| `name` | 字段名 |
| `type` | 数据类型（string / integer / float / date / boolean） |
| `description` | 字段描述 |
| `nullable` | 是否可空 |
| `enum` | 枚举值列表（可选） |

### 质量验收规则（quality）

| 字段 | 说明 |
|------|------|
| `match_rate` | 匹配率阈值（如 `>= 90%`） |
| `row_count` | 行数一致性要求 |
| `key_uniqueness` | 主键唯一性 |
| `unmatched_fill` | 未匹配填充策略（`0` / `null`） |
| `completeness` | 完整性要求 |

## 数据血缘（lineage）

| 字段 | 说明 |
|------|------|
| `step` | pipeline 步骤标识 |
| `inputs` | 输入资产路径列表 |
| `output` | 输出资产路径 |

## 全局验收规则（acceptance）

| 字段 | 说明 |
|------|------|
| `rule` | 规则名称 |
| `threshold` | 阈值 |
| `method` | 检验方法 |

## 变更日志（changelog）

| 字段 | 说明 |
|------|------|
| `version` | 版本号 |
| `date` | 变更日期 |
| `changes` | 变更说明 |
