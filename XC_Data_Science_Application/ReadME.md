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


This application leverages a **NLP pipeline** that integrates three key components—**semantic retrieval**, **extractive question answering**, and **generative LLM reasoning**—to accurately answer breast cancer–related questions in real time.


- **1. Semantic Embedding & Retrieval**  
  The system uses `sentence-transformers` (`all-MiniLM-L6-v2`) to embed both user queries and text passages from cancer.gov PDFs. In addition, `cosine similarity` is used to retrieve the most semantically relevant context.

- **2. Extractive QA with Hugging Face Transformers**  
  Once the most relevant passage is found, the system uses `distilbert-base-uncased-distilled-squad`—a fast and efficient question-answering model from Hugging Face—to pick out the **exact part of the text** that answers the user’s question.  
  This method works especially well when the answer is written directly or very closelys in the source passage, giving users quick and accurate responses.


- **3. LLM Reasoning with OpenAI GPT-4o-mini**  
  For complex reasoning or rephrased answers, the system uses OpenAI’s `gpt-4o-mini` model (via `ChatOpenAI`) with temperature set to `0.0`, ensuring factual consistency and minimal hallucination. This enables natural, human-like response generation while staying grounded in the retrieved medical content. In addition, to enhance the chatbot's capability beyond exact span extraction, this application integrates OpenAI’s `gpt-4o-mini` model using the `ChatOpenAI` interface (via LangChain).



---

### How to run this Application?

1. Run in Jupyter Notebook `breast_cancer_QA_chatbot_demo.ipynb`
2. When the code run the end, the `gradio` service will be set up and gradio user interface will be launched
3. Use the web interface, and type in the quastion, and press `enter`

Example:
![alt text](<./Picture/CleanShot.jpg>)


---

### Demo Video

https:
