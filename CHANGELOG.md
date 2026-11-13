# 更新日志

本文档记录项目所有重要变更。格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.0.0/)。

## [Unreleased]

### 变更

- 更新子模块：gallery(d01a10b)，qtadmin 产品范围新增 cli 板块——cli 是 AI 的入口，平台内部不一定内置 AI，AI 能力通过 Skill 适配接入
- 更新子模块：gallery(2b7c3c7)，qtadmin 产品范围 cli 板块补自建边界——外部工具 cli 能批量做的就用它，做不了的批量操作是自建系统的建设重点
- 更新子模块：gallery(5418b98)，qtadmin 新增账号管理（密码本纪律、quanttide-secret）、记账（审批数据为记账依据）、平台经济（分成与分工、抽成即税收）三篇案例，入口页补财务与经济板块
- 更新子模块：intention(58e66de)，qtclass 新增产品篇——AI 原生的产教融合众包生态定位、目标用户、三级火箭架构（site/lite/studio）、AI 原生创新点

## [0.7.7] - 2026-11-12

### 移除

- packages/quanttide-project-toolkit 子模块退役：取消挂载、本地目录清空（README/STATUS 同步）

### 变更

- 更新子模块：gallery(v0.2.3)，qtadmin 首页取消全部引用改为概述；议事规则 `qtadmin/delib/rule.md` 移除，`myst.yml` toc 同步
- 更新子模块：journal(3b49184)，移除 fetch-chat-logs skill
- 更新子模块：journal(a0ce841)，恢复 qtclass/ 日志 35 篇（撤销 10-29 迁出，default/ 7 篇归位，README/AGENTS 口径复原）

- 更新子模块：roadmap(e264ddd)，qtclass 账号与支付接入设计 auth-pay 并入 provider 篇——落地 Phase 0-5 转待办勾选项，设计全文归数据面路线图
- 更新子模块：roadmap(bc68b17)
- 更新子模块：qtclass(b04cc59)——ROADMAP 全系按 v0.1 目标重写（root + site/studio/lite/provider/cli）：静态探针纪律、服务端等待契约、双引擎分工与收口顺序对齐产品路线，qtclass 产品路线图重写——v0.1 固定一版数据模型（契约喂真场景、模板/实例第一刀、双引擎切分）、v1.0 商业化运营三条标志；正文按口径不引用具体文档
- 更新子模块：qtclass(lite/v0.1.3)——筛选由底部弹层改为两排常驻分段（需求/验收各一排，选项不藏）；同批纠正 lite 0.1.2 与 site 0.1.3 的 CHANGELOG 发布日期（实发 11-07）；tag 触发部署，线上复核 200 且 bundle 与本地构建同哈希
- 更新子模块：qtclass(lite/v0.1.2、site/v0.1.3)——lite 页签外壳（理论 / 实践 / 我的 + AppBar，微信式）与两把尺筛选（任务书 `tags.requirement/acceptance` 全量标注 12/12，课程清单自 site 迁入理论页）；site 首页上线（课程特色取材宣传册）瘦身为首页 + 价格并加 lite / studio 连接引用；两仓 CHANGELOG 转正 + package.json 升版 + tag 触发部署，线上复核 200
- 更新子模块：qtadmin(v0.1.0-alpha.1)——CLI 四命令骨架首发（entity / domain / adapter / category，名词为主，叶子诚实标注数据源未接），版本起点与 ROADMAP 新结构线同步
- journal/profile 禁移动措辞收窄（事实源不搬不入 app；语境仓库草稿定稿归位属正常流动）；qtadmin 板块两草稿归位：journal→`data/journal/default/2026-11-06.md`（按分流：管理后台不单独立目录）、platform/cli→`apps/qtadmin/docs/dev-guide/cli.md`；子模块指针 data/journal、data/context、qtadmin 更新
- 仓库分工明文：qtcloud=职能执行仓（execute / connect），qtadmin=围绕 journal / profile 资产只读展示；**journal/profile 禁止移动**（住 `data/`，不入 app）——tech README/AGENTS/CONTRIBUTING 与 qtcloud、qtadmin 各自 README/AGENTS/CONTRIBUTING 同步；子模块指针 qtcloud(1cd16a6)、qtadmin(eee0c70)
- 加深七篇原文挂入门槛/收敛认知（2026-11-02）：insight 四篇（business-lines-and-clouds、open-source-as-moat、intent-supply、free-traffic-leverage）+ intention 三篇（from-project-to-product、from-heart-to-designer、intro/index），均带日期补节并互链新篇
- 更新子模块：roadmap(99f2608)，qtclass 新增账号与支付接入设计 auth-pay（qtcloud-auth JWT 校验、qtcloud-pay 钱包与订单代理、Phase 0-5 落地），studio 落点口径终态同轮入册

