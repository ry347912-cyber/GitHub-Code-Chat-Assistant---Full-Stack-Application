# GitHub Code Chat Assistant 🚀

An AI-powered full-stack application that allows users to connect their GitHub repositories and chat with their codebase using natural language. Ask questions, get explanations, understand architecture, and generate documentation.

## ✨ Features

### Core Features
- 🔗 **GitHub Integration**: Connect public repositories directly
- 🤖 **AI Code Understanding**: Uses OpenAI and LangChain for intelligent code analysis
- 💬 **Smart Chat Interface**: Ask questions about your codebase
- 🔍 **Semantic Search**: Find relevant code using embeddings
- 📚 **Vector Database**: FAISS/ChromaDB support for fast retrieval
- 🔐 **Authentication**: JWT-based secure user system
- 📱 **Responsive UI**: Modern dark theme similar to GitHub Copilot

### Advanced Features
- ✅ **Multi-file Reasoning**: Understand interactions across files
- 📖 **Auto Documentation**: Generate README and API docs
- 🛡️ **Security Analysis**: Identify vulnerabilities
- 🏗️ **Architecture Explanation**: Understand system design
- 📊 **Code Statistics**: Repository analysis and insights
- 💾 **Conversation History**: Persistent chat sessions
- ⚡ **Streaming Responses**: Real-time AI response streaming

### Supported Languages
- Python
- JavaScript/TypeScript
- Java
- C/C++
- Go
- Rust
- And more...

## 📋 Requirements

### Backend
- Python 3.11+
- FastAPI
- PostgreSQL (or SQLite for development)
- Redis
- OpenAI API Key

### Frontend
- Node.js 18+
- React 18+
- Vite
- TailwindCSS

### Services
- GitHub API Token (for fetching repositories)
- OpenAI API Key (for AI features)

## 🚀 Quick Start

### Option 1: Docker Compose (Recommended)

```bash
# Clone repository
git clone https://github.com/yourusername/github-code-chat.git
cd github-code-chat

# Create environment file
cp .env.example .env

# Edit .env with your API keys
GITHUB_TOKEN=your_github_token
OPENAI_API_KEY=your_openai_key
SECRET_KEY=your_secret_key

# Build and run with Docker
docker-compose up -d

# Access the application
# Frontend: http://localhost:5173
# Backend API: http://localhost:8000
# API Docs: http://localhost:8000/api/docs
```

### Option 2: Manual Setup

#### Backend Setup

```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Create .env file
cp .env.example .env

# Edit .env with your configuration
nano .env

# Run migrations (if using PostgreSQL)
alembic upgrade head

# Start backend server
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

#### Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# Create .env.local
echo "VITE_API_URL=http://localhost:8000/api" > .env.local

# Start development server
npm run dev

# Access at http://localhost:5173
```

### Option 3: Using index.html Directly

1. **Build the frontend for production**:
   ```bash
   cd frontend
   npm install
   npm run build
   ```

2. **Open the built application**:
   ```bash
   # The compiled files are in frontend/dist/
   # Open frontend/dist/index.html in your browser
   # Make sure the backend is running on port 8000
   ```

3. **Or serve with a simple HTTP server**:
   ```bash
   cd frontend/dist
   python -m http.server 5173
   # Access at http://localhost:5173
   ```

## 📁 Project Structure

