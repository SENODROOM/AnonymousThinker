# 🧠 AnonymousThinker — Full Stack AI Chat App

A ChatGPT-like AI chat application built with MERN stack using **free AI APIs**.

![Stack](https://img.shields.io/badge/MongoDB-4EA94B?style=flat&logo=mongodb&logoColor=white)
![Stack](https://img.shields.io/badge/Express-black?style=flat&logo=express&logoColor=white)
![Stack](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black)
![Stack](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)

## ✨ Features

- 💬 **Full Chat Interface** — New chat, chat history, sidebar like ChatGPT
- 🤖 **Free AI APIs** — Hugging Face (free) + Groq (free, ultra-fast)
- 🧬 **AI Training** — Custom personas, system prompts, training examples
- 📤 **Export Training Data** — JSONL format for Hugging Face fine-tuning
- 🔐 **Auth System** — Register, login, JWT tokens
- 📱 **Responsive** — Works on mobile and desktop

---

## 🚀 Quick Setup

### Prerequisites
- Node.js 18+
- MongoDB (local or [MongoDB Atlas](https://cloud.mongodb.com) - free)
- A free API key (see Step 3)

### Step 1: Clone & Install

```bash
# Install all dependencies
npm run install-all

# Or manually:
cd backend && npm install
cd ../frontend && npm install
```

### Step 2: Configure Environment

Edit `backend/.env`:

```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/anonymousthinker
JWT_SECRET=change_this_to_a_random_secret_string

# Choose ONE (or both) of these free AI APIs:
HUGGINGFACE_API_KEY=hf_your_token_here
GROQ_API_KEY=gsk_your_token_here

# Optional: change the model
HUGGINGFACE_MODEL=mistralai/Mistral-7B-Instruct-v0.3
```

### Step 3: Get a FREE API Key

#### Option A: Hugging Face (Recommended for beginners)
1. Sign up at [huggingface.co](https://huggingface.co) — completely free
2. Go to **Settings → Access Tokens**
3. Create a new token (read access is enough)
4. Copy it to `HUGGINGFACE_API_KEY` in `.env`
5. Free tier: ~30,000 tokens/month, public models

#### Option B: Groq (Recommended for speed — 10x faster!)
1. Sign up at [groq.com](https://console.groq.com) — completely free
2. Go to **API Keys** → Create API Key
3. Copy it to `GROQ_API_KEY` in `.env`
4. Free tier: **14,400 requests/day**, 500k tokens/minute
5. Models: `llama-3.1-8b-instant`, `mixtral-8x7b-32768`

### Step 4: Start MongoDB

```bash
# If MongoDB is installed locally:
mongod

# Or use MongoDB Atlas (cloud) - paste the connection string in .env
```

### Step 5: Run the App

```bash
# From root directory — runs both servers:
npm run dev

# Or run separately:
cd backend && npm run dev    # http://localhost:5000
cd frontend && npm start     # http://localhost:3000
```

Open **http://localhost:3000** 🎉

---

## 🏗️ Project Structure

```
anonymousthinker/
├── backend/
│   ├── server.js           # Express server entry point
│   ├── models/
│   │   ├── User.js         # User schema
│   │   ├── Conversation.js # Chat + messages schema
│   │   └── Training.js     # Personas + training examples
│   ├── routes/
│   │   ├── auth.js         # Register, login, /me
│   │   ├── chat.js         # CRUD conversations, send messages
│   │   └── training.js     # System prompts, training data
│   ├── middleware/
│   │   └── auth.js         # JWT verification
│   ├── config/
│   │   └── aiService.js    # HuggingFace & Groq API calls
│   └── .env                # Your API keys (don't commit!)
│
└── frontend/
    └── src/
        ├── App.js           # Router setup
        ├── context/
        │   ├── AuthContext.js   # Global auth state
        │   └── ChatContext.js   # Conversation state
        ├── pages/
        │   ├── LoginPage.js
        │   ├── RegisterPage.js
        │   ├── ChatPage.js      # Main chat interface
        │   └── TrainingPage.js  # AI training panel
        └── components/
            ├── Sidebar.js       # Chat history sidebar
            └── MessageBubble.js # Message rendering + markdown
```

---

## 🧬 How to Train Your AI

### Method 1: System Prompts (Easiest — No code needed)

Go to the **Train AI** page from the sidebar:
1. Click **"AI Personas"** tab
2. Write a system prompt that defines how the AI should behave
3. Click **"Activate"** to use it in all new chats

Example system prompt:
```
You are AnonymousThinker, a Socratic teacher. Instead of giving direct 
answers, guide users to discover insights through thoughtful questions. 
Be patient, encouraging, and help break down complex problems into 
manageable steps. Always end responses with a thought-provoking question.
```

### Method 2: Groq with Llama 3.1 (Free, Fast, Smart)

```bash
# Get Groq key at console.groq.com (free)
# Add to backend/.env:
GROQ_API_KEY=gsk_xxxxxxxxxxxx
```

The app automatically uses Groq if the key is set. Groq's Llama 3.1 models are:
- Much faster than HuggingFace (instant responses)
- Higher quality than smaller HuggingFace models
- 100% free up to 14,400 requests/day

### Method 3: Fine-tune on Hugging Face AutoTrain (Real Training!)

```bash
# Step 1: Add training examples in the Training page
# Step 2: Export data (click "Export Data" button)
# Step 3: Go to huggingface.co/autotrain
# Step 4: Create project → "Chat/Conversation" task
# Step 5: Upload your training_data.jsonl
# Step 6: Select base model: mistralai/Mistral-7B-Instruct-v0.3
# Step 7: Train (free tier available!)
# Step 8: Copy new model ID → update HUGGINGFACE_MODEL in .env
```

**Hugging Face AutoTrain Free Tier:**
- ~$1 in free credits monthly
- Enough to fine-tune on ~1000 examples
- Pay-as-you-go after that (~$0.001/example)

### Method 4: Local Training with Unsloth (Free, Unlimited, Private)

```bash
# Install Unsloth (optimized for consumer GPUs)
pip install unsloth

# Use the Google Colab notebook:
# https://colab.research.google.com/drive/1Ys44kVvmeZtnICzWz0xgpRnrIOjZAuxp

# Or run locally with Python:
python train_local.py  # (create this script using Unsloth docs)
```

### Method 5: OpenAI-Compatible APIs

The backend supports any OpenAI-compatible API. Change `aiService.js` to use:
- **Ollama** (localhost, completely free, privacy-first)
- **OpenRouter** (access to many models, free tier)
- **Together.ai** (fine-tuning, free credits)
- **Replicate** (free credits to start)

---

## 🔧 API Reference

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Create account |
| POST | `/api/auth/login` | Login |
| GET | `/api/auth/me` | Get current user |
| GET | `/api/chat/conversations` | List all chats |
| POST | `/api/chat/conversations` | Create new chat |
| GET | `/api/chat/conversations/:id` | Get specific chat |
| POST | `/api/chat/conversations/:id/message` | Send message |
| DELETE | `/api/chat/conversations/:id` | Delete chat |
| PUT | `/api/chat/conversations/:id` | Rename chat |
| GET | `/api/training/prompts` | List AI personas |
| POST | `/api/training/prompts` | Create persona |
| PUT | `/api/training/prompts/:id/activate` | Activate persona |
| GET | `/api/training/examples` | List training examples |
| POST | `/api/training/examples` | Add training example |
| GET | `/api/training/export` | Export JSONL data |

---

## 🚢 Deployment

### Deploy Backend (Railway/Render — Free)
```bash
# Railway.app (recommended):
railway login
railway init
railway up

# Add environment variables in Railway dashboard
```

### Deploy Frontend (Vercel — Free)
```bash
cd frontend
npm run build
vercel --prod

# Set API URL in Vercel env vars
```

### MongoDB Atlas (Free 512MB)
1. Create account at [cloud.mongodb.com](https://cloud.mongodb.com)
2. Create free cluster
3. Get connection string → update `MONGODB_URI` in `.env`

---

## 🔒 Security Notes

- Never commit `.env` files to git
- Change `JWT_SECRET` to a long random string in production
- Enable MongoDB authentication in production
- Add rate limiting for production (consider express-rate-limit)
- Use HTTPS in production

---

## 📝 License

MIT — Use it freely, build something awesome!
