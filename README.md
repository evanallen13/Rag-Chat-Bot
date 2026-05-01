# Rag-Chat-Bot

Rag-Chat-Bot is a Retrieval-Augmented Generation (RAG) chatbot that uses OpenAI's GPT-4 plus `text-embedding-ada-002` to answer questions strictly from a custom chat dataset stored in a persistent ChromaDB collection.

## Features

- Loads chat data from a CSV file.
- Generates embeddings with OpenAI and stores them in a persistent ChromaDB collection on disk.
- Retrieves the top-k most relevant chats for each query via semantic search.
- Generates answers with GPT-4, constrained to the retrieved context.

## Setup

1. **Clone the repository** and open it in VS Code (recommended — a Dev Container config is included).

2. **Install dependencies**:

   ```sh
   pip install -r requirements.txt
   ```

3. **Set your OpenAI API key** by creating a `.env` file in the project root:

   ```
   OPENAI_API_KEY=your_openai_api_key
   ```

4. **Provide a chat CSV** at `data/chat_training_2.csv`. The script reads column index 1 as the chat id and column index 4 as the chat text.

5. **Run the chatbot**:

   ```sh
   python chatbot.py
   ```

## Usage

When started, the chatbot will:

1. Load the chats from `data/chat_training_2.csv`.
2. Embed each chat and store it in a persistent ChromaDB collection (under `./chroma_db`).
3. Prompt you for a query — type `exit` or press Enter on an empty prompt to quit.
4. For each query, retrieve the 3 most similar chats and have GPT-4 answer using only that context.

## Files

- `chatbot.py` — Main script (CLI loop, embedding, retrieval, generation).
- `data/` — Place your chat CSV here.
- `requirements.txt` — Python dependencies.
- `.devcontainer/` — VS Code Dev Container configuration.
