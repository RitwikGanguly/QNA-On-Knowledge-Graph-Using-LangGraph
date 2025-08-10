# Question Answering of BioMedicle KG 

![diff image](https://www.js-craft.io/wp-content/uploads/2025/03/langchain-vs-langgraph.webp)

In the repo, we will discuss the question-answering of Biomedicle Knowledge Graph using a approach, where **we will use the natural language for query** and the information will be retrieved and **we can see the answer also in natural language format.**

SEEMS INTERESTING ❗

I performed the workflow of this task, in 2 ways
- Using LangChain
- Using LangGraph

As, name suggested, lanchain supported sequence-wise instruction and all the instructions performed in a sequencing manner, whereas langgraph worked in a stepwise manner, where we used multiple sub-Agent our all sub-tasks.

## LangChain:
The files are found at - `KG_RAG_LLM_GRAPH.ipynb` and `graph_kg_PROMPTING.ipynb`

![langchain](https://miro.medium.com/v2/resize:fit:1200/1*05zEoeNU7DVYOFzjugiF_w.jpeg)

As, from the image all the instruction and sub-tasks are performed sequentially, so when needed **we cannot backtrack or rethink about the process**.

## LangGraph

It's the advance Multi-Agent system by LangChain community.

File found at - `KG_langgraph.ipynb`

![langgraph](https://www.getzep.com/guides/images/67763d0c2c765ddc16efcfd0_67763cbb89e7793bdd588306_key_20conceps.jpeg)

Here, the main and foremost advantage is, it performed all the instruction and sub-task step-wise (node specific), and when needed we can backtrack or use the reasoning.

## Why the LangGraph is more ROBUST than LangChain in our task ❓

**LangGraph moves you from being a user of a pre-built tool to the architect of a transparent, robust, and custom-fit reasoning engine.**

Let's use an analogy:
- **LangChain (e.g., GraphCypherQAChain)** is like buying a high-quality, pre-built car. It's fast, convenient, and works great for standard trips on well-paved roads.
- **LangGraph** is like being given a professional garage with an engine, chassis, and all the specialized parts. You assemble the car yourself. It takes more upfront effort, but you can build a custom Formula 1 racer designed specifically for the complex, high-stakes track of biomedical data.

### Comparison:
| Feature | LangChain (`GraphCypherQAChain`) Approach | LangGraph (Your New Agent) Approach |
|---------|-------------------------------------------|--------------------------------------|
| **Control & Transparency** | **Black Box.** The chain internally generates a query, executes it, and synthesizes an answer. You have very little visibility or control over these intermediate steps. | **Glass Box.** Every step (entity extraction, query generation, KG execution, vector search, final synthesis) is an explicit, inspectable node. You see the exact state after each step. |
| **Error Handling & Robustness** | **Brittle.** If any internal step fails (e.g., the final synthesis), the whole chain can fail silently, giving you a useless "I don't know" answer. | **Robust.** You can build custom logic at each step. If Cypher generation fails, you can route to a different path. If KG execution returns no data, you can rely solely on the vector context. |
| **Combining Data Sources** | **Difficult.** Designed to work with *one* primary source (the graph). Injecting context from a separate vector store into its hidden internal prompt is complex and unnatural. | **Natural & Stateful.** The `GraphState` object is a shared workspace. The KG node puts its findings there, the vector store node adds its context, and the final synthesis node uses both for a rich answer. |
| **Custom Logic & Prompts** | **Limited.** You can provide a custom prompt for Cypher generation, but it's only one piece of hidden machinery. You can’t control the final synthesis prompt as effectively. | **Unlimited.** Every node is powered by your own Python code and custom prompts. You have fine-grained control over the “brain” of each step, from entity extraction to the final answer. |
| **Debuggability** | **Painful.** When it fails, you have to guess which internal part broke. | **Simple.** The `app.stream()` output gives you a turn-by-turn “flight recording” of your agent’s thought process. You can pinpoint the exact node and state where things went wrong. |
| **Suitability for Your Task** | Good for **simple, direct lookups** on a graph. | Essential for **complex, multi-source, high-stakes question answering** where reliability and explainability are paramount. |


### Flowchart

![flowchart](https://github.com/RitwikGanguly/QNA-On-Knowledge-Graph-Using-LangGraph/blob/main/flowchart_kg_qna_langgraph.png)











