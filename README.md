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