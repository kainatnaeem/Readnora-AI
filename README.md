# 📖 ReadNora — AI-Powered PDF Assistant

> **ReadNora is an AI-powered document assistant that allows users to upload PDFs, ask questions about their content, and receive context-aware answers using Retrieval-Augmented Generation (RAG).**

ReadNora was built to explore how **RAG, vector databases, embeddings, LLMs, authentication, and conversational interfaces** can work together to create a practical AI application.

---

## ✨ Overview

Reading and understanding long PDF documents can be time-consuming.

ReadNora provides a simple conversational experience:

```text
📄 Upload a PDF
        ↓
🧠 Process the document
        ↓
🔢 Generate embeddings
        ↓
🗄️ Store them in ChromaDB
        ↓
💬 Ask a question
        ↓
🔍 Retrieve relevant information
        ↓
🤖 Generate an AI response
```

Instead of manually searching through a document, users can simply **ask questions in natural language**.

---

# 🚀 Key Features

### 📄 PDF Upload

Users can upload PDF documents directly through the application.

The document is processed and prepared for semantic search.

### 🧠 Retrieval-Augmented Generation

ReadNora uses **RAG** to retrieve relevant information from the uploaded document before generating an answer.

This allows the AI to respond using the actual content of the document.

### 🔍 Semantic Search

The document is converted into embeddings, allowing ReadNora to search for content based on **meaning**, rather than only matching exact keywords.

### 🗄️ ChromaDB

ChromaDB is used as the vector database for storing document embeddings and retrieving relevant chunks during question answering.

### 🤖 AI-Powered Answers

The retrieved document context is provided to an OpenAI model, which generates a natural-language response.

### 🔐 Authentication

Firebase Authentication is used to manage users securely.

### 💬 Conversational Chat

Users can continue asking questions within the same conversation.

Each conversation is identified using a unique `chat_id`.

### 🕘 Chat History

Conversations can be maintained separately, allowing users to return to previous chats without mixing messages between different conversations.

---

# 🧠 How RAG Works in ReadNora

The core of ReadNora is **Retrieval-Augmented Generation (RAG)**.

When a PDF is uploaded, the application follows this process:

### 1. Extract

Text is extracted from the PDF using **PyMuPDF**.

### 2. Chunk

The extracted text is divided into smaller pieces called **chunks**.

### 3. Embed

Each chunk is converted into a numerical representation called an **embedding** using Sentence Transformers.

### 4. Store

The embeddings are stored in **ChromaDB**.

### 5. Ask

The user asks a question about the document.

### 6. Retrieve

The question is converted into an embedding and compared with the stored document embeddings.

The most relevant chunks are retrieved.

### 7. Generate

The retrieved context and the user's question are provided to the AI model.

### 8. Respond

The model generates an answer based on the retrieved document context.

---

# 🏗️ Architecture

```text
                         USER
                           │
                           ▼
                  ┌─────────────────┐
                  │    Streamlit    │
                  │   User Interface│
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │     FastAPI     │
                  │     Backend     │
                  └────────┬────────┘
                           │
             ┌─────────────┴─────────────┐
             │                           │
             ▼                           ▼
      ┌──────────────┐           ┌────────────────┐
      │ PDF Processing│           │ Authentication │
      │   PyMuPDF     │           │    Firebase    │
      └───────┬──────┘           └────────────────┘
              │
              ▼
       ┌──────────────┐
       │    Chunks    │
       └───────┬──────┘
               │
               ▼
       ┌──────────────┐
       │  Embeddings  │
       │  Sentence    │
       │ Transformers │
       └───────┬──────┘
               │
               ▼
       ┌──────────────┐
       │   ChromaDB   │
       │ Vector Store │
       └───────┬──────┘
               │
          User Question
               │
               ▼
       ┌──────────────┐
       │   Retrieval  │
       └───────┬──────┘
               │
               ▼
       ┌──────────────┐
       │    OpenAI    │
       │  LLM / RAG   │
       └───────┬──────┘
               │
               ▼
             ANSWER
```

---

# 🛠️ Technology Stack

| Technology                  | Purpose                           |
| --------------------------- | --------------------------------- |
| **Python**                  | Core development                  |
| **FastAPI**                 | Backend and API layer             |
| **Streamlit**               | User interface                    |
| **PyMuPDF**                 | PDF text extraction               |
| **Sentence Transformers**   | Text embeddings                   |
| **ChromaDB**                | Vector database                   |
| **OpenAI**                  | AI response generation            |
| **Firebase Authentication** | User authentication               |
| **Firestore**               | User and conversation data        |
| **RAG**                     | Document-based question answering |

