# tiny-jarvis
A chatbot that can answer questions based on the content of a provided PDF document

## 1. **Objective**

Create a chatbot that can answer questions based on the content of a provided PDF document. If the chatbot cannot find the answer in the PDF, it should respond:

"Sorry, I didn’t understand your question. Do you want to connect with a live agent?"

---

## **Functionality**

### 1. **PDF Understanding**
- The chatbot loads the provided PDF and use its content as the knowledge base.
- It accurately retrieves and displays answers from the PDF content.

### 2. **Fallback Response**
- If the chatbot cannot find the answer in the PDF, it provides a fallback response:
  "Sorry, I didn’t understand your question. Do you want to connect with a live agent?"

### 3. **User Interaction**
- Developed an interface (text-based or graphical) where users can ask questions and receive responses.
- Ensured the interaction is clear and intuitive.
- 
---


## 2. **Documentation**

## **Piping and Instrumentation Diagram (P&ID): End-to-End Design of AI Bot**
![Piping and Instrumentation Diagram](https://drive.google.com/uc?id=1A-Y2fCpNg9gwFDn4RnXdqQLw2_AzakPC)

Overall Design

**Correction** : Result--> INTO --> Summarizer (BART) will also be in backend



Above diagram illustrates the architecture and workflow for an AI chatbot designed to answer questions based on documents like PDFs, DOCs, and TXT files. Here's an explanation of the components:

---

### **1. Data Source**
- **Input Formats:** The user uploads files in supported formats:
  - **PDF** : Implemented
  - **DOC** : Can be extended to
  - **TXT** : Can be extended to
- **Purpose:** These files act as the knowledge base for the chatbot.

---

### **2. Data Parsing**
- **Chunking:**
  - The uploaded documents are broken down into smaller, manageable chunks (e.g., `chunk01`, `chunk02`, etc.).
  - **Reason:** This helps in processing and embedding the text more efficiently for querying.

---

### **3. Embedding Models**
- **Purpose:** Convert the text chunks into vector embeddings, which are mathematical representations of the text.
- **Process:**
  - Each chunk is processed using a pre-trained **embedding model**. In my small project, I used SentenceTransformer
\*[Sentence Transformer Documentation](https://www.canva.com/design/DAGX6P98jv0/_hkeMRWL92X_AQCRPkP76Q/edit?utm_content=DAGX6P98jv0&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)*
  - Outputs are **vector embeddings**, which capture the semantic meaning of the text.

---

### **4. Data Warehouse (Storage)**
- **Embedded Text Corpus:**
  - The embeddings are stored in a database for efficient retrieval.
  - Example: For PDF1, embeddings might include sentences like "Approval of class...".

---

### **5. Vector Database**
- **Examples:** Tools like **Pinecone** or **SingleStore** are used. I have used **Pinecone**.
- **Functionality:**
  - The vector embeddings from the embedding model are stored in this database.
  - This allows for fast similarity searches when a user query is processed.

---

### **6. Query Processing**
- **User Query:**
  - The user inputs a query (e.g., "What is date of exam ...?").
  - The query is embedded into a vector format using the same embedding model.
- **Cosine Similarity:**
  - The vectorized query is compared with the stored embeddings using cosine similarity to determine relevance.

---

### **7. Results**
- **Similarity Scores:**
  - Result tokens are ranked based on how closely they match the query (e.g., token1: 0.98, token4: 0.79, etc.).
  - These results are presented to the user in descending order of similarity.

---

### **8. User Interface**
- **Purpose:** Provides an intuitive platform for user interaction.
- **Features:**
  - Users can input queries and view responses.
  - Can be extended to more sophasticated user interactions and UI
---

### **Backend (Highlighted in the Diagram)**
- The backend handles:
  - Parsing and embedding the uploaded documents.
  - Storing embeddings in a vector database.
  - Processing user queries and retrieving results based on similarity.

---

This architecture ensures efficient and accurate question-answering while maintaining user-friendly interaction through fallback mechanisms and feedback loops.

## Models Used 

### Sentence-transformer
#### Sentence Transformer Architecture

Sentence Transformers are built on top of transformer-based models (such as BERT, RoBERTa, or DistilBERT) and are specifically designed for tasks that require sentence or text embeddings. The model generates dense vector representations of sentences that capture their semantic meaning, making them ideal for tasks like semantic search, clustering, and text similarity analysis. The architecture uses techniques like **Siamese networks** and **triplet loss** to train the model on sentence pairs, optimizing it for producing meaningful sentence-level embeddings.

![Sentence Transformer Architecture](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*fhd9gsQGBcPWduThINIIUQ.png)

 [Sentence Transformers](https://sbert.net/).

 ### Facebook BART Architecture

BART (Bidirectional and Auto-Regressive Transformers) is a sequence-to-sequence model that combines the strengths of BERT's bidirectional encoder and GPT's autoregressive decoder. It is trained using a denoising autoencoder approach, where the model learns to reconstruct corrupted text. BART excels at tasks like text summarization, generation, and translation due to its ability to both understand and generate text. Its hybrid architecture allows it to perform well on a variety of natural language processing tasks, making it a versatile and powerful tool in NLP.

![Sentence Transformer Architecture](https://production-media.paperswithcode.com/methods/Screen_Shot_2020-06-01_at_9.49.47_PM.png)

 [BART Docs](https://huggingface.co/docs/transformers/en/model_doc/bart).

 ## DataBase
 ### Setting Up Pinecone for Storing Embeddings

Pinecone is a fully managed vector database designed for similarity search and machine learning applications. It allows you to store, index, and search vector embeddings at scale. Pinecone makes it easy to manage and query large collections of high-dimensional vectors, such as embeddings generated from text or images, without needing to manage the underlying infrastructure.

#### What is Pinecone?

Pinecone is a cloud-native vector database that provides a high-performance platform to store, search, and retrieve vector embeddings. It is optimized for applications such as:

- **Semantic Search**: Quickly retrieving relevant documents based on the similarity of their embeddings.
- **Recommendation Systems**: Finding similar items (e.g., products, movies) based on user preferences or item characteristics.
- **Anomaly Detection**: Identifying outliers by comparing vectors in a database.

![Sentence Transformer Architecture](https://miro.medium.com/v2/resize:fit:1200/1*4Z90ZgAq7nDdkuWe1bWnlg.jpeg)

 [Vector Databases](https://www.pinecone.io/learn/vector-database/).

 ## **Conclusion**

The **Tiny-Jarvis** chatbot serves as an intelligent, document-based Q&A system, leveraging advanced NLP models like **Sentence-Transformers** and **BART** for precise query matching and summarization. Its integration with **Pinecone** ensures fast and efficient similarity search, providing users with accurate answers in real-time. This end-to-end solution demonstrates a practical approach to building AI-driven, document-aware chatbots, offering seamless user interaction and reliable fallback support. Future enhancements could include support for additional file formats, multi-lingual support, and a more interactive user interface for an even better experience.
