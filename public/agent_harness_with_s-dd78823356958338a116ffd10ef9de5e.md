# Agent Harness 的工业安全工程方法论

## 摘要

工业控制系统的安全工程实践（IEC 61508/61511）可直接复用至 Agent Harness 的设计中。智能体故障本质是物理设备故障的工程映射，而非简单的类比。通过将安全完整性等级（SIL）、独立保护层（IPL）、冗余表决等成熟机制映射到智能体架构中，可构建可靠的多智能体系统。

---

## 一、背景与定义

### 1.1 Agent Harness 的行业定义

Agent Harness 是包裹在 AI 模型外的基础设施层，负责管理长期运行任务的可靠性。它区别于 Agent Framework（提供抽象与心智模型）和 Agent Runtime（执行图与状态管理），核心职责包括：

- 观察对话状态，判断是否需要介入
- 执行规则与策略注入
- 决定 agent 的停止时机
- 管理上下文压缩与上下文窗口

### 1.2 工业控制安全工程

IEC 61508（电气/电子/可编程电子安全相关系统的功能安全）和 IEC 61511（过程工业安全仪表系统的功能安全）是工业控制系统安全工程的国际标准。其核心方法论包括：

- 安全完整性等级（SIL）分级
- 故障安全模式（Fail-Safe / Fail-Operational）
- 冗余表决机制
- 独立保护层（IPL）

### 1.3 两者的互补关系

Agent Harness 是"载体"，工业安全工程是"设计原则"。Harness 定义了包裹 agent loop 的基础设施长什么样，安全工程提供了这个基础设施如何设计才能安全。

---

## 二、理论框架：工业控制与智能体的映射

### 2.1 安全工程映射

| 工业控制 | Agent Harness | 说明 |
|----------|---------------|------|
| 传感器 | LLM 输出 / 工具返回 | 同样存在漂移、噪声、失效 |
| 执行器 | 工具调用 / 状态修改 | 可能拒动、误动、延迟 |
| 安全 PLC | 观察者 Agent | 独立进程/模型，实时监控 |
| 联锁逻辑 | 介入强度（L1-L3） | 硬接线 → 代码化阈值 |
| 冗余表决 | 多模型共识 | 2oo3 → 三模型输出比对 |
| 故障安全位 | 创造者冻结状态 | 失电 → 人工接管 |

### 2.2 风险管理框架迁移

人类社会的风险管理经验可直接迁移至智能体系统：

| 人类风险管理 | Agent Harness | 核心机制 |
|-------------|---------------|----------|
| 金融 Basel 协议 | 认知资本充足率 | 保留上下文预算应对极端场景 |
| 航空 SMS（安全管理系统） | 智能体运营安全 | 危险识别→风险评估→缓解措施→持续监控 |
| 核电 Defense in Depth | 多层防护 | 五层屏障：预防→检测→保护→包容→应急 |

---

## 三、核心机制

### 3.1 安全完整性等级（SIL）

SIL 等级按每小时危险失效概率量化分级。对应到 Agent 架构，单任务累积错误成本可作为分级依据：

| SIL 等级 | 风险降低能力 | Agent 介入层级 | 典型场景 |
|----------|--------------|---------------|----------|
| SIL 1 | 10-100x | L1 提示 | 信息查询、低风险增强 |
| SIL 2 | 100-1000x | L2 确认 | 中等风险决策、需人工确认 |
| SIL 3 | 1000-10000x | L3 熔断 | 高风险操作、立即停止 |
| SIL 4 | 10000+x | 人工强制接管 | 极少用，涉及重大风险 |

关键点：同一指标（如置信度 0.7）应映射到不同 SIL 等级。电商支付与信息查询的错误成本截然不同。

### 3.2 失效模式

#### Fail-Safe（故障安全模式）

- 工业场景：电梯故障 → 强制停靠最近楼层
- Agent 场景：L3 熔断 → 冻结状态 → 转人工接管
- 适用场景：用户可等待（如复杂报告生成）

#### Fail-Operational（故障运行模式）

- 工业场景：飞机飞控 → 冗余系统继续运行
- Agent 场景：创造者降级 → 切换备用模型继续
- 适用场景：必须完成（如紧急预订）

