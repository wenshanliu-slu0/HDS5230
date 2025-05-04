# Put directory structure here!


Directories:  </br>
./ - This is the top-level directory for the project.   </br>
./Config - constant.py </br>
./data -      </br>
./doc - ReadME.md  </br>
./src -   </br>

<pre>```
├── Config
│ └── constant.py
├── data
├── doc
│ └── ReadME.md
├── src
└── README.md
``` </pre>

#### ====== Below will be placed in Doc folder! ======
# Breast Cancer QA Chatbot 

Authors: 

Date: May 1, 2025

---

### Objective

This project demonstrates a unique **Question Answering (QA) chatbot** for breast cancer-related content using **transformer-based language models**. The chatbot is capable of understanding user queries and extracting relevant answers from a predefined breast cancer corpus. This showcases the potential application of a **Retrieval Augmented Generation (RAG)** along with **Natural Language Processing (NLP)** in supporting:

- Medical education  
- Patient-centered health information  
- Clinical decision support  

---


### Real-World Scenario

This QA chatbot can be deployed in real-world healthcare or public health contexts to address common information gaps related to breast cancer. 

Here are a few potential use cases:

- **Patient Portals and Hospital Websites**  
  Patients often ask "What are the early signs of breast cancer?" or "How is breast cancer diagnosed?". Instead of searching through lengthy papers or waiting for doctor visits, people may connect with our chatbot to get correct, simple real-time responses—thereby increasing involvement and lowering misunderstanding.

- **Clinical Decision Support for Health Professionals**  
  During consultations or training sessions, healthcare professionals, teachers, or students may utilize the chatbot as a fast reference tool to find definitions, recommendations, or treatment choices so improving decision-making efficiency with medically based replies.

- **Community Health & Awareness Campaigns**  
  Especially in low-resource environments where professional personnel may not be easily available, this application may act as a virtual assistant to address frequently requested questions in a reliable and accessible way during breast cancer education or outreach activities.

By providing immediate, accurate responses drawn from reliable sources like the National Cancer Institute, this chatbot helps to:
- **Reduce misinformation**
- **Alleviate workload on medical staff**
- **Promote health literacy among diverse populations**


---

### Dataset Info

**Source:**

- All content is sourced from the official [National Cancer Institute XML sitemap](https://www.cancer.gov/sitemaps/pageinstructions.xml), which contains hundreds of links to educational pages about breast cancer. While the sitemap includes both PDF and HTML resources, the application primarily retrieves **HTML pages**, which are more structured and easier to parse for QA purposes.

The system uses `WebBaseLoader` to crawl and load these HTML documents, skipping over non-text resources such as videos or PDFs.

**Content:**

- Extracted HTML content includes information on breast cancer prevention, diagnosis, screening, treatment, etc.
- Each document is split into smaller chunks for embedding and retrieval.
- These chunks form the internal **domain-specific knowledge base** used to answer user questions.


**Usage:**

- When a user asks a question, the system compares it to the vectorized text from cancer.gov PDFs and selects the most semantically relevant passage.
- The most semantically relevant content is retrieved and passed to `gpt-4o-mini`, which then generates a natural language answer grounded in the selected content.
- If the internal knowledge base returns no relevant results, the system optionally queries **PubMed** for external biomedical literature.


---

### Data Science & Model Architecture


This application uses a unified LLM-driven pipeline centered on **OpenAI's GPT-4o-mini**, which handles all stages of question interpretation, document reading, and answer generation.


- **1. Semantic Retrieval with OpenAI Embeddings**  
  To find relevant context for a user question, the system uses **`OpenAIEmbeddings()`** (via `langchain_openai`) to convert both the question and document chunks into dense vector representations. 


- **2.1 Answer Generation with GPT-4o-mini**  
  This main agent uses **`gpt-4o-mini`**, accessed via `ChatOpenAI`, to:

  - Interpret the question
  - Read retrieved document context
  - Generate natural language answers
  - Optionally reformulate or clarify the question (agent-style reasoning)

- **2.2 Answer Generation with PubMed**
  
  If the main agent retriever (based on National Cancer website) fails to return relevant results—for example, if the context is missing or similarity scores are too low—the system automatically invokes a second agent powered by the **LangChain PubMed Retriever**.


  This second agent:
  
  - Queries the top5 relevant literature from **PubMed**
  - Uses GPT-4o-mini to read retrieved abstracts
  - Synthesizes a relevant, concise answer based on the scientific findings


---

### How to run this Application?
Before run the application, download `breast_cancer_QA_chatbot_demo.ipynb` and `constant.py` and then upload to your own `Google Drive` folder. 
Please make sure both of them are in the same folder.

0. Enter your ChatGPT API Key informatation in `constant.py` file.
1. Run in Jupyter Notebook `breast_cancer_QA_chatbot_demo.ipynb` by using `Google Colab`.
2. When the code run the end, the `gradio` service will be set up and gradio user interface will be launched.
3. You will see a chat window with:

    - A textbox to enter your question
    - A “Clear Chat” button to reset the conversation
    - Type your question about breast cancer (e.g., "What are the symptoms of breast cancer?")
    - Press `Enter`.      
    - The chatbot will display the reply in the chat window

Example:
![alt text](<./Picture/CleanShot.jpg>)


---

### Demo Video

https:
