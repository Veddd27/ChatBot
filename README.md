# LangGraph Chatbot

A conversational chatbot built with [LangGraph](https://github.com/langchain-ai/langgraph) and Streamlit, featuring persistent multi-thread conversation history and real-time streaming responses.

## Features

- **Stateful conversation graph** — built as a LangGraph `StateGraph` with a single chat node powered by OpenAI's chat models
- **Persistent chat history** — conversations are checkpointed to a local SQLite database via `SqliteSaver`, so chats survive app restarts
- **Multiple conversation threads** — start new chats and switch between past conversations from the sidebar, each with its own `thread_id`
- **Streaming responses** — assistant replies are streamed token-by-token using `st.write_stream`

## Tech Stack

- Python
- [LangGraph](https://github.com/langchain-ai/langgraph) — state graph orchestration
- [LangChain](https://github.com/langchain-ai/langchain) — message types and OpenAI integration
- [Streamlit](https://streamlit.io/) — chat UI
- SQLite — conversation checkpointing/persistence

## Project Structure

```
ChatBot/
├── app.py                          # Main app — streaming + persistent multi-thread chat
├── langgraph_database_backend.py   # LangGraph graph + SQLite checkpointer
├── requirements.txt                # Python dependencies
├── .env.example                    # Environment variable template
└── iterations/                     # Earlier build steps, kept to show progression
    ├── langgraph_backend.py             # Step 1 — basic in-memory chatbot
    ├── streamlit_frontend_streaming.py  # Step 2 — added token streaming
    └── streamlit_frontend_threading.py  # Step 3 — added multi-thread chat (in-memory)
```

## Setup

1. Clone the repo and install dependencies:
```bash
   pip install -r requirements.txt
```

2. Copy `.env.example` to `.env` and add your OpenAI API key:
```bash
   cp .env.example .env
```

3. Run the app:
```bash
   streamlit run app.py
```

## How It Works

The core of the app is a LangGraph `StateGraph` with a single `chat_node` that calls an OpenAI chat model and appends the response to conversation state. Each conversation is tied to a `thread_id`, and LangGraph's `SqliteSaver` checkpointer persists the full message history for every thread to `chatbot.db`. The Streamlit sidebar lists all past threads (loaded via `retrieve_all_threads()`), letting you resume any previous conversation, while new messages stream back token-by-token for a responsive chat experience.

## Status

## Status

Actively maintained — planned next steps include tool-calling nodes, RAG integration, and multi-agent workflows.