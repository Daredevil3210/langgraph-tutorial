# LangGraph 学习教程

基于 [LangGraph](https://www.langchain.com/langgraph) 的入门学习项目，通过 Jupyter Notebook 循序渐进地演示 Agent / 状态图（StateGraph）的核心概念与用法。

## 目录结构

```
langgraph/
├── chapter01/            # 第一章：图（Graph）基础
│   ├── 01_graph.ipynb           # StateGraph 入门：定义状态、构建图、可视化
│   ├── 02_dataclass.ipynb       # 使用 dataclass 定义状态
│   ├── 03_pydantic.ipynb        # 使用 Pydantic 模型定义状态
│   ├── 04_reducer.ipynb         # Reducer：自定义状态合并逻辑
│   ├── 05_node_state.ipynb      # 节点读写状态
│   ├── 06_node_overwrite.ipynb  # 节点内覆盖 / 更新状态
│   ├── 08_node_state.ipynb      # 节点状态进阶示例
│   ├── 09_state.ipynb           # 输入/输出/全局/私有状态划分
│   ├── 10_message_llm.ipynb     # 接入 LLM（ChatDeepSeek）+ MessagesState 消息状态
│   └── first_demo_graph.png     # 示例图可视化输出
├── chapter02/            # 第二章：图的高级结构与控制流
│   ├── 01_edge.ipynb            # 边（Edge）连接节点
│   ├── 02_parallel.ipynb        # 并行节点执行
│   ├── 03_route.ipynb           # 条件路由（conditional edges）
│   ├── 04_path_map.ipynb        # 路由映射 path_map
│   ├── 05_router2.ipynb         # 路由进阶（Router 变体）
│   ├── 06_path_map2.ipynb       # path_map 进阶
│   ├── 07_defer.ipynb           # 延迟节点（defer，异步审计）
│   ├── 08_Dynamic_send.ipynb    # Send 动态分发子任务
│   ├── 09_command.ipynb         # Command 在节点内更新图状态
│   ├── 10_fan_in_and.ipynb      # 多路扇入（fan-in）汇合
│   ├── 11_mapreduce.ipynb       # Map-Reduce 模式（mapper/router/reducer + Send）
│   ├── 12_static_loop.ipynb     # 静态边与条件路由构建工具调用循环
│   ├── 13_loop_goto.ipynb       # Command.goto 动态控制工具调用循环
│   ├── 14_remaining_steps.ipynb # RemainingSteps：根据剩余步数结束循环
│   ├── 15_end_loop.ipynb        # recursion_limit 与 GraphRecursionError
│   └── 16_retry.ipynb           # RetryPolicy：节点异常重试
├── requirements_full.txt # 完整依赖清单（LangChain / LangGraph / Jupyter 等）
└── .env                  # 环境变量（API Key 等，不纳入版本控制）
```

## 内容概览（chapter01）

| Notebook | 主题 |
| --- | --- |
| 01_graph | StateGraph 基本流程：TypedDict 定义状态、节点、START/END、Mermaid 可视化 |
| 02_dataclass | 用 `dataclass` 定义状态 |
| 03_pydantic | 用 Pydantic `BaseModel` 定义状态 |
| 04_reducer | 自定义 reducer，演示 list 追加等合并行为 |
| 05_node_state | 节点对状态字段的读写 |
| 06_node_overwrite | 节点中覆盖 / 更新状态字段 |
| 08_node_state | 节点状态相关进阶示例 |
| 09_state | 输入状态 InputState / 输出状态 OutputState / 全局状态 / 私有状态 PrivateState |
| 10_message_llm | 连接 DeepSeek 等 LLM，`MessagesState` 消息队列与 HumanMessage/AIMessage 流转 |

## 内容概览（chapter02）

| Notebook | 主题 |
| --- | --- |
| 01_edge | 用 `add_edge` 连接 START → 节点 → END 的线性流程 |
| 02_parallel | 多节点并行执行与汇聚 |
| 03_route | `add_conditional_edges` 条件路由，根据节点结果选择下一分支 |
| 04_path_map | 路由映射 `path_map`：用映射表驱动条件路由 |
| 05_router2 | 条件路由变体：多个下游分支反复路由 |
| 06_path_map2 | path_map 进阶：路由函数 + 映射表组合 |
| 07_defer | `defer` 延迟节点：主流程先返回，审计等任务异步执行 |
| 08_Dynamic_send | `Send` API 动态分发：按数据生成多个 worker 子任务 |
| 09_command | `Command`：节点内直接更新状态并指定后继节点 |
| 10_fan_in_and | 多路扇入：多个节点汇聚到同一目标节点（AND 汇合） |
| 11_mapreduce | Map-Reduce：mapper 拆分子任务 → 并行执行 → reducer 汇总 |
| 12_static_loop | 静态边 + 条件路由：在 LLM 与工具节点间循环，模拟工具失败后的再次调用 |
| 13_loop_goto | 使用 `Command(update=..., goto=...)` 更新消息并动态选择工具或输出节点 |
| 14_remaining_steps | 使用 `RemainingSteps` 读取剩余超步数，在步数不足时路由到 END |
| 15_end_loop | 设置 `recursion_limit`，捕获 `GraphRecursionError` 并结束循环示例 |
| 16_retry | 使用 `RetryPolicy(max_attempts=3, jitter=False)`，演示节点异常重试及耗尽后的处理 |

## 环境准备

```bash
# 安装依赖
pip install -r requirements_full.txt

# 配置 API Key（可选，.env 已加入 .gitignore）
# 在 .env 中填写 DEEPSEEK_API_KEY、DEEPSEEK_BASE_URL 等变量
```

然后用 Jupyter Notebook 逐个打开 `chapter01/`、`chapter02/` 下的 notebook 运行即可。

`chapter02/12_static_loop.ipynb` 和 `13_loop_goto.ipynb` 需要配置 DeepSeek API Key；天气和新闻工具返回的是硬编码演示数据，不是实时查询结果。工具失败由随机数模拟，运行过程和输出可能不同。

`14_remaining_steps.ipynb`、`15_end_loop.ipynb` 和 `16_retry.ipynb` 不需要 LLM API Key，可用于学习循环步数限制和异常重试。其中 `16_retry` 会主动抛出 `HTTPError` 来演示重试耗尽的处理。

## 版本发布

- [v0.3.0](https://github.com/Daredevil3210/langgraph-tutorial/releases/tag/v0.3.0)：新增第二章 12–16，涵盖工具调用循环、剩余步数、循环终止与节点重试。
- 完整版本记录见 [Releases](https://github.com/Daredevil3210/langgraph-tutorial/releases)。

## 许可证

[MIT](LICENSE)