关键决策点：业务场景能承受停机还是必须完成？这决定观察者是否需设计冗余表决层。

### 3.3 冗余表决

工业场景：三个传感器 → 多数表决剔除异常值

Agent 场景：同一任务派给三个模型 → 观察者比对输出差异

```
创造者 A (GPT-4) ──┐
创造者 B (Claude) ──┼→ 观察者表决 → 差异 > 阈值则 L2 确认 / L3 熔断
创造者 C (Gemini) ──┘
```

工业冗余解决单点传感器漂移，智能体冗余解决单模型偏见或幻觉。成本较高（3x token），仅用于 SIL 3 级关键决策（如支付确认 > 10000 元）。

### 3.4 共因失效（CCF）与异构冗余

#### 共因失效的本质

| 大模型现象 | 安全工程概念 | 本质 |
|-----------|-------------|------|
| 花很多 token 也修不好 | 系统性失效 | 设计固有缺陷，运行期不可修复 |
| 同一错误模式反复出现 | 共因失效 | 根因相同（训练数据/架构偏见），多实例同时失效 |
| 提示工程越调越偏 | 诊断盲区 | 观测手段本身受故障影响，无法自我定位 |

#### 为什么传统冗余失效

- 硬件冗余：传感器 A 故障 → 传感器 B 继续工作（独立失效）
- 模型冗余：GPT-4 幻觉 → Claude 同时幻觉（CCF，同受互联网文本污染）

#### 异构冗余解法

- 不同物理原理 → 不同模型架构（Transformer + 符号推理 + 规则引擎）
- 强制异构：不同训练数据、不同模型提供商

### 3.5 风险管理框架迁移

#### 3.5.1 Basel 操作风险映射

| Basel 定义 | Agent Harness 对应 | 缓释措施 |
|-----------|-------------------|----------|
| 内部欺诈 | 创造者故意绕过观察者（如提示注入） | 职责分离、双人控制 |
| 外部欺诈 | 对抗攻击诱导错误工具调用 | 输入验证、行为白名单 |
| 系统故障 | 模型幻觉、工具超时、上下文截断 | 冗余设计、熔断机制 |

#### 3.5.2 领先指标 vs 滞后指标

传统风险管理的核心从"事后归因"转向"事前感知"：

| 滞后指标（传统） | 领先指标（Agent 日志） |
|-----------------|----------------------|
| 任务失败后才分析 | 叙事流中提前发现认知漂移 |
| 最终输出质量评估 | 思考过程中的异常模式识别 |
| 用户投诉驱动改进 | 创造者-观察者交互数据预警 |

日志体系是风险管理中的领先指标库——记录过程数据而非仅记录结果。

#### 3.5.3 认知资本缓冲

类似于金融的资本充足率，Agent 系统需要预留"认知资本"应对极端场景：

```python
class CognitiveCapitalBuffer:
    reserved_for_risk: float = 0.3      # 30% token/计算预算不用于正常任务
    drawdown_trigger = lambda usage: (
        "yellow" if usage > 0.7 else "green"
    )
```

### 3.6 Defense in Depth：五层防护

核电的纵深防御理念直接适用于智能体系统：

| 层级 | 防护类型 | Agent 实现 |
|------|---------|-----------|
| 第一层 | 预防 | 创造者设计：输入过滤、工具 Schema 验证 |
| 第二层 | 检测 | 观察者监控：置信度漂移、工具异常、循环调用检测 |
| 第三层 | 保护 | 自动响应：暂停、升级、优雅降级 |
| 第四层 | 包容 | 限制影响范围：沙箱隔离、资源配额 |
| 第五层 | 应急 | 人工接管：最终安全阀 |

---

## 四、架构设计：独立保护层（IPL）

独立保护层（IPL）的核心理念：每一层应与被保护对象完全隔离。

```python
class SafetyLayer:
    is_independent: bool  # 关键：与创造者完全隔离
    safety_function: SafetyFunction

class SmartAgentSystem:
    # IPL 1：创造者自检（非安全相关，降本）
    creator: Creator

    # IPL 2：观察者（安全相关，独立）
    observer: Observer = Observer(
        separate_model_provider=True,  # 异构隔离
        voting_logic=VotingLogic.ONE_OF_TWO,  # 任一指标触发即动作
        fail_safe_action=lambda: creator.freeze_and_escalate()
    )

    # IPL 3（可选）：冗余表决（高价值操作）
    redundant_council: RedundantCouncil = RedundantCouncil(
        members=[gpt4, claude, gemini],
        trigger_condition=lambda m: m.estimated_value > 10000
    )

    # 工业标准：最终元件（人工）
    human_override: HumanGate
```

