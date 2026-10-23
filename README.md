RAG Document QnA Bot via Google Drive and Pinecone

An end-to-end, Langchain-powered AI Agent built in n8n. This workflow bridges the gap between your cloud storage and conversational AI. It automatically syncs documents from Google Drive into a Pinecone vector database and serves a conversational agent that can answer questions based on the ingested content.

Business and Operational Value
1. Automated Knowledge Syncing: No need to manually upload documents to the AI. When a new file is added to a specific Google Drive folder, it is automatically parsed, split, and embedded into the vector database.
2. Accurate Retrieval (RAG): The AI Agent accesses a Vector Store QnA tool to pull verified context directly from Pinecone before answering, significantly reducing hallucinations.
3. Computation Capabilities: Includes a Calculator tool allowing the agent to perform on-the-fly math based on the data retrieved (e.g. aggregating costs or calculating deductions found in policies).

Tech Stack and Key Nodes
1. Framework: n8n Advanced AI (Langchain)
2. Data Ingestion Source: Google Drive (Trigger and File Download)
3. Document Processing: PDF Data Loader and Recursive Character Text Splitter
4. Vector Database: Pinecone (Insert and Retrieval)
5. LLM and Embeddings: OpenAI (gpt-4o-mini, text-embedding-ada-002)
6. Agent Tools: Vector Store QnA Tool (For RAG) and Calculator Tool (For mathematical reasoning)

Execution Flow
Flow 1: Data Ingestion (Left side of workflow)
1. Trigger: Google Drive Trigger monitors a designated folder for new files every minute.
2. Download and Process: New PDFs are downloaded, parsed via Default Data Loader, and split into optimal chunks via Recursive Character Text Splitter.
3. Embed and Store: OpenAI Embeddings are generated, and chunks are stored securely into the PineconeVectorStore.

Flow 2: AI Agent and Retrieval (Right side of workflow)
1. Trigger: A user sends a message via the Chat interface or Webhook.
2. Agent Processing: The AI Agent receives the prompt. If the question requires factual knowledge, the agent delegates the query to the Vector Store QnA Tool.
3. Semantic Search: The Vector tool queries Pinecone to find the most relevant document chunks.
4. Synthesis and Response: The Agent synthesizes the retrieved chunks into a concise, accurate response and returns it to the user.
