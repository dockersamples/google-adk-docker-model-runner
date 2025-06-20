
# Google ADK + Docker Model Runner Agents 

AI agents built using Google ADK and Docker Model Runner. 


## Available Agents

| Agent | Description | Key Features |
|-------|-------------|-------------|
| **Sequential Agent** | Code development pipeline | Write → Review → Refactor |
| **Parallel Agent** | Market intelligence analysis | Concurrent competitive/trend/sentiment analysis |
| **Loop Agent** | Iterative recipe development | Recipe creation with dietician feedback loops |
| **Human-in-Loop** | Travel planning with feedback | Human decision points in AI workflows |
| **Google Search** | Web research and synthesis | Live search with comprehensive reports |
| **Find Job** | Job market analysis | Career guidance and opportunity analysis |

## 🏗️ Architecture

### System Overview

```
┌─────────────────────────────────────┐
│        Application Layer            │ ← Your Agent Logic
├─────────────────────────────────────┤
│      🤖 Google ADK Framework       │ ← Agent Orchestration
│   • Multi-agent workflows          │
│   • State management               │
│   • Tool integration               │
├─────────────────────────────────────┤
│    📡 Centralized Configuration    │ ← Environment Detection
│   • Auto endpoint detection        │
│   • Container networking           │
│   • Model configuration            │
├─────────────────────────────────────┤
│      🔌 LiteLLM Abstraction        │ ← Model API Layer
├─────────────────────────────────────┤
│    🚢 Docker Model Runner          │ ← Local Inference
│   • llama.cpp engine               │
│   • OpenAI-compatible API          │
├─────────────────────────────────────┤
│      🧠 AI Model (Llama 3.2)       │ ← The Actual Model
└─────────────────────────────────────┘
```

## Quick Start

### Prerequisites

- **Docker Desktop 4.40+** with Model Runner enabled
- **Python 3.9+** (for local development)
- **Google API Key** (optional, for Google Search agents)

### 1. Pull and Run a Model

```bash
# Enable Docker Model Runner
docker desktop enable model-runner --tcp 12434

# Pull a model
docker model pull ai/llama3.2:1B-Q8_0

# Verify Model Runner is working
curl http://localhost:12434/engines/llama.cpp/v1/models
```

### 2. Clone and Setup

```bash
git clone https://github.com/dockersamples/google-adk-docker-model-runner.git
cd google-adk-docker-model-runner

# Copy environment template
cp agents/.env.example agents/.env

# Edit .env file with your configuration
nano agents/.env
```

### Sample .env file

```
DOCKER_MODEL_RUNNER=http://localhost:12434/engines/llama.cpp/v1
MODEL_NAME=ai/llama3.2:1B-Q8_0
OPENAI_API_KEY=anything
GOOGLE_API_KEY=XXX
GOOGLE_GENAI_USE_VERTEXAI=FALSE
GOOGLE_CLOUD_LOCATION=us-central1
GOOGLE_CLOUD_PROJECT=XXX
LOG_LEVEL=DEBUG
DEV_MODE=true
LITELLM_DROP_PARAMS=true
LITELLM_TIMEOUT=180
LITELLM_REQUEST_TIMEOUT=120
LITELLM_MAX_RETRIES=5
LITELLM_LOG=DEBUG
OPENAI_API_TYPE=openai
OPENAI_API_BASE=http://localhost:12434/engines/llama.cpp/v1
OPENAI_MODEL_NAME=ai/llama3.2:1B-Q8_0
LITELLM_CONNECTION_TIMEOUT=60
LITELLM_READ_TIMEOUT=180
LITELLM_FALLBACK_MODEL=ai/llama3.2:1B-Q8_0
HTTPX_TIMEOUT=180
```


### 3. Run Locally

```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run specific agents
cd agents && adk web
```
Now open - http://localhost:8000

### 4. Run with Docker

```bash
# Build the image
docker build -t docker-adk-agents:v1 .

# Run with local .env variables
docker run -p 8000:8000 --env-file agents/.env docker-adk-agents:v1
```
Now open - http://localhost:8000

## Sample prompts

| Agent | Prompts |
|-------|-------------|
| **Sequential Agent** | Write a HTML code with title and description for front main website page |
| **Parallel Agent** | Customer sentiment and feedback trends on Docker Model Runner and Docker AI |
| **Loop Agent** | Suggest some healthy recipe with paneer |
| **Human-in-Loop** | Plan a trip to dubai |
| **Google Search** | Share details about docker model runner features release |
| **Find Job** | Share job related to python |












