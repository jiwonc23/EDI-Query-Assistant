# EDI-Query-Assistant

RAG architecture in Phase I is finished. Phase II will be enhanced with Agentic AI to handle advanced analysis service with AutoGen and Magentic-One. Of course, gpt-4o might be replaced with DeekSeek R1 after evaluating the performance.
 
Here’s how our RAG architecture delivers smarter insights:
 
RAG Architecture Overview

1. User Query in Microsoft Teams
 - A user types a natural language question into Teams, which is forwarded to an AI Bot Service endpoint.

2. Conversation Analysis with CLU
 - The AI Bot Service calls Azure Conversational Language Understanding (CLU) to parse the message.
 - CLU extracts key entities, intent, and context from the user query. These insights help steer how the query is processed downstream.

3. Vector-Based Retrieval with Azure AI Search
 - In the background, Azure AI Search continuously indexes business transaction data stored in Cosmos DB.
 - Through an indexing scheduler, the data is converted into vector embeddings, making it searchable for semantic matches.
 - When CLU’s analysis completes, the system constructs a search query (including relevant context) and retrieves the top-matching results from Azure AI Search’s vector index.

4. Contextual Response Generation with OpenAI GPT-4
 - The retrieved data and the original user query are passed to Azure OpenAI (GPT-4).
 - GPT-4 synthesizes a response, using both the user’s question and the business data from Azure AI Search.
 - This blending of user context and domain knowledge ensures answers are accurate, relevant, and natural-sounding.

5. Returning the Answer
 - The AI Bot Service receives GPT-4’s response and sends it back to Teams, completing the conversation loop.
 - Logic Apps or Azure Functions can be used for orchestration and any custom business or helper logic in between.

TODO: 
- Prompt Engineering for delivering more insights from retrieved data.
- Evaluation for latest model such as o3-mini and R1.
- Enhancing training CLU model for more intents and entities to cover further query requiring analysed report.