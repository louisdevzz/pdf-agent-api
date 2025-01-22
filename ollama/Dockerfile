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

# Start Ollama service and pull the model with CPU only
ENV OLLAMA_HOST=0.0.0.0
CMD ["sh", "-c", "ollama serve & sleep 10 && ollama pull llama2:latest && tail -f /dev/null"] 