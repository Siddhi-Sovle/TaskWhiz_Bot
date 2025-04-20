# TaskWhiz - The Smart Project & Task Management Chatbot
TaskWhiz, an AI-powered chatbot assistant designed to help users with all things related to TaskWhiz, the SaaS project management platform. TaskWhiz helps teams organize, manage, and track their projects, tasks, and collaboration efforts, all in one place. This platform's goal is to reduce repetitive support requests and help users get quick answers to their questions!

Key Features:
🛠️ Task Management: Create tasks, set priorities, assign team members, and track progress.
📅 Project Planning: Use Kanban boards, timelines, and task dependencies to streamline project workflows.
📈 Analytics & Reporting: Get project insights, track productivity.
🔌 Third-party Integrations: Easily integrate with tools like Slack, Google Calendar, and Zapier.
🔒 Security & Permissions: Set team roles and permissions to maintain control over your workspace.


How Does TaskWhiz Chatbot Work?

Knowledge Base
The chatbot pulls from a carefully crafted knowledge base that contains product documentation. The base includes 10–15 documents on key topics such as features, pricing, troubleshooting, and more.
Context-Aware Conversations
The bot remembers previous messages in the conversation, so it can provide personalized, relevant answers based on what’s been asked before.
Fallback Mechanism
If the bot doesn’t know the answer, it politely responds with a fallback message: "I'm not sure based on the available information. Could you clarify your question?"
Advanced Search & Retrieval
Using ChromaDB and HuggingFace embeddings, the bot retrieves the most relevant information from the knowledge base to answer your questions.
Language Model
The core of TaskWhiz is the flan-t5-base model. It takes your question + relevant docs + chat history and returns a natural, helpful answer.


Analytics and Tracking:

Question Categories: The chatbot logs which topics are asked the most (e.g., pricing, integrations, setup).
Fallbacks: It tracks when a fallback message is triggered, helping us improve responses.
User Feedback: After each answer, users are asked if the response was helpful. This feedback is collected to continuously improve the bot.


System Architecture:

Document Loading:
We use DirectoryLoader from langchain_community to load .md or .txt files containing the product knowledge from a ZIP archive. The documents are then split into chunks using RecursiveCharacterTextSplitter for efficient retrieval.

Embedding & Vector Store:
We use HuggingFaceEmbeddings with the MiniLM model to convert the product knowledge into embeddings. Chroma is used to store the embeddings and provide efficient retrieval using nearest-neighbor search.

Retriever & Reranking:
A ContextualCompressionRetriever is employed to compress the retrieved documents and improve response accuracy. Cohere's rerank model is used for context-aware reranking of the top results.

LLM for Response Generation:
Google's FLAN-T5 model is used to generate answers based on the context and chat history. A custom PromptTemplate ensures that the generated answers are clear, accurate, and concise.

Memory:
The chatbot uses ConversationBufferWindowMemory to store the last 3 exchanges, enabling context retention for follow-up questions.

Fallback Mechanism: 
If the response is uncertain or too vague, a fallback message is triggered to guide the user for clarification.


Design Decisions:

Each part of the system, from document loading to response generation, is modular, allowing for easy adjustments and scaling. The use of both recent conversation history and document context ensures that answers are not only relevant but personalized.


Prompt Engineering Approach:

This is the prompt that was used, and below it is given what it infers-

custom_prompt = PromptTemplate.from_template("""
You are an intelligent and helpful AI assistant for a SaaS product called **TaskWhiz**.

Your job is to answer user questions **clearly, accurately, and helpfully**, using:
- The **retrieved context**
- The **recent conversation history**

Rules:
- If the question is a follow-up, use past history to respond accurately.
- Never repeat the same advice multiple times.
- If unsure or context is lacking, respond: "I'm not sure based on the available information."
- Avoid overly short answers like "Yes." or "No." — provide helpful reasoning or links.
- Keep responses concise, but informative.
- Highlight key actions in **bold** when guiding users.

---

Chat History:
{chat_history}

Relevant Context:
{context}

Current Question:
{question}

Answer:
""")

User Instructions: The AI is clearly instructed to answer clearly, accurately, and helpfully.
Chat History: Previous exchanges are included to maintain context.
Relevant Context: The model is provided with the relevant knowledge retrieved from the document base.
Fallback Instructions: The prompt explicitly tells the AI how to handle uncertainty or lack of context by offering helpful clarification or defaulting to "I'm not sure" if necessary.


Rules for Answering:

If the question is a follow-up, the AI should utilize past history to provide an accurate and context-aware response.
Avoid repetitive advice, ensuring that answers are fresh and avoid redundancy.
Concise but informative responses: The model must keep answers to the point, but also make sure that the answer provides enough detail to resolve the user’s query.
Highlight key actions in bold when providing guidance, making it easier for users to follow important steps or suggestions.


Limitations:
The chatbot is limited to answering questions based on the knowledge base provided. If it doesn't know something, it will say, "I'm not sure."
It can't process real-time data or dynamic updates from external systems like your TaskWhiz account.


What’s Coming Next?
Multi-Language Support: Extend the chatbot’s reach to a global audience.
Advanced Analytics: Track deeper insights, like user satisfaction and behavior trends.
Web/ Mobile Interface: Make TaskWhiz available on more platforms for easy access.



![image](https://github.com/user-attachments/assets/97e50d6b-f969-433a-a685-64d30ca41e02)
































