# 🤖 GenAI-Assistant

An AI-powered assistant platform that leverages OpenAI's GPT-3.5-turbo to provide three specialized services: DevOps interview preparation, code explanation, and DevOps troubleshooting. Built with a modern stack combining Next.js frontend and FastAPI backend.

## 📊 Tech Stack

| Language | Percentage |
|----------|-----------|
| JavaScript | 82.8% |
| Python | 12.8% |
| Dockerfile | 2.6% |
| CSS | 1.1% |
| TypeScript | 0.7% |

**Frontend:** Next.js, React, TypeScript, Tailwind CSS  
**Backend:** FastAPI, Python, OpenAI API  
**DevOps:** Docker, Docker Compose

---

## ✨ Main Features

### 🎯 1. **Interview Preparation Bot**
- AI-powered DevOps technical interview questions and answers
- Detailed explanations with real-world examples
- Expert-level knowledge base for interview preparation

### 💻 2. **Code Explainer**
- Analyze and explain code snippets in detail
- DevOps-focused explanations with practical scenarios
- Break down complex logic into understandable concepts

### 🔧 3. **DevOps Assistant**
- Troubleshoot errors and deployment issues
- Get expert guidance on resolving DevOps problems
- Detailed analysis of error logs and debugging

---

## 🏗️ Architecture & Component Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                         Frontend (Next.js)                       │
│                     (Port 3000, React + TS)                     │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │ • Interview Bot UI                                       │   │
│  │ • Code Explainer Interface                               │   │
│  │ • DevOps Assistant Chat                                  │   │
│  │ • Typewriter Animation Effects                           │   │
│  └──────────────────────────────────────────────────────────┘   │
└────────────────────────────────┬────────────────────────────────┘
                                 │
                    HTTP/REST API Requests
                   (CORS Enabled for all origins)
                                 │
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Backend (FastAPI)                           │
│                    (Port 8000, Python 3.11)                     │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │ POST /interview         → handle_interview()            │   │
│  │ POST /explain-code      → explain_code()                │   │
│  │ POST /devops-assistant  → review_devops()               │   │
│  └──────────────────────────────────────────────────────────┘   │
│                              │                                    │
│                     Utility Functions                            │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │ • interview.py     - Interview preparation logic        │   │
│  │ • code_explainer.py - Code analysis logic               │   │
│  │ • devops_assistant.py - DevOps troubleshooting logic    │   │
│  └──────────────────────────────────────────────────────────┘   │
└────────────────────────────────┬────────────────────────────────┘
                                 │
                    OpenAI API Calls (GPT-3.5-turbo)
                    (Requires OPENAI_API_KEY env var)
                                 │
                                 ▼
                  ┌──────────────────────────────┐
                  │   OpenAI GPT-3.5-turbo       │
                  │   AI Model Service           │
                  └──────────────────────────────┘
```

### 📡 Data Flow

1. **User Input** → Frontend captures user query/code/error
2. **API Request** → Frontend sends POST request to backend endpoint
3. **Processing** → Backend utility processes the request
4. **AI Call** → OpenAI API is called with customized prompt
5. **Response** → AI response is returned and displayed on frontend
6. **Output** → User sees formatted AI-generated response

---

## 🚀 How It Works

### Prerequisites

- **Node.js** (v18 or higher) - for frontend
- **Python** (3.11 or higher) - for backend
- **Docker & Docker Compose** (optional but recommended)
- **OpenAI API Key** - Get from [platform.openai.com](https://platform.openai.com)

### ⚡ Quick Start with Docker

The easiest way to run the entire application:

```bash
# 1. Clone the repository
git clone https://github.com/vishal030308-star/GenAI-Assistant.git
cd GenAI-Assistant

# 2. Create environment file
echo "OPENAI_API_KEY=your_api_key_here" > backend/.env

# 3. Start all services
docker-compose up --build
```

Visit **http://localhost:3000** for the frontend and **http://localhost:8000** for the API.

---

### 🛠️ Local Development Setup

#### Backend Setup (FastAPI)

```bash
cd backend

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Create .env file with your OpenAI API key
echo "OPENAI_API_KEY=sk-your-key-here" > .env

# Run the server
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

Backend will be available at: **http://localhost:8000**  
API Documentation: **http://localhost:8000/docs**

#### Frontend Setup (Next.js)

```bash
cd frontend

# Install dependencies
npm install

# Create environment file (optional for local development)
# The frontend can connect to backend at http://localhost:8000

# Run development server
npm run dev

# Or build for production
npm run build
npm start
```