---

## 五、工程实践

### 5.1 最小可运行版本（MVP）

```python
# 工业风格：策略配置
class SafetyInstrumentedSystem:
    layers = [
        # 第一层：创造者自检（类似设备自诊断）
        CreatorSelfCheck(max_retries=2),
        # 第二层：观察者阈值（类似安全 PLC）
        ObserverThreshold(
            metrics=['confidence', 'tool_fail'],
            voting_logic=VotingLogic.ONE_OF_TWO,
        ),
        # 第三层：冗余表决（关键操作）
        RedundantVoting(
            creators=[gpt4, claude, gemini],
            agreement_threshold=0.8,
        ),
        # 最终层：物理隔离（人工）
        ManualShutdown(),
    ]
```

### 5.2 Proof Test（定期验证）

工业做法：离线注入已知异常任务，检验观察者触发灵敏度。

智能体做法：定期注入异常任务，验证观察者阈值设置是否合理。

### 5.3 最小可行风险管理（MVR）

```python
class SmartAgentRiskFramework:
    # 1. 风险 appetite 定义（由业务决定）
    appetite = RiskAppetite(
        acceptable_hallucination_rate=0.01,    # 1% 可接受幻觉
        max_cognitive_capital_drawdown=0.3,    # 上下文预算最大 30% 用于风险缓冲
    )

    # 2. 三层防御（Defense in Depth）
    barriers = [
        # 第1层：预防（创造者设计）
        PreventionBarrier(
            rules=['input_sanitization', 'tool_schema_validation']
        ),
        # 第2层：检测（观察者监控）
        DetectionBarrier(
            metrics=['confidence_drift', 'tool_anomaly', 'loop_detection']
        ),
        # 第3层：保护（自动响应）
        ProtectionBarrier(
            actions=['suspend', 'escalate', 'degrade_gracefully']
        ),
    ]

    # 3. 资本缓冲（Basel 风格）
    buffer = CognitiveCapitalBuffer(
        reserved_for_risk=0.3,    # 30% token/计算预算不用于正常任务
        drawdown_trigger=lambda usage: (
            "yellow" if usage > 0.7 else "green"
        ),
    )
```

### 5.3 安全需求规格书（SRS）

业务策略文档化：

| 指标 | 阈值 | 动作 |
|------|------|------|
| confidence | < 0.7 | L2 确认 |
| tool_fail | > 2 | L3 熔断 |
| total_cost | > 10000 元 | 人工确认 |

---

## 六、关键区分与决策

### 随机错误 vs 系统性失效

| 场景 | 策略 |
|------|------|
| 随机错误（温度高偶尔幻觉） | 重试、降温度、增加 context |
| 系统性失效（某类任务必败） | 停止投入 token，重新设计 |
| 诊断盲区（不知为何失败） | 强制异构验证，不一致则熔断 |

### 介入强度选择

| 业务容忍度 | 推荐模式 | 架构选择 |
|-----------|---------|---------|
| 可等待完成 | Fail-Safe | L3 熔断 → 人工 |
| 必须完成 | Fail-Operational | 冗余表决 + 备用模型 |

---

## 七、结论

智能体没有新的故障类型，只有新的故障表现。工业控制的百年经验——失效模式分析、独立保护层、定量安全目标——可直接复用至 Agent Harness 的设计中。

这不是类比，是工程复用。

---

## 附录：工业经验的核心启示

| 工业原则 | Agent Harness 实践 |
|----------|-------------------|
| 任何组件可能失效 | 创造者可能幻觉，观察者可能漏报 |
| 失效模式必须已知 | 定义创造者失效模式（重复错误/置信度崩溃/循环调用） |
| 独立保护层（IPL） | 创造者-观察者分离，不共享状态 |
| 最小化安全功能 | 观察者只做观测+告警，不替代决策 |
| 安全不是"不出错" | 而是"出错后按预定方式失效" |