- course 域模型定型（用户裁决终态）：**toolkit 暂不引入**——Assignment / Solution / SolutionStep 三件**独立实现于 studio `lib/models/`**，业务迭代稳定后固定回 `quanttide-tech-toolkit` 的 `dart/course`（toolkit 当轮落地已 revert 回裸骨架；中途树形 DecompositionNode 设计已撤）；三件孪生 id/title/content，SolutionStep + `after` 边组 DAG（一层不嵌套、单元自足，判断标准与注解进 content）；`states/` 装 bloc 与状态、不设 bloc/；flutter analyze 无告警、全量 81 测全绿；roadmap studio 篇、app ROADMAP、studio TODO 三处同步
- studio 更名：Brief → **Assignment（大作业）**，studio 定位明确为「大作业的解体思路」；数据契约三字段由用户定：`id`(uuid) / `title` / `content`（content 默认 Markdown 长文本，未来拓展视频等格式，四问降为正文内素材）——活文档三份与代码落点随口径（实例存储后改本机 XDG，不进仓不进 assets），洞察归档保留原词
- studio 单用户化：砍全部学员交互与客户面（派发/批改/客户面/淘汰赛等七项），定位改教学设计工作台；核心判断=本体是 v0.1 互动编排引擎、节点载荷暂为文档非视频；创作空间保持优先——app 四个 ROADMAP 与 roadmap 仓三处同步，精简理由入册
- 洞察仓新增 qtclass/studio.md（Studio 作为教学思路的载体，自语境仓库移交），索引挂入演进主题
- qtclass lite v0.1.1：当前任务换小说发行与游戏两个工作室任务书（源 academy intention，与公众号同源），旧「任务书修订」下线
- qtclass lite 发正式版 lite/v0.1.0：Web 形态学员任务端首切片上线 lite.class.quanttide.com（三页 + 静态契约 + 任务书 10 篇首迁）；基础设施照 site 惯例新建（OSS qtclass-lite + CDN 子域 + ZeroSSL 证书 + deploy-lite.yml）
- qtclass site 发正式版 site/v0.1.2：课程页回归单一列表、首页与 /learn 下线、/prices 上线（三档服务模式卡）；验收流程入 CONTRIBUTING，实习生执行清单入 TODO
- qtclass 路线图双仓对齐：roadmap 仓产品路线图按 scope 分五篇（site/studio/lite/provider/cli），app 六个 ROADMAP 精简为下一步待办（179 → 78 行），决策史归 git/CHANGELOG 与意图库、历史库
- qtclass 商业化归置：宣传册新增 qtclass/business.md（G/B/C 三种合作方式对外口径），learn 两篇历史页迁图书馆存档；意图库 business.md 收薄只留内部判断；history 同名同实体（演化故事）；roadmap 产品路线图对齐三端与仓内自持；app 根 ROADMAP 标明只管工程
- 日志归位 30 篇：context 草稿箱清空仅留当日（qtcloud 10、qtconsult 6、qtdata 2、default 3 归 journal；qtadmin 2 归 archive；qtclass 7 归实训基地日志仓）
- 更新子模块：qtcloud(b1e27b6, cli/v0.1.0-alpha.1)，首发 CLI 并发布 crates.io——内置 skills 命令（qtcloud-devops-release 随二进制分发）、退出码契约自 qtfounder 吸收、release-cli 发布链路
- 更新子模块：brochure(8c890a2)，qtdata 宣传册新增 how.md（制衣厂数据清洗）
- CONTRIBUTING.md 精简（134 → 38 行），AI 操作经验迁 AGENTS.md
- AGENTS.md 记录语境仓库（data/context）是其他仓库的草稿箱
- STATUS.md 精简为纯快照（19 → 13 行），qtdata 差距分析移除——已由 data/insight 承载