```
github-code-chat/
├── app/                           # Backend application
│   ├── main.py                   # FastAPI application factory
│   ├── core/
│   │   ├── config.py             # Settings and configuration
│   │   ├── database.py           # Database models and setup
│   │   └── security.py           # Authentication and JWT
│   ├── api/
│   │   └── routes/
│   │       ├── auth.py           # Authentication endpoints
│   │       ├── repositories.py    # Repository management
│   │       ├── chat.py           # Chat and conversation
│   │       └── analysis.py       # Code analysis features
│   ├── services/
│   │   ├── github_service.py      # GitHub API integration
│   │   ├── vector_db_service.py   # Vector database operations
│   │   ├── llm_service.py         # LLM/AI integration
│   │   └── code_processing_service.py  # Code parsing and chunking
│   └── utils/
│       └── logger.py              # Logging configuration
│
├── frontend/                      # React frontend application
│   ├── index.html                # Main HTML entry point
│   ├── src/
│   │   ├── main.jsx              # React entry point
│   │   ├── App.jsx               # Main application component
│   │   ├── pages/
│   │   │   ├── LoginPage.jsx
│   │   │   ├── DashboardPage.jsx
│   │   │   ├── RepositoriesPage.jsx
│   │   │   └── ChatPage.jsx
│   │   ├── components/
│   │   │   ├── Layout.jsx
│   │   │   ├── ProtectedRoute.jsx
│   │   │   └── ... other components
│   │   ├── store/
│   │   │   ├── authStore.js
│   │   │   ├── repositoryStore.js
│   │   │   └── chatStore.js
│   │   ├── index.css             # Tailwind CSS styles
│   │   └── services/
│   │       └── api.js            # API client
│   ├── package.json
│   ├── vite.config.js
│   └── Dockerfile
│
├── requirements.txt              # Python dependencies
├── docker-compose.yml           # Docker composition
├── Dockerfile.backend           # Backend Docker image
├── .env.example                 # Environment variables template
└── README.md                    # This file
```

## 🔑 Environment Variables

### Backend (.env)

```env
# GitHub
GITHUB_TOKEN=your_github_token_here
GITHUB_API_URL=https://api.github.com

# Database
DATABASE_URL=postgresql://user:password@localhost:5432/github_chat
# Or SQLite: sqlite:///./github_chat.db
REDIS_URL=redis://localhost:6379/0

# Security
SECRET_KEY=your-super-secret-key-change-in-production
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30

# AI/LLM
OPENAI_API_KEY=your_openai_key_here
LLM_MODEL=gpt-4-turbo-preview
LLM_TEMPERATURE=0.7

# Vector Database
VECTOR_DB_TYPE=faiss  # or chromadb
FAISS_INDEX_PATH=./data/faiss_index

# Server
HOST=0.0.0.0
PORT=8000
DEBUG=False
CORS_ORIGINS=http://localhost:3000,http://localhost:5173

# File Processing
CHUNK_SIZE=1000
CHUNK_OVERLAP=200
MAX_FILE_SIZE_MB=50

# Logging
LOG_LEVEL=INFO
LOG_FILE=./logs/app.log
```

### Frontend (.env.local)

```env
VITE_API_URL=http://localhost:8000/api
```

## 🔄 Workflow

### 1. User Registration & Login
```
User → Register/Login → JWT Token → Authenticated Session
```

### 2. Repository Connection
```
User → Enter GitHub URL → Validate & Fetch Metadata → Store Repository
```

### 3. Repository Indexing
```
Repository → Fetch Files → Parse & Chunk Code → Generate Embeddings → Vector DB
```

### 4. Chat & Query
```
User Question → Vector Search → Retrieve Context → LLM Processing → Response
```

## 📚 API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `POST /api/auth/refresh` - Refresh access token
- `GET /api/auth/me` - Get current user
- `POST /api/auth/logout` - Logout user

### Repositories
- `GET /api/repositories` - List user repositories
- `POST /api/repositories/connect` - Connect new repository
- `GET /api/repositories/{id}` - Get repository details
- `GET /api/repositories/{id}/files` - Get repository files
- `POST /api/repositories/{id}/index` - Start indexing
- `DELETE /api/repositories/{id}` - Delete repository

### Chat
- `POST /api/chat/sessions` - Create chat session
- `GET /api/chat/sessions` - List chat sessions
- `GET /api/chat/sessions/{id}` - Get session details
- `POST /api/chat/message` - Send message
- `POST /api/chat/message/stream` - Stream message response
- `DELETE /api/chat/sessions/{id}` - Delete session

