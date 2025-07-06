# 🚀 TaskWhiz – The Smart Project & Task Management Chatbot

🔗 **Colab Demo**: [Try it here](https://colab.research.google.com/drive/1CVy7SVPOdCmIT8FoHQyhoCf_VqAaaqc9?usp=sharing)

**TaskWhiz** is an AI-powered chatbot assistant built for **TaskWhiz**, a SaaS platform that helps teams organize, manage, and track their projects and tasks — all in one place. The chatbot is designed to **reduce repetitive support queries** by providing fast, helpful, and context-aware answers to user questions.

---

## 💡 What It Does

The TaskWhiz chatbot acts as a virtual support assistant that can:
- Answer common questions using real product documentation
- Understand follow-up queries using recent conversation history
- Handle uncertainty gracefully with fallback messages
- Improve over time with user feedback and analytics

---

## 🔍 Key Features

- 🛠️ **Task Management** – Create tasks, assign members, set deadlines, and track progress.
- 📅 **Project Planning** – Use Kanban boards, timelines, and dependencies.
- 📈 **Reporting & Analytics** – Understand productivity trends across projects.
- 🔌 **Integrations** – Works with Slack, Google Calendar, Zapier, and more.
- 🔒 **Access Controls** – Role-based permissions for team collaboration.

---

## 🤖 How the Chatbot Works

### 🧠 Knowledge Base
The bot is grounded in 10–15 carefully curated markdown documents on key topics: features, pricing, onboarding, and troubleshooting.

### 🔄 Context-Aware Chat
It remembers the last few exchanges using **LangChain's `ConversationBufferWindowMemory`**, enabling meaningful follow-up answers.

### ❓ Fallback System
If the chatbot lacks enough context, it responds with:  
*“I'm not sure based on the available information. Could you clarify your question?”*

### 🔍 Smart Retrieval
- Uses **MiniLM embeddings via HuggingFace**
- Stores them in **ChromaDB** for fast, vector-based similarity search
- Applies **ContextualCompressionRetriever** and **Cohere’s reranker** for precision

### 🧾 Response Generation
- Powered by **Google’s FLAN-T5 (base)** model
- Uses a custom prompt template combining retrieved context + chat history + current question
- Generates clear, concise, and helpful responses

---

## 🧱 System Architecture

- **Document Loading**: `DirectoryLoader` loads `.md/.txt` docs from a zip archive  
- **Chunking**: `RecursiveCharacterTextSplitter` prepares docs for embedding  
- **Embedding & Storage**: `HuggingFaceEmbeddings` → `ChromaDB`  
- **Retrieval Pipeline**: Compression + reranking with Cohere  
- **LLM Integration**: `flan-t5-base` via LangChain with a custom `PromptTemplate`  
- **Memory**: Stores the last 3 turns of the conversation  

---

## 🧪 Prompt Engineering

```python
custom_prompt = PromptTemplate.from_template("""
You are an intelligent and helpful AI assistant for a SaaS product called TaskWhiz.

Your job is to answer user questions clearly, accurately, and helpfully, using:
- The retrieved context
- The recent conversation history

Rules:
- If the question is a follow-up, use past history to respond accurately.
- Never repeat the same advice multiple times.
- If unsure or context is lacking, respond: "I'm not sure based on the available information."
- Avoid overly short answers like "Yes." or "No." — provide helpful reasoning or links.
- Keep responses concise, but informative.
- Highlight key actions in **bold** when guiding users.

Chat History: {chat_history}

Relevant Context: {context}

Current Question: {question}

Answer:
""")

---




![Screenshot 2025-07-06 113504](https://github.com/user-attachments/assets/52c61800-2cab-46d9-880e-9ab704e99ad2)





![Screenshot 2025-07-06 113430](https://github.com/user-attachments/assets/17302dea-2524-45b0-a648-8c8842ebf7a0)


