## [0.7.6] - 2026-10-01

### 新增

- 新增 packages/quanttide-project-toolkit 子模块（量潮项目管理标准库，2583096）

### 变更

- 更新子模块：qtconsult(3a073fd)、insight(df5cafd)、roadmap(1eac5f0)、profile(6084734)、intention(8d9420c)、archive(f3016c8)、tutorial(8faca2b)
- qtconsult 应用重构：路由 go_router 化、main.dart 瘦身为纯入口、文档主题合并、CI Flutter 版本对齐
- 量潮咨询内容重组：教程目的改写；业务档案自 profile 归档至 archive；洞察与路线图中 self 归入 project，Studio 文档自 roadmap 迁入 insight

## [0.7.5] - 2026-09-29

### 变更

- 更新子模块：intention(v0.3.1)、tutorial(v0.7.2)

## [0.7.4] - 2026-09-29

### 变更

- 量潮招聘、量潮众包两章自 tutorial 迁入 handbook：handbook(104556a)、tutorial(abb7c03)

## [0.7.3] - 2026-09-29

### 新增

- 新增 apps/qtconsult 子模块（量潮咨询，e9ba97c）

### 变更

- examples/default → examples/quanttide-tech-lab（云端仓库名 + 本地路径同步重命名，子模块项目名改为 quanttide-tech-lab）

## [0.7.2] - 2026-08-13

### 新增

- 新增 qtconsult 简介文档（what.md）及其目录引用。
- 新增氛围编程实践课时 1 任务书与附加题。
- 新增 qtcloud-code 意图，用于 Vibe Coding 治理。
- 新增 qtrecurit 生产代码交叉评审实验，以及 qtdata 原型 v1-v4（含进度条仪表盘）。

### 变更

- 同步更新多个子模块（qtadmin、qtclass、qtcloud、qtdata、qtrecurit、roadmap、insight、intention、journal、brochure、tutorial、handbook、bylaw、examples 等）至最新版本，并统一切换为跟随 main 分支。
- 重构 qtadmin（lib 化、接入 connect chat、添加 qtrecurit 示例）与 qtclass（widgets 按粒度分组重构、宣传册合并为单页）。
- 完成 qtdata studio 重写与 qtrecurit Flutter 初始化，新增 Studio 路线图及产品化意图。
- 调整战略报告、咨询文档、brochure 等内容的组织与格式，统一为列表风格。

### 修复

- 修复测试警告与测试清理相关问题。
- 修复文档中的空格、路径、标题、编号等细节问题。

### 移除

- 移除 qtadmin 中废弃的 project、share 及业务域命令。
- 移除 brochure 中的 services、training、qtdata 定价与案例行等内容。
- 移除 bylaw 中的 blueprint、data contract 章节及 roadmap changelog 等冗余文档。
- 清理构建产物（target/、lib/）并迁移/整理相关目录。

## [0.7.1] - 2026-06-17

### 变更

- 更新子模块：handbook(v0.4.1)、bylaw(v0.6.2)

## [0.7.0] - 2026-06-17

### 变更

- 重构：docs/ 下子模块迁移至 data/（archive、report、context、library、brochure、intention、history）
- 重构：myst.yml 和 index.md 从 docs/ 移至根目录
- 重构：docs/vision → docs/intention
- 添加子模块：docs/intention
- 移除子模块：qtcloud-business、qtcloud-delib、qtcloud-org
- 重写 index.md 为角色化导航门户
- 更新子模块：bylaw(v0.6.1)、handbook(v0.4.0)、profile、roadmap、qtadmin、qtdata、examples、gallery、essay

## [0.6.9] - 2026-06-15

### 变更

- 更新子模块：bylaw(v0.5.8)

## [0.6.8] - 2026-06-15

### 变更

