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
│   └── first_demo_graph.png     # 示例图可视化输出
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

## 环境准备

```bash
# 安装依赖
pip install -r requirements_full.txt

# 配置 API Key（可选，.env 已加入 .gitignore）
# 在 .env 中填写 DEEPSEEK_API_KEY 等变量
```

然后用 Jupyter Notebook 逐个打开 `chapter01/` 下的 notebook 运行即可。

## 许可证

[MIT](LICENSE)