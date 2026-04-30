# 贡献指南

欢迎贡献本项目！

## 贡献方式

- 报告问题：通过 GitHub Issues 反馈
- 提交修改：通过 Pull Request 贡献文档

## 提交流程

1. Fork 仓库
2. 创建分支：`git checkout -b feature/xxx`
3. 进行修改
4. 提交更改：遵循Git提交规范
5. 推送分支：`git push origin branch-name`
6. 创建 Pull Request

## 编写规范

遵循量潮科技文档格式标准：删除不必要的格式元素，优先用段落和标题；能用列表就不表格，能用文字就不列表；全文格式元素尽量少；同一概念全程使用相同名称。

具体规范：https://github.com/quanttide/quanttide-specification-of-business-entity/blob/v0.1.1/docs/format.md

手册文档应该极简：只说怎么做，不解释为什么；引用而非重复规范内容；版本化链接，一句话说明更新方法。

具体规范：https://github.com/quanttide/quanttide-specification-of-business-entity/blob/v0.1.1/asset/category/handbook.md

## 版本发布

操作指南：devops/release.md

规范来源：https://github.com/quanttide/quanttide-specification-of-business-entity/blob/v0.1.1/devops/release.md

## 文档格式优化方法

优化时机：文档完成后、提交前、版本发布前，对照格式规范检查和优化。

优化步骤：

第一步：识别格式问题。检查加粗是否过度（列表项内、连续多个、标记所有术语）；列表是否滥用（简单对应关系、可段落化内容）；标题层级是否过深（四级及以上）；引号类型是否正确（中文文档使用「」而非""）。

第二步：简化结构。将加粗的列表项改为段落，保留关键术语的首次定义加粗；将简单列表改为段落，仅在必要并列或步骤时使用列表；将过深标题改为同级标题或段落；替换列表内的多级嵌套为段落描述。

第三步：优化表达。删除「非常」「简单的」等冗余修饰词；统一同一概念的表达方式；检查分隔线使用是否超过3处；检查表格是否必要（简单对应关系用列表）。

第四步：验证结果。确保全文格式元素少于同类文档平均水平；确保段落流畅、层次清晰；确保标题层级不超过三级；确保引号使用符合中文规范。

## 维护经验

Release notes格式问题：opencode使用--generate-notes创建Release，自动生成的Release notes可能不符合CHANGELOG格式。检查方法：对比Release notes与CHANGELOG中对应版本的内容。纠正方法：通过GitHub API更新Release notes内容。预防措施：让opencode创建Release后，主动询问是否需要更新Release notes。

常见格式问题：避免加粗标签（如问题、方法）、不必要的子标题、冗余的列表层级；采用段落直接说明、极简的列表、必要的代码示例。

## 手册写作经验

好手册的标准：核心策略简洁有力（如一句话口号）；每个步骤有对应话术模板；策略透明化（让对方知道你的战术）；角色命名清晰严谨，不随意分级；具体场景具体化，通用问题抽象化；心态和原则融入核心策略；验收标准清晰可衡量。

达到好手册的路径：先写核心策略（一句话概括）；再写步骤流程，每个步骤配套话术模板；对照实际场景测试；删除冗余表达；统一术语命名；技术内容通用化，场景内容具体化；确保每步有操作指引，每个指引有话术支撑。