- 更新子模块：bylaw(v0.5.7)

## [0.6.7] - 2026-06-15

### 变更

- 更新子模块：bylaw(v0.5.6)

## [0.6.6] - 2026-06-15

### 变更

- 更新子模块：bylaw(v0.5.5)

## [0.6.5] - 2026-06-15

### 变更

- 更新子模块：roadmap(v0.1.0)

## [0.6.4] - 2026-06-15

### 变更

- 更新子模块：bylaw(v0.5.4)

## [0.6.3] - 2026-06-03

### 新增

- 新增子模块：qtcloud-business、qtcloud-delib、qtcloud-org（PoC 案例逐域拆分）
- 商务报价三条线完成：章程(v0.5.3) + 手册(场景化) + 教程(定价思维)
- PoC 清单：新增 examples/README.md，覆盖 10 个业务域

### 变更

- archive 子模块：archive/ → docs/archive/
- examples/default：重新指向 laboratory 仓库
- docs/story → docs/history（云端仓库名 + 本地路径同步重命名）
- 更新子模块：bylaw(v0.5.3)、handbook、tutorial、report、journal、profile、library

### 移除

- 旧 examples/default（指向 example 仓库）

## [0.6.2] - 2026-05-19

### 变更

- 更新子模块：handbook(v0.3.0)、tutorial(v0.4.0)

## [0.6.1] - 2026-05-15

### 变更

- 移动子模块路径：archive(docs/archive → archive)、library(assets/library → docs/library)
- 删除已空的 assets/ 目录

## [0.6.0] - 2026-05-15

### 新增

- 新增子模块：examples/default(v0.0.1)

### 变更

- 更新子模块：bylaw(v0.4.0)、qtconsult、qtdata
- 重构 docs/ 导航分类为程序性记忆与陈述性记忆
- 统一协议：docs 下 CC-BY-4.0，apps 下 Apache 2.0

## [0.5.3] - 2026-05-12

### 变更

- 重构 myst.yml：不依赖子仓库，子站点全部引用已部署的 GitHub Pages URL
- 简化部署工作流：只构建 docs/，不再构建子模块
- 更新 index.md 为已发布链接清单表格
- 新增子站点：宣传册 (brochure)、品牌故事 (story)
- 更新子模块：handbook(v0.2.1)、tutorial(v0.2.2)、bylaw(v0.3.1)、qtdata

## [0.5.2] - 2026-05-11

### 新增

- 文档站点：为 tutorial、bylaw、vision 子模块配置 MyST 文档站点及 GitHub Pages 自动部署
- docs-deploy SKILL：标准化 MyST 文档部署流程
- 主仓库 TOC 新增子站点链接（工作教程、工作章程、业务愿景）

### 变更

- 更新子模块：tutorial(v0.2.0)、bylaw(v0.3.0)、archive(v0.1.0)、vision(v0.2.0)

## [0.5.1] - 2026-05-08

### 变更

- 更新子模块：qtadmin(v0.0.7)、qtclass(v0.0.1)、qtdata、library、brochure、profile(v0.1.3)、report

## [0.5.0] - 2026-05-08

### 变更

- 移除子模块：qtgame-tycoon
- 新增子模块：qtconsult(v0.1.0)、qtcloud

## [0.4.3] - 2026-05-05

### 变更

- 更新子模块：vision(v0.1.0)

## [0.4.2] - 2026-05-05

### 变更

- 更新子模块：story(v0.1.0)、gallery(v0.1.0)

## [0.4.1] - 2026-05-05

### 变更

- 更新子模块：essay(v0.1.1)

## [0.4.0] - 2026-05-05

### 变更

- 更新子模块：bylaw(v0.2.0)、handbook(v0.1.0)、tutorial(v0.1.0)

## [0.3.2] - 2026-05-02

### 新增
- 新增子模块：qtgame-tycoon(v0.0.1)

## [0.3.1] - 2026-04-30

### 新增
- 新增子模块：qtweb
- 新增文档：zstu 大数据微专业蓝图、qtdata 与 qtclass 工作方案

### 变更
- 更新子模块：qtadmin、tutorial、roadmap

