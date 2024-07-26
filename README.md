# GraphRAG with AutoGen, Chainlit and Ollama
Microsoft’s GraphRAG with AutoGen, Ollama and Chainlit to run a local Multi-Agent RAG bot

This application integrates GraphRAG with AutoGen agents, powered by local LLMs from Ollama, for a offline embedding and inference. Key highlights include:

Agentic-RAG: - Integrating GraphRAG's knowledge search method with an AutoGen agent via function calling.
Offline LLM Support: - Configuring GraphRAG (local & global search) to support local models from Ollama for inference and embedding.
Non-OpenAI Function Calling: - Extending AutoGen to support function calling with non-OpenAI LLMs from Ollama via Lite-LLM proxy server.
Interactive UI: - Deploying Chainlit UI to handle continuous conversations, multi-threading, and user input settings.

Retrieval-augmented generation (RAG) is a powerful tool that equips large language models (LLMs) with the ability to access real-world data for more informed responses. This is achieved by integrating the models with a vector database for real-time learning and adaptation. This feature makes RAG a preferred choice for chatbot applications where the requirement for accurate and grounded responses in near real-time responses is the goal. An advanced variant of this, known as Graph Retrieval-Augmented Generation (GraphRAG), merges the benefits of graph-based knowledge retrieval with LLMs, further enhancing the capabilities in natural language processing. Unlike traditional RAG methods that rely on vector similarity searches, GraphRAG constructs a structured knowledge graph from raw text, capturing entities, relationships, and critical claims. This can enhance the LLMs’ ability to understand and synthesize complex datasets and their relationships, yielding greater accuracy and contextually grounded responses.

This repository will guide you through constructing a multi-agent AI application with a GraphRAG retrieval system, which operates on your local machine. The key components of this application are:
> GraphRAG’s knowledge search methods are integrated with an AutoGen agent via function calling.
> GraphRAG (local & global search) is configured to support local models from Ollama for inference and embedding.
> AutoGen is extended to support function calling with non-OpenAI LLMs from Ollama via the Lite-LLM proxy server.
> Provide a Chainlit UI for continuous conversations, multi-threading, and user input settings.
> 

![Flow Diagram](https://github.com/Netizine/GraphRAG_AutoGen/blob/main/images/flow_diagram.jpg?raw=true)

## Installation and Setup on Windows

Follow these steps to set up and run AutoGen and GraphRAG Local with Ollama and Chainlit UI on Windows:
1. Install LLMs:
   Visit **[Ollama's](https://ollama.com/download/windows)** website for installation files.
   ```
   ollama pull mistral
   ollama pull nomic-embed-text
   ollama pull llama3.1
   ollama serve
   ```
2. Create python environment and install packages:
   ```
   git clone https://github.com/Netizine/GraphRAG_AutoGen.git
   cd GraphRAG_AutoGen
   python -m venv venv
   ./venv/Scripts/activate
   pip install -r requirements.txt
   ```
3. Initiate GraphRAG root folder:
   ```
   mkdir input
   python -m graphrag.index --init  --root .
   cp ./utils/settings.yaml ./
   ```
4. Replace 'embedding.py' and 'openai_embeddings_llm.py' in the GraphRAG package folder using files from Utils folder:
   ```
   cp ./utils/openai_embeddings_llm.py .\venv\Lib\site-packages\graphrag\llm\openai\openai_embeddings_llm.py
   cp ./utils/embedding.py .\venv\Lib\site-packages\graphrag\query\llm\oai\embedding.py 
   ```
5. Create embeddings and knowledge graph:
   ```
   python -m graphrag.index --root .
   ```
6. Start the Lite-LLM proxy server:
   ```
   litellm --model ollama_chat/llama3.1
   ```
7. Run the app:
   ```
   chainlit run appUI.py
   ```