### Code Analysis
- `POST /api/analysis/analyze` - Analyze code
- `POST /api/analysis/explain-function` - Explain function
- `POST /api/analysis/extract-functions` - Extract functions
- `POST /api/analysis/security-analysis` - Security analysis
- `POST /api/analysis/generate-documentation` - Generate docs
- `POST /api/analysis/generate-readme` - Generate README

## 🛠️ Technology Stack

### Backend
| Technology | Purpose |
|-----------|---------|
| **FastAPI** | Web framework |
| **SQLAlchemy** | ORM |
| **Pydantic** | Data validation |
| **LangChain** | LLM orchestration |
| **Sentence Transformers** | Embeddings |
| **FAISS/ChromaDB** | Vector storage |
| **PyGithub** | GitHub API |
| **Python-jose** | JWT tokens |
| **Passlib** | Password hashing |

### Frontend
| Technology | Purpose |
|-----------|---------|
| **React 18** | UI framework |
| **Vite** | Build tool |
| **Zustand** | State management |
| **Axios** | HTTP client |
| **TailwindCSS** | Styling |
| **React Markdown** | Markdown rendering |
| **Framer Motion** | Animations |
| **Lucide Icons** | Icons |

### Infrastructure
| Technology | Purpose |
|-----------|---------|
| **PostgreSQL** | Primary database |
| **Redis** | Caching |
| **Docker** | Containerization |
| **Docker Compose** | Orchestration |

## 🔐 Security

### Implemented Security Measures

1. **Authentication**
   - JWT token-based authentication
   - Refresh token rotation
   - Secure password hashing (bcrypt)

2. **Authorization**
   - User-specific data isolation
   - Repository ownership verification
   - Session-based access control

3. **API Security**
   - CORS configuration
   - Rate limiting
   - Input validation with Pydantic
   - SQL injection prevention (SQLAlchemy ORM)

4. **Data Protection**
   - HTTPS ready
   - Secure token storage
   - Environment variable configuration

### Security Best Practices

```python
# Always use environment variables for secrets
SECRET_KEY = os.getenv('SECRET_KEY')

# Validate and sanitize inputs
class RepositoryConnect(BaseModel):
    url: str  # Validated by Pydantic

# Use HTTPS in production
CORS_ORIGINS = ["https://yourdomain.com"]

# Implement rate limiting
@limiter.limit("100/minute")
```

## 📊 Database Schema

### Users Table
```sql
id, username, email, hashed_password, full_name, is_active, is_admin, created_at, updated_at
```

### Repositories Table
```sql
id, owner_id, github_url, repo_name, repo_owner, description, language, stars,
is_indexed, indexed_at, index_status, file_count, total_tokens, vector_store_path,
created_at, updated_at
```

### RepositoryFiles Table
```sql
id, repository_id, file_path, file_name, language, content, size_bytes,
chunk_count, token_count, created_at, updated_at
```

### FileChunks Table
```sql
id, file_id, chunk_index, content, start_line, end_line, token_count,
embedding_id, created_at
```

### ChatSessions Table
```sql
id, user_id, repository_id, title, is_active, created_at, updated_at
```

### ChatMessages Table
```sql
id, session_id, role, content, referenced_files, context_chunks,
tokens_used, response_time_ms, created_at
```

## 🚀 Deployment

### Production Deployment

#### Using Docker Compose

```bash
# Set production environment variables
export ENVIRONMENT=production
export SECRET_KEY=$(openssl rand -hex 32)
export DEBUG=False

# Build and deploy
docker-compose -f docker-compose.yml up -d

# Check health
curl http://localhost:8000/health
```

