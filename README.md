# ai003：A 股日线回测系统

供外部模型逐日提交目标组合和买入区间的回测系统。核心流程是 T 日收盘后冻结决策，下一交易日 09:30 先买后卖，收盘估值并计算独立奖励。

## 当前进度

已完成需求、架构、第一版执行策略、开发切片、恢复流程设计原型及架构补充契约。正式 Python 回测系统尚未实现，真实数据资格尚未核验；补齐契约不等于业务验收通过。

## 阅读顺序

1. [1.spec.md](1.spec.md)：产品需求、账户行为与 A01–A19 验收场景。
2. [2.ARCHITECTURE.md](2.ARCHITECTURE.md)：框架选择、模块职责、接口和恢复设计。
3. [3.EXECUTION_POLICY_V1.md](3.EXECUTION_POLICY_V1.md)：第一版执行选择、资金分配算法和费用口径。
4. [4.DEVELOPMENT_PLAN.md](4.DEVELOPMENT_PLAN.md)：开发任务、依赖、验收映射和证据缺口。
5. [5.CONTRACTS.md](5.CONTRACTS.md)：经济敞口与取整、阶段信息与派生值可见性、冻结输入/历史修订/快照、SQLite提交与响应兼容、Gym映射及K01–K15增量验收。

## 开发入口

下一项任务仍是 [T01：单股首日闭环](.scratch/backtest-v1/issues/T01-single-day.md)。任务单保存在 [.scratch/backtest-v1/issues](.scratch/backtest-v1/issues)，共 11 个开发任务和 1 个真实数据证据核验任务。

实施时同时采用原执行策略和[补充契约](5.CONTRACTS.md)，记录execution-v1、contracts-v1及target-exposure-v1与实际参数身份。原C/D规则、A/R编号不改；新增K类已追加至12张任务单，原依赖、状态和T01有限范围保持。T03后的受限Gym映射探测不代表T09已经完成。

## 恢复流程原型

下载或克隆仓库后，在本地浏览器打开 [.scratch/recovery-prototype.html](.scratch/recovery-prototype.html)，可体验请求恢复、奖励失败和重复提交等场景。

原型使用内存状态及预设成交结果，只用于核对状态设计；数据库、进程恢复和正式业务验收仍待开发验证。
