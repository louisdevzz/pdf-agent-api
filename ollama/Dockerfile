FROM ubuntu:22.04

# Install required dependencies
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    && rm -rf /var/lib/apt/lists/*

# Install Ollama
RUN curl -fsSL https://ollama.com/install.sh | sh

# Expose the Ollama port
EXPOSE 11434

# Start Ollama service and pull the model
ENV OLLAMA_HOST=0.0.0.0
# Check if NVIDIA GPU is available, if not use CPU only
CMD ["sh", "-c", "\
    if command -v nvidia-smi >/dev/null 2>&1; then \
        echo 'NVIDIA GPU detected, using GPU mode'; \
    else \
        echo 'No NVIDIA GPU detected, using CPU mode'; \
        export OLLAMA_CUDA=0; \
    fi && \
    ollama serve & sleep 10 && \
    ollama pull llama2:latest && \
    tail -f /dev/null \
"] 