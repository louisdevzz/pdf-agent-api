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

## Notes

- The API service depends on the Ollama service being available
- Make sure your system has sufficient GPU resources for running the LLM model
- The API service uses FastAPI and supports automatic API documentation at `/docs` 