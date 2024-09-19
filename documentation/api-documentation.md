| Description              | API Endpoint
| :---------------- | :------ | 
| Fetch the database entries for the text chunk table        |   `http://localhost:4004/odata/v4/embedding-storage/DocumentChunk`  |
| Trigger the document chunking, creation of the embeddings and storing them as embeddings in the SAP HANA Cloud vector engine        |   `http://localhost:4004/odata/v4/embedding-storage/storeEmbeddings()`  |
| Delete the vector embeddings from the SAP HANA Cloud vector engine        |   `http://localhost:4004/odata/v4/embedding-storage/deleteEmbeddings()`  |
| Get the RAG response from the AI partner model        |   `http://localhost:4004/odata/v4/roadshow/getRagResponse()`  |
| Execute a similarity search        |   `http://localhost:4004/odata/v4/roadshow/executeSimilaritySearch()`  |