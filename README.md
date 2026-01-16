
# OpenScout

**OpenScout** is an open-source **Agentic Retrieval-Augmented Generation (RAG)** system built using the **LangGraph** framework. It intelligently routes user queries between a **local vectorstore** and **real-time web search**, ensuring optimal relevance, freshness, and efficiency.

OpenScout leverages **open-source LLMs** for both routing and generation, enabling a transparent, controllable, and vendor-neutral AI stack suitable for production and research use cases.

---

## Core Capabilities

* **Agentic Query Routing with LangGraph**
  Deterministic, graph-based agent orchestration using LangGraph for explicit and debuggable control flow.

* **Dual-Model Architecture**

  * **Router Model**: `qwen3:8b` for lightweight, fast decision-making
  * **Generator Model**: `gpt-oss:20b` for high-quality response generation

* **Local-First RAG Strategy**
  Queries are routed to the local vectorstore whenever possible, preserving privacy and reducing latency.

* **Real-Time Web Search via Tavily**
  Automatically invoked for queries requiring fresh or external information.

* **Open Embedding Stack**
  Uses `embeddinggemma:300m` for efficient and high-quality semantic embeddings.

* **Modular and Extensible**
  Each component i.e., routing, retrieval, search, and generation is independently swappable.

---

## System Architecture

OpenScout is implemented as a **LangGraph-powered agentic workflow**, where each node represents a discrete reasoning or retrieval step.

### High-Level Flow

1. User submits a query
2. Router agent (`qwen3:8b`) evaluates intent and freshness requirements
3. Query is routed to:

   * Local vectorstore retrieval, or
   * Tavily-powered live web search
4. Retrieved context is normalized and aggregated
5. Generator model (`gpt-oss:20b`) produces the final answer

---

LangGraph ensures:

* Explicit state transitions
* Deterministic routing logic
* Full traceability and debugging support

---

## Technology Stack

### Agent Framework

* **LangGraph**: Graph-based agent orchestration and control flow

### Language Models

* **Router**: `qwen3:8b`
* **Generator**: `gpt-oss:20b`

### Embeddings

* **embeddinggemma:300m**

### Vectorstore

* SKLearnVectorStore

### Web Search

* **Tavily API** (real-time, LLM-optimized search)

### Evaluation

* LLM as a Judge implemetation to check for Hallusinations and Answer correctness

---

### Example Queries

**Internal Knowledge Query**

```text
"What is CoT prompting?"
```

→ Routed to **vectorstore**

**Fresh / External Query**

```text
"What are the latest developments in the EU AI Act?"
```

→ Routed to **Tavily web search**

---

## LangGraph Agent Design

### Router Node

* Powered by `qwen3:8b`
* Classifies:

  * Knowledge domain (internal vs external)
  * Freshness requirements
  * Confidence threshold for local retrieval

### Retrieval Nodes

* Vectorstore retriever
* Tavily search retriever

### Generation Node

* `gpt-oss:20b`
* Receives structured context and provenance metadata

---


## Use Cases

* Enterprise internal knowledge assistants
* Research copilots with real-time awareness
* Privacy-sensitive RAG systems
* Local-first AI assistants with web fallback
* Developer documentation bots

---