---

# 🖥️ Application Screens

## 🔐 Authentication

ReadNora provides an authentication flow that allows users to access their own conversations and data.

**Login Screen**

> Add your login screenshot here.

<img width="1366" height="768" alt="Screenshot (92)" src="https://github.com/user-attachments/assets/117b3cce-5b15-4b26-a89f-126041e54a15" />
<img width="1366" height="768" alt="Screenshot (93)" src="https://github.com/user-attachments/assets/9c0da6a4-27ed-4537-9c49-b012e351619f" />


---

## 📄 PDF Upload

After logging in, users can upload a PDF document and prepare it for AI-powered interaction.

> Add your PDF upload screenshot here.

<img width="1366" height="768" alt="Screenshot (95)" src="https://github.com/user-attachments/assets/2b5587bc-fdb4-4c5e-a902-1fe54aa3ccd7" />


---

## 💬 AI Chat

Once the document is processed, users can ask questions about its content.

The system retrieves relevant information from the PDF and uses it as context for generating the response.

> Add your chat screenshot here.




---

## 🧠 Context-Aware Answers

ReadNora doesn't simply generate a generic answer.

The RAG pipeline first searches the uploaded document for relevant information and then provides that context to the AI model.

> Add your answer/result screenshot here.

<img width="1366" height="768" alt="Screenshot (98)" src="https://github.com/user-attachments/assets/f49865a4-45c4-4322-b9fa-74146f970d27" />

---

## 🕘 Chat History

Each conversation is associated with a unique `chat_id`.

This allows multiple conversations to remain separate while new messages can continue inside an existing chat.

> Add your chat history screenshot here.

<img width="1366" height="768" alt="Screenshot (96)" src="https://github.com/user-attachments/assets/3582361d-ed6a-481c-9f73-603f3a8d027d" />

---

# 💬 Understanding `chat_id`

A `chat_id` identifies one particular conversation.

For example:

```text
User
│
├── Chat: abc123
│     ├── Question
│     ├── Answer
│     ├── Question
│     └── Answer
│
└── Chat: xyz789
      ├── Question
      └── Answer
```

When a user starts a new conversation, a new `chat_id` is created.

When the user returns to an existing conversation, the same `chat_id` is used so new messages are stored within that conversation.

This keeps chat history organized and prevents different conversations from being mixed together.

---

# 🔐 Authentication & User Data

ReadNora uses Firebase for authentication and user-related data management.

The basic flow is:

```text
User
 ↓
Firebase Authentication
 ↓
Firebase ID Token
 ↓
FastAPI
 ↓
Token Verification
 ↓
User UID
 ↓
User-specific Data & Chats
```

This allows the backend to identify the authenticated user and associate conversations with the correct account.

---

# 🎯 Why I Built ReadNora

ReadNora was created as a practical project to understand and implement modern AI application concepts beyond simply calling an LLM API.

The project combines:

* Retrieval-Augmented Generation
* Embeddings
* Vector databases
* Semantic search
* LLM integration
* REST APIs
* Authentication
* Conversation management
* Document processing

It demonstrates how these individual technologies can be combined into a complete AI-powered application.

---

# 📚 What This Project Demonstrates

Through ReadNora, I explored:

```text
Python
   ↓
FastAPI
   ↓
Document Processing
   ↓
Embeddings
   ↓
Vector Database
   ↓
RAG
   ↓
LLM
   ↓
Conversational AI
```

The project helped me understand not only how individual AI tools work, but also **how they communicate with each other inside a real application**.

---

# 🔮 Future Improvements

Some planned improvements include:

* 📚 Multiple PDF support
* 📌 Source citations for answers
* 🧠 Improved retrieval strategies
* 📊 Document analytics
* 🗂️ Better conversation organization
* ⚡ Streaming AI responses
* 🌐 Cloud deployment
* 📑 Support for additional document formats
* 🎙️ Voice-based interaction

---

# 🔒 Repository Note

This repository is a **public showcase of ReadNora**.

The source code and private configuration are intentionally not included in this repository.

This repository focuses on documenting the project's:

* Architecture
* Features
* AI/RAG workflow
* Technology stack
* User interface
* Development concepts

---

# 👩‍💻 Author

### Kainat Naeem

**Flutter Developer | AI & RAG Developer**

Interested in building practical applications with:

`Python` · `FastAPI` · `RAG` · `LLMs` · `Vector Databases` · `AI Agents`

---

## ⭐ ReadNora

> **Upload a document. Ask a question. Let AI find the answer.**

---
