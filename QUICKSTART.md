# Quick Start Guide - GitHub Code Chat Assistant

Get up and running in 5 minutes! ⚡

## Prerequisites

Choose one:
- **Docker** (easiest) - Just Docker & Docker Compose
- **Local** - Python 3.11+, Node 18+, PostgreSQL/SQLite

## 5-Minute Setup with Docker

### Step 1: Get API Keys (2 min)

1. **GitHub Token**: https://github.com/settings/tokens
   - Click "Generate new token"
   - Select: `repo`, `user` scopes
   - Save it

2. **OpenAI API Key**: https://platform.openai.com/api-keys
   - Create new secret key
   - Save it

### Step 2: Clone & Configure (1 min)

```bash
# Clone
git clone https://github.com/yourusername/github-code-chat.git
cd github-code-chat

# Create .env
cp .env.example .env

# Edit .env (any text editor)
# GITHUB_TOKEN=your_token_here
# OPENAI_API_KEY=your_key_here
# SECRET_KEY=any_random_string
```

### Step 3: Start (2 min)

```bash
docker-compose up -d
```

That's it! 🎉

### Access

- **Frontend**: http://localhost:5173
- **API**: http://localhost:8000
- **API Docs**: http://localhost:8000/api/docs

### First Steps

1. Register account
2. Connect GitHub repo (e.g., `facebook/react`)
3. Wait for indexing
4. Start chatting!

## 10-Minute Setup Without Docker

### Backend (5 min)

```bash
# Setup
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# Configure
cp .env.example .env
# Edit .env with your keys

# Run
python -m uvicorn app.main:app --reload
```

### Frontend (5 min)

```bash
cd frontend
npm install
echo "VITE_API_URL=http://localhost:8000/api" > .env.local
npm run dev
```

Visit http://localhost:5173 ✨

## Testing the App

### 1. Create Account
```
Email: test@example.com
Password: TestPassword123
Username: testuser
```

### 2. Connect Repository
Try these public repos:
- `facebook/react` - React library
- `kubernetes/kubernetes` - Kubernetes
- `python/cpython` - Python
- `torvalds/linux` - Linux kernel

### 3. Chat Examples

Try these questions:
- "What is the main purpose of this repository?"
- "Explain the authentication flow"
- "Show me the API routes"
- "Find security vulnerabilities"
- "Generate documentation"

## Common Issues

### Port Already in Use
```bash
# Change port in docker-compose.yml or .env
PORT=8001  # Use different port
```

### API Key Invalid
```bash
# Double-check keys
echo $OPENAI_API_KEY
echo $GITHUB_TOKEN

# Regenerate if needed
```

### Database Error
```bash
# For SQLite (development):
DATABASE_URL=sqlite:///./github_chat.db

# Already configured, should work!
```

### "Can't connect to API"
```bash
# Verify backend running
curl http://localhost:8000/health

# Check API URL
VITE_API_URL=http://localhost:8000/api
```

## Next Steps

1. **Read** [README.md](README.md) for features
2. **Explore** [API Documentation](API.md)
3. **Deploy** with [Deployment Guide](DEPLOYMENT.md)
4. **Contribute** via [Contributing Guide](CONTRIBUTING.md)

## Helpful Commands

```bash
# View logs
docker-compose logs -f backend
docker-compose logs -f frontend

# Stop everything
docker-compose down

# Restart services
docker-compose restart

# Database reset
docker-compose exec backend python -c \
  "from app.core.database import Base, engine; \
   Base.metadata.drop_all(bind=engine); \
   Base.metadata.create_all(bind=engine)"

# Frontend rebuild
cd frontend && npm run build
```

## Keyboard Shortcuts

In chat:
- `Ctrl+Enter` / `Cmd+Enter` - Send message
- `Ctrl+K` / `Cmd+K` - Focus search
- `Esc` - Close modals

## Tips & Tricks

### Faster Indexing
```env
# Reduce for faster indexing
CHUNK_SIZE=500
CHUNK_OVERLAP=100
```

### Better AI Responses
```env
# Use GPT-4 for best results
LLM_MODEL=gpt-4-turbo-preview
```

### Local Development Only
```env
# Use SQLite instead of PostgreSQL
DATABASE_URL=sqlite:///./github_chat.db
```

## Getting Help

1. **Check FAQ** - See SETUP.md troubleshooting
2. **Review logs** - `docker-compose logs`
3. **Read docs** - Check README.md
4. **Create issue** - GitHub Issues
5. **Discuss** - GitHub Discussions

## What's Next?

- [ ] Connect your first repo
- [ ] Ask your first question
- [ ] Explore advanced features
- [ ] Customize for your needs
- [ ] Deploy to production
- [ ] Share feedback

## Support

- **Documentation**: See [README.md](README.md)
- **API Reference**: See [API.md](API.md)
- **Issues**: GitHub Issues
- **Email**: support@example.com

---

**Enjoy using GitHub Code Chat Assistant!** 🚀

Questions? Check [SETUP.md](SETUP.md) for detailed help.
