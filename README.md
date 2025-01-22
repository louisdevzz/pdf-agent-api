# PDF Agent API

This project consists of two main components:
1. An Ollama service for running the LLM model
2. A FastAPI service for handling PDF processing and questions

## Prerequisites

- Docker and Docker Compose
- GPU support (for Ollama)
- CUDA drivers (for GPU support)

## Running the Services

### Start server

```bash
git clone https://github.com/louisdevzz/pdf-agent-api.git
cd pdf-agent-api
```

### Install dependencies

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### Using Docker Compose (Recommended)

The easiest way to run all services is using Docker Compose:

```bash
docker compose up --build
```

This will start both the Ollama service and the API service. The services will be available at:
- Ollama: http://localhost:11434
- API: http://localhost:8000

### Running Services Separately

#### 1. Running Ollama Service

Navigate to the ollama directory and build/run the Docker container:

```bash
cd ollama
docker build -t ollama-service .
docker run --gpus all -p 11434:11434 ollama-service
```

#### 2. Running API Service

Navigate to the api directory and run the service:

```bash
cd api
# Install dependencies
pip install -r requirements.txt
# Run the uvicorn server
uvicorn app:app --host 0.0.0.0 --port 8000 --reload
```

## API Endpoints

The API service provides the following endpoints:

- `POST /upload`: Upload PDF files for processing
- `POST /ask`: Ask questions about the uploaded documents

## Testing with Postman

### 1. Upload PDF Files
- **Endpoint**: `POST http://localhost:8000/upload`
- **Request Type**: Form-data
- **Headers**: None required
- **Body**: 
  - Key: `files` (Type: File)
  - Select one or multiple PDF files
- **Expected Response**:
```json
{
    "message": "Files uploaded and processed successfully",
    "file_paths": ["./uploads/your_file.pdf"]
}
```

### 2. Ask Questions
- **Endpoint**: `POST http://localhost:8000/ask`
- **Request Type**: Raw JSON
- **Headers**: 
  - Content-Type: application/json
- **Body**:
```json
{
    "question": "Your question about the PDF content"
}
```
- **Expected Response**:
```json
{
    "answer": "The answer to your question based on the PDF content"
}
```

### Testing Steps
1. Start the API service using Docker Compose
2. Open Postman
3. First, use the upload endpoint to send your PDF files
4. Wait for the upload confirmation
5. Then, use the ask endpoint to ask questions about the uploaded documents
6. You should receive relevant answers based on the PDF content

**Note**: Make sure all services are running before testing. If you get connection errors, verify that both the Ollama service and API service are up and running.
