## Attempt to run a LLM based chatbot locally
This Jupyter Notebook implements a demo chatbot for handling return policy-related queries.

### Installation
You need to download the pre-trained LLM model `llama-2-7b-chat.ggmlv3.q8_0.bin` in https://huggingface.co/TheBloke/Llama-2-7B-Chat-GGML/blob/main/llama-2-7b-chat.ggmlv3.q8_0.bin and put it into the root directory of this project if you want to run the notebook.

### Summary of the methodology
1. Loading and Preprocessing:
The code uses the DirectoryLoader from the langchain.document_loaders module to load return policy documents stored as text files.
The text content of the documents is split into smaller chunks using the RecursiveCharacterTextSplitter from the langchain.text_splitter module.
The text chunks are then embedded using the Hugging Face pre-trained model specified as "sentence-transformers/all-MiniLM-L6-v2".

2. Building a Local Vector Database:
The embedded text chunks are used to create a local vector database using the FAISS library (langchain.vectorstores.FAISS).
The vector database is saved locally for future use.

3. Setting up the Language Model:
A template is defined for prompting the AI with context and a question.
The LLM (Language Learning Model) is loaded using the CTransformers class from the langchain.llms module, with the specified model and configuration.
The interpreted information from the local database is loaded, including the embeddings and the FAISS database.

4. Creating the Chatbot:
The local database is transformed into a retriever using the as_retriever method.
A prompt template is created for generating prompts to the AI model.
The RetrievalQA class from the langchain.chains module is used to create a chatbot instance, which combines the LLM, retriever, and prompt template.
The chatbot is configured to return source documents as part of the answer.

5. Asking Questions:
The query function is defined to interact with the chatbot.
The function takes a question and the chatbot model as inputs.
The chatbot model is invoked with the question, and the response is displayed.

### Architecture of the system
![Local LLM drawio](https://github.com/gwu1/local-llm-chatbot/assets/2475857/070ca990-aac8-4781-af95-2b5adf0661cf)


The flow of information when the user interacts with the system is as follows:

1. The User Input, which can be a query or a question, is provided to the system.
2. The Retriever component interacts with the Local Vector Database to retrieve relevant passages based on the User Input.
3. The retrieved passages, along with the User Input, are provided to the Language Model (LLM) for generating a response.
4. The Language Model (LLM) processes the retrieved passages and User Input to generate the final response.
5. The response is returned to the user.

