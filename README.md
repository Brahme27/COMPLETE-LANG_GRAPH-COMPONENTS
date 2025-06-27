# LangGraph components
### This repo will help you to understand how to use different components using LangGraph 


| **Component**              | **Type**         | **Simple Definition**                                               | **Example**                                                                                    |
| -------------------------- | ---------------- | ------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `StateGraph`               | Class            | Used to **build a graph** of steps/functions.                       | `graph = StateGraph(MyState)`                                                                  |
| `START`, `END`             | Constants        | Special markers to show **start and end** of the graph.             | `graph.add_edge(START, "step1")`<br>`graph.add_edge("step2", END)`                             |
| `.add_node(name, fn)`      | Method           | Adds a **node (function)** to the graph with a unique name.         | `graph.add_node("playgame", play_game)`                                                        |
| `.add_edge(from, to)`      | Method           | Creates a **fixed path** between two nodes.                         | `graph.add_edge("playgame", "cricket")`                                                        |
| `.add_conditional_edges()` | Method           | Adds **dynamic branching** based on condition function return.      | `graph.add_conditional_edges("playgame", decide_play)`                                         |
| `.compile()`               | Method           | Finalizes the graph and makes it ready to run.                      | `graph_builder = graph.compile()`                                                              |
| `.invoke(data)`            | Method           | Executes the compiled graph with input data.                        | `graph_builder.invoke({"name": "Brahme"})`                                                     |
| `ToolNode`                 | Prebuilt Node    | Built-in LangGraph node that handles **tool/function execution**.   | `graph.add_node("tools", ToolNode([add]))`                                                     |
| `tools_condition`          | Prebuilt Utility | **Condition function** to check if tool should be called.           | `graph.add_conditional_edges("llm_tool", tools_condition)`                                     |
| `add_messages`             | Reducer          | Appends new messages to the state instead of overwriting.           | `Annotated[list[AnyMessage], add_messages]`                                                    |
| `Annotated`                | Python Typing    | Used to **enhance type** with a reducer like `add_messages`.        | `messages: Annotated[list[AnyMessage], add_messages]`                                          |
| `TypedDict`                | Python Typing    | Defines a state with **static type hints** (no runtime check).      | `class MyState(TypedDict): name: str`                                                          |
| `@dataclass`               | Python Class     | Used to define state with class-like structure (no runtime checks). | `@dataclass class MyState: name: str`                                                          |
| `BaseModel` (Pydantic)     | Python Class     | Defines state with **type validation at runtime**.                  | `class MyState(BaseModel): name: str`<br>`graph_builder.invoke({"name": 123})  → Raises Error` |

---

### ✅ Example Comparison of States:

| **State Type** | **Enforces at Runtime?** | **Example**                        |
| -------------- | ------------------------ | ---------------------------------- |
| `TypedDict`    | ❌ No                     | Accepts wrong types silently       |
| `@dataclass`   | ❌ No                     | Accepts wrong types silently       |
| `BaseModel`    | ✅ Yes                    | Raises error if type doesn’t match |