#### Using Kubernetes

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: github-code-chat-backend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: github-code-chat
  template:
    metadata:
      labels:
        app: github-code-chat
    spec:
      containers:
      - name: backend
        image: github-code-chat:latest
        ports:
        - containerPort: 8000
        env:
        - name: ENVIRONMENT
          value: "production"
        - name: DATABASE_URL
          valueFrom:
            secretKeyRef:
              name: app-secrets
              key: database-url
```

#### Cloud Deployment (Heroku Example)

```bash
# Create Heroku app
heroku create your-app-name

# Set environment variables
heroku config:set OPENAI_API_KEY=your_key
heroku config:set GITHUB_TOKEN=your_token
heroku config:set SECRET_KEY=your_key

# Deploy
git push heroku main

# Check logs
heroku logs --tail
```

## 🐛 Troubleshooting

### Backend Issues

**Issue**: "ModuleNotFoundError: No module named 'app'"
```bash
# Solution: Make sure you're running from the project root
python -m uvicorn app.main:app --reload
```

**Issue**: Database connection error
```bash
# Check PostgreSQL is running
psql -U github_chat -d github_chat -c "SELECT 1"

# Or use SQLite instead
DATABASE_URL=sqlite:///./github_chat.db
```

**Issue**: CORS errors in browser
```python
# Update CORS_ORIGINS in .env
CORS_ORIGINS=http://localhost:5173,http://localhost:3000
```

### Frontend Issues

**Issue**: API calls failing
```bash
# Check backend is running on port 8000
curl http://localhost:8000/health

# Check API URL in .env.local
VITE_API_URL=http://localhost:8000/api
```

**Issue**: Module not found
```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

## 📈 Performance Optimization

### Backend Optimization
```python
# Enable query caching
ENABLE_CACHE=True
CACHE_TTL_HOURS=24

# Use FAISS for faster similarity search
VECTOR_DB_TYPE=faiss

# Optimize chunk size
CHUNK_SIZE=1000  # Adjust based on your data
```

### Frontend Optimization
```javascript
// Code splitting
const ChatPage = lazy(() => import('./pages/ChatPage'));

// Memoization for expensive components
const MemoizedCodeBlock = memo(CodeBlock);

// Virtual scrolling for long message lists
<VirtualList items={messages} />
```

## 🤝 Contributing

### Setup Development Environment

```bash
# Clone repository
git clone https://github.com/yourusername/github-code-chat.git
cd github-code-chat

# Create feature branch
git checkout -b feature/awesome-feature

# Make changes and test
# ... your changes ...

# Run tests
pytest tests/

# Commit and push
git commit -am 'Add awesome feature'
git push origin feature/awesome-feature

# Create Pull Request
```

### Code Standards
- Follow PEP 8 for Python
- Use ES6+ for JavaScript
- Add docstrings to functions
- Write tests for new features
- Update documentation

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🆘 Support

### Getting Help

1. **Documentation**: Check the docs in this README
2. **Issues**: Create an issue on GitHub
3. **Discussions**: Start a discussion for questions
4. **Email**: support@yourdomain.com

### Common Questions

**Q: Can I use this with private repositories?**
A: Yes, if you provide a GitHub token with appropriate permissions.

**Q: What LLM models are supported?**
A: Currently OpenAI (GPT-4, GPT-3.5), with support for Gemini coming soon.

**Q: How much does it cost?**
A: Costs depend on API usage. See OpenAI pricing for details.

**Q: Can I self-host?**
A: Yes, use Docker Compose for complete self-hosted deployment.

## 🎉 Acknowledgments

- Built with FastAPI, React, and LangChain
- Inspired by GitHub Copilot and Cursor AI
- Vector database support by FAISS and Chromadb
- Embeddings by Sentence Transformers

## 📞 Contact

- **GitHub Issues**: [Create an issue](https://github.com/yourusername/github-code-chat/issues)
- **Email**: your.email@example.com
- **Website**: your-website.com

---

**Made with ❤️ by the GitHub Code Chat Team**

**Last Updated**: December 2024
**Version**: 1.0.0
