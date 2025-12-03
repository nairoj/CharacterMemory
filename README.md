# AI Character Memory System

A locally deployable AI character memory system that supports long-term memory, structured profile management, and agentic reflection.

[English](README.md) | [中文](README_ZH.md)

## 📂 Project Structure

```
d:\MyProj\character-memory\
├── data/                  # 💾 Runtime Data Storage
│   ├── profile.json       # Character profile (Name, Personality, Daily Log, etc.)
│   └── chroma_db/         # Vector Database (ChromaDB) for semantic memory retrieval
├── src/                   # 🧠 Source Code
│   ├── app.py             # Main Streamlit Application (Frontend & Entry Point)
│   ├── core/              # Core Logic
│   │   └── memory_manager.py # Manages profile, retrieval, and reflection logic
│   ├── models/            # Data Schemas
│   │   └── schema.py      # Pydantic models (CharacterProfile, MemoryItem, DailyLogEntry)
│   ├── services/          # External Services
│   │   └── llm_service.py # LLM Integration (OpenRouter/OpenAI)
│   └── storage/           # Data Access Layer
│       ├── json_store.py  # Handles profile.json operations
│       └── vector_store.py# Handles ChromaDB operations
├── docs/                  # Documentation
└── requirements.txt       # Python Dependencies
```

## 💾 Data Storage

-   **Profile Data**: Stored in `data/profile.json`. This file contains the character's structured state, including:
    -   Basic Info (Name, Occupation)
    -   Personality & Values
    -   Relationships
    -   **Daily Log** (Record of activities and interactions)
    -   Status (Health, Wealth)

-   **Memory Data**: Stored in `data/chroma_db`. This is a local vector database that stores:
    -   Conversation history (User inputs & AI responses)
    -   Observations and Thoughts
    -   Each memory is embedded for semantic search (RAG).

## 🚀 How to Run

```bash
streamlit run src/app.py
```

## ✨ Key Features

1.  **RAG Memory**: Retrieves relevant past memories based on the current conversation.
2.  **Agentic Reflection**:
    -   Click **"🛑 End Conversation & Reflect"** to trigger a self-reflection process.
    -   The AI analyzes the chat, updates its mood/relationships, and writes a **Daily Log** entry.
3.  **Real-time Timing**: Displays the execution time for Retrieval (RAG) and Generation (LLM) in the UI.
4.  **Advanced RAG (Parent-Child Indexing)**:
    -   **Threshold-based Summarization**:
        -   **Short (<300 chars)**: Stored directly to preserve detail and save costs.
        -   **Long (>300 chars)**: Automatically summarized by LLM. The **Summary** is indexed for search, but the **Original Content** is retrieved for context.
    -   **Daily Log Integration**: Daily logs are also vectorized (as `daily_log` type) to ensure long-term retrieval of past activities.
