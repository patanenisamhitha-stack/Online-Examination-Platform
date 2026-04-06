# ⚡ ExamPortal — MERN Stack Online Examination Platform

A full-stack online examination system built with **MongoDB + Express + React + Node.js**.

---

## 📁 Project Structure

```
examportal/
├── backend/               ← Node.js + Express + MongoDB REST API
│   ├── server.js          ← Main server file (all routes & models)
│   ├── package.json
│   └── .env               ← MongoDB URI + JWT secret
│
└── frontend/              ← React.js Single Page Application
    ├── public/
    │   └── index.html
    ├── src/
    │   ├── App.js         ← All React components (UI)
    │   ├── api.js         ← All API fetch calls (centralised)
    │   └── index.js       ← React entry point
    └── package.json       ← Includes "proxy": "http://localhost:5000"
```

---

## 🚀 Getting Started

### Prerequisites
- Node.js v18+
- MongoDB Community Server (https://www.mongodb.com/try/download/community)
- npm

---

### STEP 1 — Start MongoDB

**Windows:** MongoDB runs as a Windows Service after install (automatic)
**Mac/Linux:**
```bash
mongod --dbpath /usr/local/var/mongodb
```

---

### STEP 2 — Start the Backend

```bash
cd examportal/backend
npm install
npm run dev
```

Backend starts at: **http://localhost:5000**

You should see:
```
✅  MongoDB connected → mongodb://localhost:27017/examportal
🚀  ExamPortal Backend running at http://localhost:5000
```

---

### STEP 3 — Seed the Database (Run ONCE)

Open a browser or use curl to call the seed endpoint:

```bash
curl -X POST http://localhost:5000/api/seed
```

Or open **http://localhost:5000/api/seed** in Postman (POST request).

This creates:
- 3 users (1 admin + 2 students)
- 180 questions (20 per subject × 9 subjects)
- 10 exams (1 per subject + 1 MERN combined)

---

### STEP 4 — Start the Frontend

```bash
cd examportal/frontend
npm install
npm start
```

Frontend starts at: **http://localhost:3000**

> The `"proxy": "http://localhost:5000"` in frontend/package.json automatically forwards
> all `/api/*` requests to the backend — no CORS issues!

---

## 🔐 Login Credentials

| Role    | Email                  | Password    |
|---------|------------------------|-------------|
| Admin   | admin@exam.com         | admin123    |
| Student | mani@student.com       | student123  |
| Student | waseef@student.com     | student123  |
| Admin Registration Code | — | ADMIN2024 |

---

## 🗄️ MongoDB Collections

| Collection  | Purpose |
|-------------|---------|
| `users`     | Registered users (password is bcrypt-hashed) |
| `questions` | MCQ questions with 4 options each |
| `exams`     | Exam configs with linked question IDs |
| `results`   | Student exam submissions with scores |

---

## 🌐 API Endpoints

### Auth
| Method | Route | Description |
|--------|-------|-------------|
| POST | /api/auth/register | Register new user |
| POST | /api/auth/login | Login and get JWT token |
| POST | /api/auth/check-email | Check if email exists (forgot password step 1) |
| POST | /api/auth/forgot-password | Reset password |

### Questions (auth required)
| Method | Route | Description |
|--------|-------|-------------|
| GET | /api/questions | Get all questions |
| POST | /api/questions | Add question (admin only) |
| PUT | /api/questions/:id | Update question (admin only) |
| DELETE | /api/questions/:id | Delete question (admin only) |

### Exams (auth required)
| Method | Route | Description |
|--------|-------|-------------|
| GET | /api/exams | Get all exams (with populated questions) |
| POST | /api/exams | Create exam (admin only) |
| PUT | /api/exams/:id | Update exam (admin only) |
| DELETE | /api/exams/:id | Delete exam (admin only) |

### Results (auth required)
| Method | Route | Description |
|--------|-------|-------------|
| GET | /api/results | Get results (admin: all, student: own) |
| POST | /api/results | Submit exam result |

### Users (admin only)
| Method | Route | Description |
|--------|-------|-------------|
| GET | /api/users | Get all users |
| POST | /api/users | Add user |
| DELETE | /api/users/:id | Delete user |

---

## 📦 Subjects & Questions

| Subject | Questions |
|---------|-----------|
| JavaScript | 20 |
| React | 20 |
| MongoDB | 20 |
| Node.js | 20 |
| Express.js | 20 |
| Java | 20 |
| Python | 20 |
| C | 20 |
| C++ | 20 |
| **Total** | **180** |

---

## ☁️ Deploy to Cloud (Optional)

**Backend → Railway / Render:**
1. Push `backend/` to GitHub
2. Deploy on Railway or Render
3. Add environment variable: `MONGO_URI=mongodb+srv://...` (MongoDB Atlas)

**Frontend → Vercel / Netlify:**
1. Push `frontend/` to GitHub
2. Deploy on Vercel
3. Update `api.js` BASE URL from `/api` to your backend URL

---

## 🔧 .env Configuration

```env
MONGO_URI=mongodb://localhost:27017/examportal
JWT_SECRET=examportal_super_secret_key_2024
PORT=5000
```

For MongoDB Atlas (cloud):
```env
MONGO_URI=mongodb+srv://<username>:<password>@cluster0.xxxxx.mongodb.net/examportal
```
