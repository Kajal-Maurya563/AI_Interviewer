# 🤖 AI Interviewer

An AI-powered interview preparation tool that analyzes your resume and a job description to generate a personalized interview strategy — including technical questions, behavioral questions, a preparation roadmap, skill gap analysis, and even a tailored resume PDF.

---

## 💡 What It Does

You paste in a job description, upload your resume (or write a quick self-description), and the AI does the rest. It figures out where you stand, what questions you're likely to face, and gives you a day-by-day plan to get ready. It can also generate a polished resume PDF based on your profile and the target role.

---

## 🛠 Tech Stack

**Frontend** — React (Vite) + SCSS  
**Backend** — Node.js + Express + MongoDB  
**AI** — Google Gemini (via `google-genai`)  
**Auth** — JWT + bcrypt + HTTP-only cookies  
**PDF** — Puppeteer (generation) + pdf-parse (reading)

---

## 🏗 Architecture

This project follows a clean **4-layer architecture** on the frontend to keep things organized and easy to scale:

```
UI Layer          → Components & Pages (what the user sees)
Hooks Layer       → useAuth.js, useInterview.js (state + logic)
State Layer       → auth.context.jsx, interview.context.jsx (global state)
API Layer         → services/auth.api.js, services/interview.api.js (backend calls)
```

---

## 🚀 Getting Started

### Prerequisites

- Node.js v18+
- Python 3.9+ (for AI integration)
- MongoDB (local or Atlas)
- A Google Gemini API key

---

## 📦 Installation & Commands

### 1. Backend Setup

```bash
# Initialize Node.js project
npm init -y

# Core dependencies — server, database, environment variables
npm i express mongoose dotenv

# Auth dependencies — password hashing, JWT tokens, cookie handling
npm i bcryptjs jsonwebtoken cookie-parser

# Run the server with auto-restart
npx nodemon server.js
```

Create a `.env` file in the backend root:
```env
PORT=3000 or 8000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret_key
GEMINI_API_KEY=your_gemini_api_key
```

---

### 2. Frontend Setup

```bash
# Create React app with Vite
npm create vite@latest .

# Install dependencies
npm install

# Start development server
npm run dev

# SCSS styling support
npm i sass

# Connect frontend to backend
npm i axios
```

---

### 3. AI Integration Setup

> If you run into dependency conflicts, create a Python virtual environment first:
> ```bash
> python -m venv .venv
> .venv\Scripts\activate   # Windows
> source .venv/bin/activate  # Mac/Linux
> ```

```bash
# Google Gemini Python SDK
pip install -q -U google-genai

# Google Gemini Node.js SDK
npm install @google/genai

# Structured output validation
npm i zod
npm i zod-to-json-schema

# Handle resume file uploads
npm i multer

# Read content from uploaded PDF resumes
npm i pdf-parse

# Generate resume PDFs from AI output
npm i puppeteer
```

---

## 📁 Project Structure

```
Interview-ai/
├── Backend/
│   ├── server.js
│   ├── src/
│   │   ├── config/
│   │   │   └── database.js
│   │   ├── controllers/
│   │   │   └── auth.controller.js
│   │   ├── middlewares/
│   │   │   └── auth.middleware.js
│   │   ├── models/
│   │   │   ├── user.model.js
│   │   │   └── blacklist.model.js
│   │   └── routes/
│   │       └── auth.routes.js
│
└── Frontend/
    └── src/
        ├── features/
        │   ├── auth/
        │   │   ├── auth.context.jsx      ← AuthProvider (state)
        │   │   ├── AuthContext.js        ← AuthContext object
        │   │   ├── hooks/useAuth.js      ← auth logic & API calls
        │   │   ├── services/auth.api.js  ← axios requests
        │   │   ├── components/Protected.jsx
        │   │   └── pages/ (Login, Register)
        │   │
        │   └── interview/
        │       ├── interview.context.jsx      ← InterviewProvider
        │       ├── InterviewContext.js         ← InterviewContext object
        │       ├── hooks/useInterview.js       ← interview logic
        │       ├── services/interview.api.js   ← axios requests
        │       └── pages/ (Home, Interview)
        │
        ├── App.jsx
        ├── app.routes.jsx
        └── main.jsx
```

---

## 🔐 API Endpoints

| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| POST | `/api/auth/register` | Register new user | Public |
| POST | `/api/auth/login` | Login user | Public |
| GET | `/api/auth/logout` | Logout & blacklist token | Public |
| GET | `/api/auth/get-me` | Get current user | Private |
| POST | `/api/interview/` | Generate interview report | Private |
| GET | `/api/interview/` | Get all user reports | Private |
| GET | `/api/interview/report/:id` | Get report by ID | Private |
| POST | `/api/interview/resume/pdf/:id` | Generate resume PDF | Private |

---

## ✨ Features

- 🔐 Secure auth with JWT and HTTP-only cookies
- 📄 Resume upload (PDF/DOCX) or quick self-description input
- 🧠 AI-generated technical & behavioral interview questions
- 📅 Day-by-day preparation roadmap
- 📊 Match score and skill gap analysis
- 📥 Downloadable AI-generated resume PDF

---

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you'd like to change.

---

## 📄 License

[MIT](LICENSE)
