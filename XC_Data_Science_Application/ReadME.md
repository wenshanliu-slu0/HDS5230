# Breast Cancer QA Chatbot 

Authors: 

Date: May 1, 2025

### Objective

This project demonstrates a simple **Question Answering (QA) chatbot** for breast cancer-related content using **transformer-based language models**. The chatbot is capable of understanding user queries and extracting relevant answers from a predefined breast cancer corpus. This showcases the potential application of **Natural Language Processing (NLP)** in supporting:

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

- All documents are retrieved from the official [National Cancer Institute XML sitemap](https://www.cancer.gov/sitemaps/pageinstructions.xml), which links to multiple PDF documents related to breast cancer prevention, screening, treatment, and survivorship.

**Content:**

- The application extracts text content from PDF files found in the sitemap.
- These documents serve as the domain-specific knowledge base for the QA system.
- Each passage is embedded using sentence-transformer models for similarity search.

**Usage:**

- When a user asks a question, the system compares it to the vectorized text from cancer.gov PDFs and selects the most semantically relevant passage.
- A transformer-based QA model then extracts a concise answer from that passage.

---

### Data Science & Model Architecture


This application uses a unified LLM-driven pipeline centered on **OpenAI's GPT-4o-mini**, which handles all stages of question interpretation, document reading, and answer generation.


- **1. Semantic Retrieval with OpenAI Embeddings**  
  To find relevant context for a user question, the system uses **`OpenAIEmbeddings()`** (via `langchain_openai`) to convert both the question and document chunks into dense vector representations. 


- **2. Answer Generation with GPT-4o-mini**  
  The chatbot uses **`gpt-4o-mini`**, accessed via `ChatOpenAI`, to:

- Interpret the question
- Read retrieved document context
- Generate natural language answers
- Optionally reformulate or clarify the question (agent-style reasoning)
  
This design results in a fully OpenAI-powered QA pipeline, with no Hugging Face models or sentence-transformers involved in embedding or answering.

---

### How to run this Application?

1. Run in Jupyter Notebook `breast_cancer_QA_chatbot_demo.ipynb`
2. When the code run the end, the `gradio` service will be set up and gradio user interface will be launched
3. You will see a chat window with:

    A textbox to enter your question
    A “Clear Chat” button to reset the conversation
    Type your question about breast cancer (e.g., "What are the symptoms of breast cancer?")
    Press Enter.      
The chatbot will display the reply in the chat window

Example:
![alt text](<./Picture/CleanShot.jpg>)


---

### Demo Video

https:
