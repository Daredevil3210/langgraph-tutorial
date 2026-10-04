# LangGraph 学习教程

基于 [LangGraph](https://www.langchain.com/langgraph) 的入门学习项目，通过 Jupyter Notebook 循序渐进地演示 Agent / 状态图（StateGraph）的核心概念与用法，并提供可在本地 Agent Server 中运行的人工介入示例。

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
│   ├── 16_retry.ipynb           # RetryPolicy：节点异常重试
│   └── 17_cache.ipynb           # InMemoryCache 与 CachePolicy：节点结果缓存
├── chapter03/            # 第三章：检查点、状态恢复与长期记忆
│   ├── 01_in_memory.ipynb      # InMemorySaver：按 thread_id 保存对话状态
│   ├── 02_in_SQL.ipynb         # PostgresSaver：将检查点保存到 PostgreSQL
│   ├── 03_history_state.ipynb  # 查询历史、最新与指定检查点的状态
│   ├── 04_error.ipynb          # 模拟并行节点失败，保存检查点
│   ├── 05_find_error.ipynb     # 查询失败会话的历史状态
│   ├── 06_fix_error.ipynb      # 修复节点后从失败处继续执行
│   ├── 07_replay.ipynb         # 从指定历史检查点重放
│   ├── 08_fork.ipynb           # update_state 与 as_node：状态分叉
│   ├── 09_store.ipynb          # 长期偏好与检查点：个性化多轮对话
│   └── 10_context.ipynb        # Runtime 上下文：按会员等级调整回复
├── chapter04/            # 第四章：人工介入（Human-in-the-loop）
│   ├── 01_HITL.ipynb           # interrupt 与 Command.resume：输入姓名
│   ├── 02_parallel.ipynb       # 并行中断：按中断 ID 恢复多个节点
│   ├── 03_approve.ipynb        # 人工批准或拒绝模型调用
│   ├── 04_approve_edit.ipynb   # 审核并修改模型生成的诗句
│   ├── 05_tool_approve.ipynb   # 工具内部中断：人工批准天气查询
│   ├── 06_single_node.ipynb    # 单节点内按顺序处理中断
│   ├── 07_HITL_checkpoint.ipynb # 顺序中断前后的检查点历史
│   ├── 08_parallel_checkpoint.ipynb # 并行中断前后的检查点历史
│   ├── 09_half_checkpoint.ipynb # 一个节点中断、另一个节点完成
│   ├── 10_static_interrupt.ipynb # 节点执行前后的静态断点
│   ├── 11_static_parallel.ipynb # 并行分支中的静态断点
│   ├── 12_error_static.ipynb   # 调用时设置断点及恢复时的参数变化
│   ├── 13_tool_call.ipynb      # 手动实现模型与天气、新闻工具之间的调用循环
│   ├── 14_tool_node.ipynb      # 使用内置 ToolNode 执行工具
│   ├── 15_tool_node_runtime.ipynb # ToolRuntime 与 Command：工具更新状态
│   ├── 16_wrap_tool_call.ipynb # 包装工具执行过程，按上下文配置重试
│   └── 17_wrap_tool_call.ipynb # 按工具名称和参数缓存执行结果
├── chapter05/            # 第五章：流式输出、子图与子图检查点
│   ├── 01_values.ipynb          # 状态值：TypedDict 字段与节点输出
│   ├── 02_messages.ipynb        # MessagesState + LLM 对话节点
│   ├── 03_checkpoints.ipynb     # 检查点、interrupt 中断与状态历史
│   ├── 04_custom.ipynb          # Runtime.stream_writer 流式输出与工具调用
│   ├── 05_astream_events.ipynb  # astream / astream_events 流式事件
│   ├── 06_subgraph_func.ipynb   # 子图以函数形式在父图节点中调用
│   ├── 07_subgraph_node.ipynb   # 子图作为节点嵌入父图
│   ├── 08_subgraph_checkpoint.ipynb # 子图检查点与 checkpoint_ns 区分
│   ├── 09_subgraph_checkpoint_interrupt.ipynb # 子图内中断与恢复
│   ├── 10_subgraph_checkpoint_memory.ipynb    # 子图编译检查点：多轮对话记忆
│   └── 11_subgraph_checkpoint_more.ipynb      # 子图检查点进阶：批量提问互扰
├── hitl_demo/           # 本地 Agent Server / Studio 人工介入示例
│   ├── langgraph.json          # 注册 graph、chat_graph，加载本地 .env
│   └── src/
│       ├── __init__.py
│       ├── agent.py            # 顺序中断，收集姓名、年龄、性别
│       └── chat_agent.py       # 天气工具调用的批准、拒绝与参数修改
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
| 17_cache | 使用 `InMemoryCache` 和 `CachePolicy(ttl=20)`，对比相同与不同输入下的节点调用 |

## 内容概览（chapter03）

- `01_in_memory`：使用 `InMemorySaver` 保存图检查点，通过相同 `thread_id` 延续对话，并使用不同 `thread_id` 区分会话。
- `02_in_SQL`：使用 `PostgresSaver` 和 `setup()` 初始化检查点表，在数据库连接的 `with` 作用域内运行图，将会话状态保存到 PostgreSQL。
- `03_history_state`：并行生成指定主题的诗歌与笑话，汇总结果；通过 `get_state_history()`、`get_state()` 及 `checkpoint_id` 查询历史、最新和指定检查点状态。
- `04_error`：在并行的笑话节点中主动抛出异常，演示执行失败与检查点保存。
- `05_find_error`：使用同一数据库和 `thread_id`，通过 `get_state_history()` 查看失败执行的历史状态。
- `06_fix_error`：移除人为异常，使用 `graph.invoke(None, config=...)` 恢复未完成的执行。
- `07_replay`：查找写诗、写笑话之前的历史检查点，使用该检查点的配置重新执行后续节点。
- `08_fork`：通过结构化输出选择写诗或笑话；从历史检查点调用 `update_state()`，修改输入或路由结果，使用返回的配置继续执行新分支。
- `09_store`：使用 `PostgresStore` 保存、查询偏好，通过 `runtime.store` 读取当前用户档案；结合 `PostgresSaver` 保存会话消息和已加载偏好，实现个性化多轮对话。
- `10_context`：使用 `UserContext`、`context_schema` 和 `Runtime.context` 传递用户名与会员等级，对比 VIP 和普通用户的回复要求。

## 内容概览（chapter04）

- `01_HITL`：通过 `interrupt()` 暂停图，获取姓名后使用 `Command(resume=...)` 恢复执行。
- `02_parallel`：姓名和年龄节点并行中断，使用中断 ID 到回答的映射恢复各节点。
- `03_approve`：人工决定是否调用模型，使用 `Command(goto=..., update=...)` 路由到生成或拒绝节点。
- `04_approve_edit`：生成诗歌后暂停，让用户修改内容；直接回车可保留原诗。
- `05_tool_approve`：在天气工具内部中断，人工批准或拒绝工具执行，再将结果交回模型。
- `06_single_node`：同一节点内依次询问姓名、年龄、性别，逐次恢复三个中断。
- `07_HITL_checkpoint`：在姓名、年龄的顺序中断及恢复后查询 `get_state_history()`，观察检查点历史。
- `08_parallel_checkpoint`：两个节点并行等待人工输入，按中断 ID 恢复后查看历史状态。
- `09_half_checkpoint`：姓名节点中断、年龄节点正常完成，观察同一超步内的结果保存与恢复。
- `10_static_interrupt`：通过 `compile(interrupt_before=..., interrupt_after=...)` 配置节点执行前后的断点，使用 `invoke(None, ...)` 逐次继续。
- `11_static_parallel`：在两条并行分支中配置静态断点，观察每次暂停和恢复时各节点的执行情况。
- `12_error_static`：在 `invoke()` 时传入静态断点，对比恢复时继续传入断点参数与省略这些参数的行为。
- `13_tool_call`：通过 `@tool` 定义天气和新闻工具，使用 `bind_tools()`、自定义工具节点、`ToolMessage` 和条件路由实现模型与工具之间的循环。`MessagesState` 合并消息历史，额外的 `output` 字段保存最近一次模型返回的内容。
- `14_tool_node`：使用内置 `ToolNode` 替代手写的工具执行节点，自动执行天气、新闻工具并生成工具结果消息。
- `15_tool_node_runtime`：通过自动注入的 `ToolRuntime` 获取工具调用 ID；工具返回 `Command(update=...)`，同时更新 `weather_res` 或 `new_res` 与消息历史。
- `16_wrap_tool_call`：通过 `wrap_tool_call` 包装工具执行过程，从 `UserContext.max_attempts` 读取尝试次数；捕获模拟的 `ConnectionError`，成功即停止，耗尽次数后返回失败消息。
- `17_wrap_tool_call`：使用工具名称和参数的 JSON 字符串构造缓存键，重复查询命中缓存时跳过工具执行，并生成对应当前调用 ID 的工具消息。

## 内容概览（chapter05）

- `01_values`：用 `TypedDict` 声明状态字段，演示节点 A/B 分别写入 `node_a_output`、`node_b_output` 并流式返回（`time.sleep` 模拟耗时节点）。
- `02_messages`：基于 `MessagesState` 构建 LLM 对话节点，重复调用 `invoke` 累积消息历史。
- `03_checkpoints`：使用 `InMemorySaver` 检查点；通过 `interrupt()` 暂停、`Command(resume=...)` 恢复，并以 `stream_mode=["checkpoints"]` 观察检查点流、用 `get_state_history()` 查询历史状态。
- `04_custom`：通过注入的 `Runtime.stream_writer` 在节点内流式输出文本；第二个单元演示 `ToolNode` + `ToolRuntime` + `Command` 的工具调用与状态更新。
- `05_astream_events`：用 `astream` / `astream_events` 以流式模式观察节点执行与事件序列。
- `06_subgraph_func`：编译独立子图（strip → punctuation 文本清洗），在父图节点中以 `subgraph.invoke()` 函数式调用，并用 `get_subgraphs()` 枚举。
- `07_subgraph_node`：与 06 相反，将整个子图直接作为父图的一个节点（`add_node("subgraph_node", subgraph)`）。
- `08_subgraph_checkpoint`：父图、子图共用 `InMemorySaver`；通过 `get_state(config, subgraphs=True)` 查看嵌入子图检查点，用 `checkpoint_ns` 区分不同子图的状态历史。
- `09_subgraph_checkpoint_interrupt`：在子图节点中 `interrupt()` 暂停，父图检查点记录后由 `Command(resume=...)` 恢复执行。
- `10_subgraph_checkpoint_memory`：子图 `compile(checkpointer=True)` 开启记忆（对比 per-invocation 无记忆与 per-thread 有记忆），父图注入 `InMemorySaver`，演示"我是老王 → 我是谁"的多轮对话记忆。
- `11_subgraph_checkpoint_more`：父图一次携带多个提问依次调用子图；开启子图检查点后，同 `thread_id` 的多次提问会互相干扰（历史消息残留），演示 per-thread 记忆的副作用。

## 本地服务示例（hitl_demo）

- `graph`（`src/agent.py:graph`）：在同一节点中依次询问姓名、年龄、性别，每次通过 `interrupt()` 暂停，收到回答后继续。
- `chat_graph`（`src/chat_agent.py:chat_graph`）：模型产生天气工具调用后，一次提交本轮所有调用供人工审核；支持批准（`approve`）、拒绝（`reject`）和修改参数（`edit`），再将工具结果交给模型生成回复。

## 环境准备

```bash
# 安装依赖
pip install -r requirements_full.txt

# 配置 API Key（可选，.env 已加入 .gitignore）
# 在 .env 中填写 DEEPSEEK_API_KEY、DEEPSEEK_BASE_URL 等变量
```

然后用 Jupyter Notebook 逐个打开 `chapter01/`、`chapter02/`、`chapter03/`、`chapter04/`、`chapter05/` 下的 notebook 运行即可。

`chapter02/12_static_loop.ipynb` 和 `13_loop_goto.ipynb` 需要配置 DeepSeek API Key；天气和新闻工具返回的是硬编码演示数据，不是实时查询结果。工具失败由随机数模拟，运行过程和输出可能不同。

`14_remaining_steps.ipynb`、`15_end_loop.ipynb` 和 `16_retry.ipynb` 不需要 LLM API Key，可用于学习循环步数限制和异常重试。其中 `16_retry` 会主动抛出 `HTTPError` 来演示重试耗尽的处理。

`chapter02/17_cache.ipynb` 不需要 LLM API Key，使用延时模拟耗时节点，并将缓存有效期设为 20 秒。观察缓存过期时，应确保距离对应缓存结果写入已超过该有效期。

`chapter03/01_in_memory.ipynb` 需要配置 DeepSeek API Key。请按顺序运行单元格：相同 `thread_id` 使用同一会话状态，不同 `thread_id` 使用独立会话。`InMemoryCache` 和 `InMemorySaver` 的数据都只保存在当前进程内存中，重启内核后不会保留。

第三章的 `02_in_SQL.ipynb` 和 `03_history_state.ipynb` 同样需要 DeepSeek API Key。历史状态示例应按单元格顺序运行，使用本次运行产生的 `checkpoint_id`，不要复用其他内核中的内存检查点 ID。

运行 `02_in_SQL.ipynb` 前，先启动 PostgreSQL，创建数据库和具有建表、读写权限的账号，然后在本地 `.env` 中配置连接地址（将占位内容替换为实际配置）：

```dotenv
DB_URL=postgresql://YOUR_USER:YOUR_PASSWORD@localhost:5432/YOUR_DATABASE?sslmode=disable
```

数据库驱动与检查点依赖已列在 `requirements_full.txt` 中。首次使用时执行 `checkpointer.setup()` 初始化检查点表；数据库本身需要预先创建。首次测试对话记忆时，取消“你好，我是老王”调用前的注释，成功保存后再用相同 `thread_id` 提问“我是谁”。数据库连接配置由环境变量读取，`.env` 和 `.env.*` 不纳入版本控制。

### 第三章进阶示例的运行顺序

- `04_error` → `05_find_error` → `06_fix_error`：三个示例使用同一 `DB_URL` 和 `thread_id="chapter03-05"`。先通过 `02_in_SQL` 的 `checkpointer.setup()` 初始化检查点表，或在 `04_error` 中取消该调用前的注释。`04_error` 的“人为抛异常”是预期的教学行为；随后运行 `05_find_error` 查看状态，再运行 `06_fix_error` 恢复执行。同一超步中已成功完成并保存结果的节点可在恢复时复用结果；延时 5 秒不保证另一个模型调用已经成功完成。
- `07_replay`：依次运行单元格，先产生检查点，再从选中的历史配置重放。重放会重新调用后续模型节点，生成结果可能不同于原结果。
- `08_fork`：依次运行单元格，保持同一个内存检查点对象。使用 `update_state()` 返回的配置启动分支；重启内核后需要重新产生历史检查点。示例的结构化输出只声明 `poem` 和 `joke` 两种模式，兜底节点不是模型异常处理器。
- `09_store`：先运行第一个单元格初始化长期记忆表并写入用户偏好，这部分只需要 PostgreSQL 和 `.env` 中的 `DB_URL`；第二个单元格的个性化对话还需要 DeepSeek API Key。重复写入同一命名空间和键会替换该记录的值；查询默认最多返回 10 条，数据增多时可使用 `limit` 和 `offset` 分页。同一用户的多轮对话使用相同 `thread_id`；不同用户应使用不同会话编号，避免复用他人的消息和偏好。会话已加载偏好后会跳过 Store 查询，若数据库偏好发生变化，需要主动刷新或使用新会话。
- `10_context`：只需要 DeepSeek API Key。`context` 在每次调用时提供用户身份与会员等级，节点据此生成系统提示词；它不会自动成为模型输入。此示例没有配置检查点，两次调用分别演示不同会员等级，跨调用不会自动恢复聊天历史。优惠活动问题用于演示回复语气，示例没有接入实时优惠查询工具。

`04_error`–`08_fork` 使用 DeepSeek 模型，需要 API Key；其中 `04_error`–`07_replay` 还需要 PostgreSQL。示例中的 `topic_index` 是普通全局变量，不属于检查点状态，重新运行初始化代码会将其重置。所有数据库示例从本地环境变量读取连接地址，请勿将真实数据库密码写入 Notebook。

### 第四章的运行要求

`01_HITL`、`02_parallel`、`06_single_node` 和 `07`–`12` 不需要 LLM API Key；`03_approve`、`04_approve_edit`、`05_tool_approve` 和 `13`–`17` 需要 DeepSeek API Key。第四章的人工介入示例使用内存检查点，不需要 PostgreSQL；`13`–`17` 未配置检查点，只在一次调用中维护消息历史。

请在支持 `input()` 的 Jupyter 内核中按顺序运行单元格。首次执行返回 `__interrupt__` 信息，输入答案或审批结果后，用同一个检查点对象及 `thread_id` 调用 `Command(resume=...)`。并行中断使用各自的中断 ID；同一节点内的多个中断按调用顺序逐次恢复。年龄请输入整数，性别示例输入 `male` 或 `female`。重启内核后需要重新执行初始化和首次调用，不能继续使用旧的内存中断。

`interrupt()` 暂停的是图执行；`input()` 是 Notebook 中收集人工回答的方式。恢复时节点会从开头重新执行，避免在中断前执行不可重复的操作。天气工具返回硬编码演示数据，不查询真实天气；工具审批示例需要模型产生天气工具调用，若未产生工具调用，则不会出现该审批中断。

`07_HITL_checkpoint`、`08_parallel_checkpoint` 和 `09_half_checkpoint` 请按单元格顺序运行；其中 `08_parallel_checkpoint` 会要求输入姓名和整数年龄，其余两个示例直接使用预设回答。检查点历史与同一超步内成功节点的待合并写入是不同层次的记录，不应把每次调用 `interrupt()` 都理解成新增一份完整检查点。

`10_static_interrupt`、`11_static_parallel` 和 `12_error_static` 使用静态断点：恢复时传入 `None`，无需提供 `Command(resume=...)` 的人工回答。检查下一步可以调用 `graph.get_state(config).next`，空元组表示没有待执行节点。静态断点按超步边界暂停，并行图中某个节点上的断点也会影响同一超步的其他节点；同时设置节点前后断点时，不能简单按断点数量推算调用次数。

`12_error_static` 的文件名用于提醒断点参数容易遗漏，该示例没有主动抛出异常：图在编译时未配置静态断点，前两次调用显式传入断点参数，后续调用省略参数，因此后续执行不会继续使用前两次调用临时设置的断点。

`13_tool_call` 不包含人工审批：`llm_node` 让模型选择工具，`tool_node` 按名称和参数执行工具，`router` 根据最后一条模型消息是否包含 `tool_calls` 决定继续或结束。工具执行结果使用对应的 `tool_call_id` 写入 `ToolMessage`，供下一次模型调用读取。天气和新闻均为硬编码演示数据；模型可能一次请求多个工具，也可能分多轮请求。工具调用阶段的模型正文可能为空，`output` 会在后续模型回复时被覆盖。

### ToolNode、状态更新、重试与缓存示例

建议按 `13_tool_call` → `14_tool_node` → `15_tool_node_runtime` → `16_wrap_tool_call` → `17_wrap_tool_call` 的顺序学习。这些示例不包含人工审批，也不需要 PostgreSQL；天气与新闻工具返回模拟数据，不提供实时查询。

- `14_tool_node`：图的执行路线仍是模型 → 工具 → 模型。`ToolNode` 接收工具列表，处理模型的调用请求；无需手动按名称查找工具或包装普通字符串结果。
- `15_tool_node_runtime`：模型只提供城市或国内外新闻参数，`runtime` 由 `ToolNode` 自动注入，不暴露为模型参数。`Command.update` 将查询结果写入自定义状态字段，并通过 `ToolMessage` 让模型读取结果；只更新 `weather_res` 或 `new_res` 并不会自动把它传给模型。国内与国外新闻分支均返回状态更新命令。这里的 `Command` 未指定 `goto`，工具执行后回到模型仍由图的边决定。
- `16_wrap_tool_call`：使用 `context=UserContext(max_attempts=3)` 为本次运行提供配置。每个工具请求最多尝试 3 次，包括第一次执行；失败概率为 70%，仅捕获 `ConnectionError`，没有等待间隔。重试期间不重新调用模型；三次都失败时返回工具失败消息，随后模型仍可能提出新的工具请求，新请求会重新获得尝试次数，因此这不是整轮对话的总次数限制。
- `17_wrap_tool_call`：按顺序运行两个代码单元格，在同一内核中重复查询北京以观察缓存。缓存只保存工具返回的内容，命中时使用本次 `tool_call_id` 创建新的消息；模型本身仍会执行。`global_cache` 是进程内的普通字典，没有过期时间，重新运行初始化单元格或重启内核会清空缓存。参数 JSON 未排序，多参数工具中不同的键顺序可能形成不同缓存键。

### 启动 hitl_demo 本地服务

使用 Python 3.11 或更高版本，先在仓库根目录安装 `requirements_full.txt` 中的依赖，其中已包含 `langgraph-cli[inmem]`。在本地创建 `hitl_demo/.env`，填写以下变量，并将占位内容替换为自己的配置：

```dotenv
DEEPSEEK_API_KEY=YOUR_DEEPSEEK_API_KEY
# 如需在 Studio 中调试，配置自己的 LangSmith API Key
LANGSMITH_API_KEY=YOUR_LANGSMITH_API_KEY
```

`langgraph.json` 中的 `.env` 路径相对于该配置文件，因此使用的是 `hitl_demo/.env`，不是仓库根目录的 `.env`。服务启动时会加载两个图，`chat_graph` 在模块导入时初始化 DeepSeek 模型，所以即使只调试收集信息的 `graph`，也需要准备 DeepSeek API Key。

```bash
# 从仓库根目录进入示例目录
cd hitl_demo
langgraph dev
```

根据终端输出打开 Studio 地址，或访问本地 API 文档 `http://127.0.0.1:2024/docs`。本地开发服务无需 Docker 或 PostgreSQL；更多启动选项见 [LangGraph 本地开发文档](https://docs.langchain.com/langsmith/local-dev-testing)。

- 选择 `graph`：以空输入 `{}` 启动，在各次中断中依次提供姓名、整数年龄、`male` 或 `female`，恢复至完成。
- 选择 `chat_graph`：传入用户消息，例如 `{"messages": [{"role": "user", "content": "今天北京天气怎么样？"}]}`；模型提出天气工具调用后，查看中断中的 `action_requests` 和 `review_configs`，提交审核决定。

`chat_graph` 的恢复值为包含 `decisions` 列表的对象；列表按本轮工具调用顺序排列，每个调用对应一个决定。下面是单个调用的三种恢复值示例：

```json
{"decisions": [{"type": "approve"}]}
```

```json
{"decisions": [{"type": "reject", "message": "暂不查询天气"}]}
```

```json
{"decisions": [{"type": "edit", "edited_action": {"name": "get_weather", "args": {"city": "上海"}}}]}
```

在同一个服务线程中恢复执行；通过 SDK 或 API 调用时，在 `command` 的 `resume` 字段中传入上述对象。`edit` 分支只使用修改后的参数，仍执行原请求的工具；缺少对应决定时默认拒绝该调用。若模型继续请求工具，会再次中断。天气工具返回模拟结果，不提供实时天气查询。

两个服务图都使用 `compile()` 导出，由 Agent Server 管理检查点；若直接在普通 Python 脚本中运行并恢复中断，需要自行配置检查点保存器与 `thread_id`。本地 `.env`、`.env.*`、服务运行数据和 Python 缓存均被 Git 忽略。

### 第五章的运行要求

`chapter05/02_messages`、`10_subgraph_checkpoint_memory` 和 `11_subgraph_checkpoint_more` 需要配置 DeepSeek API Key；其余示例（`01_values`、`03_checkpoints`、`04_custom`、`05_astream_events`、`06_subgraph_func`、`07_subgraph_node`、`08_subgraph_checkpoint`、`09_subgraph_checkpoint_interrupt`）不调用 LLM，可直接运行。`04_custom` 的第二个单元格涉及工具调用示例，需要 API Key 才能看到完整输出；`03_checkpoints` 按单元格顺序运行，先执行首次 `invoke` 触发中断，再通过 `Command(resume=...)` 恢复。

第五章的子图示例说明如何使用函数或节点方式嵌入子图，以及 `checkpoint_ns` 如何区分父图与子图的检查点历史；`10` 和 `11` 通过 `compile(checkpointer=True)` 对比 per-invocation 与 per-thread 记忆行为。所有示例使用 `InMemorySaver` 内存检查点，不需要 PostgreSQL；重启内核后内存检查点会清空。

## 版本发布

- [v0.11.0](https://github.com/Daredevil3210/langgraph-tutorial/releases/tag/v0.11.0)：新增第五章：流式输出、子图（函数式/节点式）与子图检查点（含中断、记忆、批量提问互扰）示例。
- [v0.10.0](https://github.com/Daredevil3210/langgraph-tutorial/releases/tag/v0.10.0)：新增内置 ToolNode、工具运行时状态更新、工具重试与结果缓存示例。
- [v0.9.0](https://github.com/Daredevil3210/langgraph-tutorial/releases/tag/v0.9.0)：新增工具调用 Notebook 和本地人工介入服务，支持天气工具的批准、拒绝与参数修改。
- [v0.8.0](https://github.com/Daredevil3210/langgraph-tutorial/releases/tag/v0.8.0)：新增中断检查点、并行恢复与静态断点示例。
- [v0.7.0](https://github.com/Daredevil3210/langgraph-tutorial/releases/tag/v0.7.0)：新增运行时上下文与第四章人工介入示例，完善长期记忆对话。
- [v0.6.0](https://github.com/Daredevil3210/langgraph-tutorial/releases/tag/v0.6.0)：新增异常恢复、历史重放、状态分叉和 PostgreSQL 长期记忆示例。
- [v0.5.0](https://github.com/Daredevil3210/langgraph-tutorial/releases/tag/v0.5.0)：新增 PostgreSQL 检查点与历史状态查询，补充第三章学习说明。
- [v0.4.0](https://github.com/Daredevil3210/langgraph-tutorial/releases/tag/v0.4.0)：新增节点缓存与内存检查点示例，开始第三章的会话状态学习。
- [v0.3.0](https://github.com/Daredevil3210/langgraph-tutorial/releases/tag/v0.3.0)：新增第二章 12–16，涵盖工具调用循环、剩余步数、循环终止与节点重试。
- 完整版本记录见 [Releases](https://github.com/Daredevil3210/langgraph-tutorial/releases)。

## 许可证

[MIT](LICENSE)
