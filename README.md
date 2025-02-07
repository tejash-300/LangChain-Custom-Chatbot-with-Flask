# LangChain Custom Chatbot with Flask

This repository contains a custom chatbot implementation using LangChain, which extracts course data from [Brainlox](https://brainlox.com/courses/category/technical), generates embeddings stored in a vector store, and provides a Flask RESTful API to handle user conversations. The project demonstrates the integration of LangChain, HuggingFace, FAISS, and Flask for building conversational AI applications.

---

## Features

1. **Data Extraction**:
   - Extracts course data from [Brainlox](https://brainlox.com/courses/category/technical) using LangChain's `WebBaseLoader`.
   - Provides fallback course data in case the URL loader fails.

2. **Embeddings and Vector Store**:
   - Creates embeddings using `HuggingFaceEmbeddings` (`all-MiniLM-L6-v2` model).
   - Stores embeddings in a FAISS vector store for efficient retrieval.

3. **Flask RESTful API**:
   - Provides a `/chat` endpoint for user interaction.
   - Uses LangChain's `ConversationalRetrievalChain` to generate responses with relevant sources.

4. **Public API Access**:
   - Exposes the Flask app via Ngrok, allowing public access for testing and usage.

---

## Requirements

- Python 3.8+
- Required Python libraries (see `requirements.txt` for detailed versions):
  - `flask`
  - `pyngrok`
  - `langchain`
  - `langchain-community`
  - `sentence-transformers`
  - `faiss-cpu`
  - `transformers`
  - `beautifulsoup4`
  - `requests`

---

## Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/<your-username>/<repository-name>.git
   cd <repository-name>
   ```

2. **Install Dependencies**:
   Install all required libraries:
   ```bash
   pip install -r requirements.txt
   ```

3. **Set Ngrok Auth Token**:
   Obtain an Ngrok auth token from [Ngrok Dashboard](https://dashboard.ngrok.com/) and set it in your code:
   ```python
   ngrok.set_auth_token("<YOUR_NGROK_AUTH_TOKEN>")
   ```

---

## Usage

1. **Run the Flask App**:
   Start the Flask app and Ngrok tunnel:
   ```bash
   python app.py
   ```

2. **Access the Public API**:
   After starting the app, Ngrok will display a public URL (e.g., `https://<your-ngrok-id>.ngrok-free.app`).

3. **Test the API**:
   Use tools like `Postman` or Python's `requests` library to interact with the API:
   ```python
   import requests

   ngrok_url = "https://<your-ngrok-id>.ngrok-free.app/chat"
   response = requests.post(ngrok_url, json={"question": "What is Python?"})
   print(response.json())
   ```

---

## API Endpoints

### 1. `/` (GET)
- **Description**: Displays a welcome message.
- **Response**:
  ```json
  {
    "message": "Welcome to the Brainlox Chatbot API! Use /chat to interact."
  }
  ```

### 2. `/chat` (POST)
- **Description**: Handles user questions and provides responses.
- **Request Body**:
  ```json
  {
    "question": "Your question here"
  }
  ```
- **Response**:
  ```json
  {
    "answer": "Generated response to the question.",
    "sources": ["Source Title 1", "Source Title 2"]
  }
  ```

---

## Project Structure

```
.
├── app.py                 # Main Flask application
├── requirements.txt       # List of required Python libraries
├── README.md              # Project documentation
└── chatbot.ipynb          # Jupyter notebook for chatbot development
```

---

## Key Technologies

- **LangChain**: Used for data loading, embedding creation, and conversational chains.
- **HuggingFace**: Provides the embedding model (`all-MiniLM-L6-v2`) and text generation model (`google/flan-t5-base`).
- **FAISS**: Efficient vector store for fast retrieval of relevant documents.
- **Flask**: RESTful API framework.
- **Ngrok**: Exposes the local API to a public URL for easy access.

---

## Future Improvements

- **Dynamic Updates**: Add functionality to dynamically update the vector store with new data from the website.
- **Swagger Integration**: Document the API endpoints using Swagger or similar tools.
- **Enhanced Error Handling**: Improve error handling for invalid inputs and unexpected API issues.

---

## License

This project is licensed under the [MIT License](LICENSE).