## [0.3.0] - 2026-04-29

### 变更
- 更新子模块：qtadmin（移除过期文档）、qtdata（添加示例文件）、brochure（更新案例故事）、roadmap（内部培训文档）、story（同步思维笔记）

## [0.2.2] - 2026-04-27

### 变更
- 更新子模块

## [0.2.1] - 2026-04-20

### 变更

- 更新子模块：roadmap(v0.0.1)、archive

## [0.2.0] - 2026-04-16

### 新增

- devops-release 技能：发布 Git 仓库 Release，支持子模块和主仓库两种发布流程
- devops-review 技能：审查仓库状态、CHANGELOG、版本一致性等
- ROADMAP.md 产品路线图文档
- docs/brochure 子模块

### 变更

- 更新多个子模块：handbook(v0.0.4-54)、tutorial、gallery、context(v0.1.0-5)、specification(v0.1.3)
- 更新文件命名规范，支持 _ 和 - 分隔符

## [0.1.2] - 2026-04-12

### 新增

- SKILL 快速索引添加触发时机列

### 变更

- 更新流程移至 CONTRIBUTING.md
- AGENTS.md 精简为工作原则

## [0.1.1] - 2026-04-11

### 新增

- 智能体技能配置目录及 release 发布技能
- Docker 部署配置
- manifests/iac FaaS 架构
- product/contract.yaml 产品契约
- AGENTS.md、CONTRIBUTING.md 规范文档

### 变更

- 同步 15+ 个子模块更新
- 重构子模块目录，新增 apps/ 目录
- 统一 Docker 术语
- 完善资产契约

## [0.1.0] - 2026-04-03

### 新增

- 13 个子模块：archive, bylaw, essay, gallery, handbook, journal, library, profile, report, roadmap, specification, tutorial
- 2 个代码子模块：qtadmin, qtcloud-finance
- AGENTS.md、CONTRIBUTING.md、README.md 规范文档
- .gitignore 配置

### 变更

- 统一 CHANGELOG 格式为中文
- 更新子模块引用

### 文档

- 秘书处制度
- 从执行者到管理者教程
- 离职工作章程
- Git 仓库资产管理规范

## [0.0.4] - 2026-03-28

### 新增

- 文档子模块：archive, gallery, handbook, library, specification, story
- 代码子模块路径调整至 apps/ 目录

### 变更

- 优化文档结构
- 更新子模块引用

## [0.0.3] - 2026-03-26

### 新增

- 文档子模块：bylaw, essay, tutorial, roadmap

### 变更

- 重构子模块目录结构

## [0.0.2] - 2026-03-24

### 新增

- 文档子模块：journal, profile, report

### 变更

- 子模块统一移至 docs/ 目录下

## [0.0.1] - 2026-03-23

### 新增

- 初始项目结构
- 量潮创始人学习日志
- AGENTS.md 文件命名规范
- 层级化日志规范体系（Paper → Handbook → Bylaw）
- 元文件夹结构（bylaw 和 tutorial）
- Journal 子模块（商业实体）
- Profile 子模块（商业实体）
- Report 子模块（商业实体）

### 变更

- 将学习日志详情移至 meta/bylaw/learn_journal.md
- 重构日志规范到 meta 文件夹
- 将子模块移至 docs 目录- qtrecurit 手册与随笔迁出至创新联盟（docs/handbook、docs/essay 两子模块更新）
- data/brochure 子模块更新：qtrecurit 招聘宣传三篇迁出至创新联盟
- data/insight、data/history 子模块更新：qtrecurit 洞察与历史文章迁出至创新联盟
- data/archive/journal 子模块更新：qtrecurit 日志 20 篇迁出至创新联盟
- data/archive 子模块更新：qtrecurit 归档平移至创新联盟
- data/roadmap、data/report、docs/bylaw 子模块更新：qtrecurit 招聘路线图、招聘报告（含生成技能）、招聘审计章程迁出至创新联盟
- data/journal 子模块更新：qtclass 实训基地实录 35 篇迁出至实训基地日志仓
- data/journal 子模块更新：移回 7 篇业务设计日志（归 default/）