Frontend will be available at: **http://localhost:3000**

---

## 📡 API Endpoints

### 1. Interview Preparation Bot

**Endpoint:** `POST /interview`

```bash
curl -X POST http://localhost:8000/interview \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "question=What is Kubernetes and how does it work?"
```

**Request:**
```json
{
  "question": "What is Kubernetes and how does it work?"
}
```

**Response:**
```json
{
  "response": "Kubernetes is an open-source container orchestration platform... [detailed AI-generated response]"
}
```

---

### 2. Code Explainer

**Endpoint:** `POST /explain-code`

```bash
curl -X POST http://localhost:8000/explain-code \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "code=for i in range(10): print(i)"
```

**Request:**
```json
{
  "code": "def deploy_container(image_name):\n    client = docker.from_env()\n    container = client.containers.run(image_name, detach=True)\n    return container.id"
}
```

**Response:**
```json
{
  "response": "This function creates a Docker client and deploys a container from the specified image... [detailed explanation with examples]"
}
```

---

### 3. DevOps Assistant (Error Troubleshooting)

**Endpoint:** `POST /devops-assistant`

```bash
curl -X POST http://localhost:8000/devops-assistant \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "content=Error: CrashLoopBackOff in Kubernetes pod"
```

**Request:**
```json
{
  "content": "Error: Connection refused on port 5432. PostgreSQL container won't start."
}
```

**Response:**
```json
{
  "response": "This error typically indicates that PostgreSQL isn't running or listening on the specified port... [detailed troubleshooting guide]"
}
```

---

## 📁 Project Structure

```
GenAI-Assistant/
├── frontend/                    # Next.js React Application
│   ├── app/                     # Next.js app directory
│   ├── components/              # Reusable React components
│   ├── pages/                   # Page components
│   ├── styles/                  # CSS files and Tailwind config
│   ├── public/                  # Static assets
│   ├── package.json             # Frontend dependencies
│   ├── tsconfig.json            # TypeScript config
│   ├── tailwind.config.js       # Tailwind CSS configuration
│   ├── postcss.config.js        # PostCSS configuration
│   ├── next.config.ts           # Next.js configuration
│   └── Dockerfile               # Frontend Docker image
│
├── backend/                     # FastAPI Python Application
│   ├── main.py                  # FastAPI application entry point
│   ├── utils/                   # Utility modules
│   │   ├── interview.py         # Interview bot logic
│   │   ├── code_explainer.py    # Code explanation logic
│   │   └── devops_assistant.py  # DevOps troubleshooting logic
│   ├── requirements.txt         # Python dependencies
│   ├── Dockerfile               # Backend Docker image
│   └── .env                     # Environment variables (git ignored)
│
├── docker-compose.yml           # Docker Compose configuration
├── .gitignore                   # Git ignore rules
└── README.md                    # This file
```

---

## 🔄 How Each Feature Works

### 1️⃣ Interview Bot Flow

```
User Question
    ↓
[Frontend Form] → Capture question input
    ↓
[API POST /interview] → Send to backend
    ↓
[Prompt Template] → "You are a DevOps expert interview bot..."
    ↓
[OpenAI API] → Send prompt + question
    ↓
[GPT-3.5-turbo] → Generate detailed answer with examples
    ↓
[Response] → Return AI answer to frontend
    ↓
[Display] → Show formatted response with typewriter effect
```

### 2️⃣ Code Explainer Flow

```
Code Input
    ↓
[Frontend Textarea] → Paste or write code
    ↓
[API POST /explain-code] → Send to backend
    ↓
[Prompt Template] → "You are a DevOps Expert, explain this code..."
    ↓
[OpenAI API] → Send prompt + code snippet
    ↓
[GPT-3.5-turbo] → Generate detailed explanation + scenarios
    ↓
[Response] → Return explanation to frontend
    ↓
[Display] → Show formatted explanation
```

### 3️⃣ DevOps Assistant Flow

```
Error/Issue Input
    ↓
[Frontend Textarea] → Paste error message
    ↓
[API POST /devops-assistant] → Send to backend
    ↓
[Prompt Template] → "You are a DevOps expert, help troubleshoot..."
    ↓
[OpenAI API] → Send prompt + error content
    ↓
[GPT-3.5-turbo] → Generate troubleshooting guide + solutions
    ↓
[Response] → Return troubleshooting steps to frontend
    ↓
[Display] → Show detailed solution
```

