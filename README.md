# 🚀 Agentic RAG – Smarter AI Retrieval with LLM Agents  

Welcome to **Agentic RAG**, an **intelligent retrieval system** that doesn’t just fetch data—it **thinks before retrieving**. Unlike traditional RAG, which passively pulls from a vector database, **Agentic RAG dynamically decides** whether to:  

✅ Retrieve **stored knowledge** (Qdrant)  
✅ Perform a **real-time web search** (Tavily)  

This **prevents outdated responses, reduces hallucinations, and improves efficiency** for LLM-powered applications.  

---

## 📌 Features  

- **🔍 Hybrid Retrieval** – Chooses **between stored embeddings & live web search** dynamically.  
- **🧠 Decision-Making AI Agent** – Knows when to **use Qdrant** vs. **search the web**.  
- **⚡ Faster & Smarter** – Reduces unnecessary API calls, optimizing response time & accuracy.  
- **🛠️ Prevents AI Hallucinations** – Avoids guessing by fetching fresh data when needed.  
- **📓 Hands-on Colab Notebook** – Try it out **without setup hassles**.  

---

## 🔧 Installation  

### 1️⃣ Install Dependencies  

```bash
pip install --upgrade langchain langchain_community pypdf langchain-huggingface google-generativeai qdrant-client
```

### 2️⃣ Clone This Repo  

```bash
git clone https://github.com/devjothish/AgenticRAG.git
cd AgenticRAG
```

### 3️⃣ Set Up API Keys  

To run Agentic RAG, you need API keys for **Qdrant** (vector search) and **Tavily** (web search).  

```python
import os
os.environ["QDRANT_API_KEY"] = "your-qdrant-api-key"
os.environ["TAVILY_API_KEY"] = "your-tavily-api-key"
```

---

## 🚀 How It Works  

### **1️⃣ Store Knowledge in Qdrant (Vector DB)**  

Qdrant stores documents in **vector format** for fast similarity-based retrieval.  

```python
from qdrant_client import QdrantClient

qdrant = QdrantClient(
    url="https://your-qdrant-instance.com",
    api_key=os.getenv("QDRANT_API_KEY")
)
```

---

### **2️⃣ Define Retrieval Tools**  

The agent chooses between **vector search** (Qdrant) and **live web search** (Tavily).  

```python
from langchain.tools import Tool

# Qdrant Vector Search Tool
vector_search_tool = Tool(
    name="VectorStore",
    func=lambda query: vectorstore.similarity_search(query, k=3),
    description="Use this tool when the query is related to stored documents."
)

# Tavily Web Search Tool
web_search_tool = Tool(
    name="WebSearch",
    func=web_search,
    description="Use this tool when the query requires fresh or real-time information."
)

tools = [vector_search_tool, web_search_tool]
```

---

### **3️⃣ Create the AI Agent**  

The agent **decides dynamically** whether to retrieve from Qdrant or use Tavily for fresh information.  

```python
from langchain.agents import AgentExecutor

agent_executor = AgentExecutor(
    agent=chain,   # The LLM-powered decision-maker
    tools=tools,   # Vector search & web search tools
    handle_parsing_errors=True,  
    verbose=True   
)
```

---

### **4️⃣ Run Queries & See It in Action**  

```python
query1 = "What is Agentic RAG?"
response1 = agent_executor.invoke({"input": query1})
print(response1)
```

```python
query2 = "Who won the latest NBA game?"
response2 = agent_executor.invoke({"input": query2})
print(response2)
```

🔹 **If the query matches stored knowledge** → The agent retrieves from **Qdrant**.  
🔹 **If the query requires real-time data** → The agent searches the web using **Tavily**.  

---

## 🎯 Live Demo  

🟢 **Try the hands-on Colab Notebook** → [Click Here](https://colab.research.google.com/drive/1y4kde6RErXgtDa8OPT6xmqSiIyy6EKjM?usp=sharing)  

---

## 📞 Contact  

👨‍💻 **Jothiswaran Arumugam**  
🔗 **GitHub:** [github.com/devjothish](https://github.com/devjothish)  
💬 **Twitter:** [@devjothish](https://twitter.com/devjothish)  

---

### **Happy Building! 🚀**