---

## 📦 Key Dependencies

### Backend
- **FastAPI** - Modern Python web framework
- **Uvicorn** - ASGI web server
- **OpenAI** - Official OpenAI Python client (v1.0+)
- **python-dotenv** - Load environment variables
- **python-multipart** - Handle form data

### Frontend
- **Next.js 15** - React framework with SSR
- **React 18** - UI library
- **TypeScript** - Type-safe JavaScript
- **Tailwind CSS** - Utility-first CSS framework
- **react-simple-typewriter** - Typewriter animation effect

---

## ⚙️ Environment Configuration

### Backend (.env file)

```bash
# Required
OPENAI_API_KEY=sk-your-openai-api-key-here

# Optional (adjust if needed)
# API_HOST=0.0.0.0
# API_PORT=8000
```

### Frontend (.env.local file) - Optional

```bash
# For local development, defaults to http://localhost:8000
NEXT_PUBLIC_API_BASE_URL=http://localhost:8000

# For production
# NEXT_PUBLIC_API_BASE_URL=https://api.yourdomain.com
```

---

## 🐳 Docker Setup

### Using Docker Compose (Recommended)

```bash
# Build and start all services
docker-compose up --build

# Stop services
docker-compose down

# View logs
docker-compose logs -f
```

The `docker-compose.yml` file:
- **Backend service:** Runs on port 8000
- **Frontend service:** Runs on port 3000
- **Network:** Both services can communicate via service names
- **API_BASE_URL:** Frontend automatically connects to backend via `http://backend:8000`

### Building Individual Docker Images

```bash
# Backend
cd backend
docker build -t genai-backend .
docker run -p 8000:8000 --env-file .env genai-backend

# Frontend
cd frontend
docker build -t genai-frontend .
docker run -p 3000:3000 genai-frontend
```

---

## 💻 Usage Examples

### Web Interface

1. Open http://localhost:3000 in your browser
2. Choose between three modes:
   - **Interview Bot:** Enter interview questions
   - **Code Explainer:** Paste code for detailed explanation
   - **DevOps Assistant:** Describe errors for troubleshooting
3. Click submit and watch the AI-generated response appear with typewriter effect

### Using cURL (Backend API)

```bash
# Interview Bot
curl -X POST http://localhost:8000/interview \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "question=Explain Docker networking"

# Code Explainer
curl -X POST http://localhost:8000/explain-code \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "code=docker run -d -p 8080:80 nginx"

# DevOps Assistant
curl -X POST http://localhost:8000/devops-assistant \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "content=Pod keeps restarting with OOMKilled error"
```

### Integration in Code

```python
# Python example
import requests

BASE_URL = "http://localhost:8000"

# Call Interview Bot
response = requests.post(
    f"{BASE_URL}/interview",
    data={"question": "What is CI/CD?"}
)
print(response.json()["response"])

# Call Code Explainer
response = requests.post(
    f"{BASE_URL}/explain-code",
    data={"code": "git clone https://github.com/user/repo.git"}
)
print(response.json()["response"])
```

---

## ⚠️ Important Notes

### Production Deployment

- **CORS Policy:** Currently allows all origins (`["*"]`). In production, change to specific domain:
  ```python
  origins = ["https://yourdomain.com"]
  ```

- **API Key Security:** Never commit `.env` file. Use environment variables in production:
  ```bash
  export OPENAI_API_KEY="your-key-here"
  ```

- **Rate Limiting:** Consider implementing rate limiting for production use

- **Error Handling:** Add comprehensive error handling and logging

- **HTTPS:** Use HTTPS/TLS in production

### Cost Considerations

- Each API call to OpenAI incurs a cost (based on GPT-3.5-turbo pricing)
- Monitor usage and set up billing alerts in OpenAI dashboard
- Consider implementing request caching to reduce costs

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

---

## 📝 License

This project is open source and available for educational and commercial use.

---

## 🔗 Repository

**GitHub:** [github.com/vishal030308-star/GenAI-Assistant](https://github.com/vishal030308-star/GenAI-Assistant)

---

## 🎓 Learning Resources

- [OpenAI API Documentation](https://platform.openai.com/docs)
- [FastAPI Documentation](https://fastapi.tiangolo.com)
- [Next.js Documentation](https://nextjs.org/docs)
- [Docker Documentation](https://docs.docker.com)

---

**Built with ❤️ using OpenAI's GPT-3.5-turbo**
