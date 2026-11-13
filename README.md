# ♞ Chess Arena &bull; CA-03 Submission

**Student Name:** Mithil Lanjewar  
**Roll No / PRN:** `25070521105`  
**Submission ID:** `25070521105-CA-03`  
**Repository:** `https://github.com/somesh-chutel/25070521105-CA-03.git`  
**Faculty / Instructor:** Prof. Somesh Chutel  
**Department & Section:** Computer Science & Information Technology &bull; SIT Section B  
**Tech Stack:** MongoDB Compass (`chess_arena`), Express.js 5, React 19, Node.js v22, React Router v7, Web Worker AI, Bootstrap  

---

## 🔑 Login Credentials (Pre-created in MongoDB)

You can log in at **[http://localhost:5000/login](http://localhost:5000/login)** or directly through the "Sign In" section on the home page.

### 1. Player Accounts (Created)
- **Primary Student Player (Mithil Lanjewar):**
  - **Role / Tab:** `Player`
  - **Username:** `mithil_lanjewar`
  - **Email:** `mithil.lanjewar@sitnagpur.edu.in`
  - **Password:** `password123`
  - **PRN:** `25070521105`
- **Secondary Demo Player:**
  - **Role / Tab:** `Player`
  - **Username:** `grandmaster_somesh`
  - **Email:** `somesh@sitnagpur.edu.in`
  - **Password:** `password123`
- **Capabilities:** Play matches vs AI or local, record finished games, review match history, and track win/loss/draw statistics.

### 2. Administrator Account (Created)
- **Role / Tab:** `Admin`
- **Username:** `admin`
- **Email:** `admin@chessarena.org`
- **Password:** `admin12345`
- **Capabilities:** Access the Control Room / Admin Dashboard, view registered player lists, monitor 24-hour match activity, and view total game metrics.

### 3. Guest Access (Instant Play)
- **Role:** Guest
- **Credentials:** None required.
- **How to use:** Click **"Play as guest →"** on the landing or login page to jump directly into a game.

### 4. Create a New Account
- Click **"Create an account"** on the login page to register any new player account. The credentials will be hashed using `bcrypt` (12 rounds) and saved into the MongoDB `users` collection.

---

## 📌 Project Architecture & Sir's Repository Structure
This application is organized into the exact two-tier structure (`client/` and `server/`) requested for Continuous Assessment 03 (CA-03):

```text
E:\new project 1\
├── client/                    # React 19 + Vite frontend
│   ├── public/                # Static assets (favicons, icons)
│   ├── src/
│   │   ├── assets/chess/      # Cinematic Queen and Parallax background
│   │   ├── components/        # Landing, Auth, Dashboards, Effects
│   │   ├── game/              # Chess engine, Web Worker, Synthesized Sound
│   │   ├── homeComp/
│   │   │   ├── header.jsx     # Header with MongoDB Compass status badge
│   │   │   ├── footer.jsx     # Academic footer with PRN & tech stack
│   │   │   └── mainContentCont.jsx # Container wrapper
│   │   ├── nav.jsx            # Top Navigation with Routes
│   │   ├── home.jsx           # Main Chess Arena (Game, AI, Dashboards, Landing)
│   │   ├── about.jsx          # Chess evolution, Minimax engine & MongoDB architecture
│   │   ├── services.jsx       # AI engine, move evaluation & match tracking services
│   │   ├── contact.jsx        # Contact inquiry & faculty submission desk
│   │   ├── LoginPage.jsx      # Dedicated Login & Registration page (/login)
│   │   ├── ChessGame.jsx      # Interactive chessboard component
│   │   ├── ChessGame.css      # Board theme & piece animations
│   │   ├── App.jsx            # React Router DOM Route mappings
│   │   ├── App.css            # Cinematic styling + Sir's nav classes
│   │   └── main.jsx           # Root entry point with BrowserRouter
│   ├── index.html
│   ├── package.json
│   └── vite.config.js
├── server/                    # Express 5 REST API + MongoDB backend
│   ├── server.js              # Express 5 REST API using MongoDB driver
│   ├── db.js                  # MongoDB client connection & indexes
│   ├── create-admin.js        # CLI utility to seed admin accounts in MongoDB
│   ├── package.json           # Backend dependencies (mongodb, bcrypt, jwt, cors)
│   └── .env                   # JWT secret, MongoDB URI, Port 5000
├── package.json               # Root scripts (npm start, npm run server, npm run client)
└── README.md                  # Project documentation & credentials
```

---

## 🍃 MongoDB Schema & Collections
- **Database:** `chess_arena` (Host: `mongodb://127.0.0.1:27017`)
- **`users` Collection**:
  - `_id`: ObjectId
  - `username`: String (Unique index)
  - `email`: String (Unique index)
  - `password_hash`: String (Bcrypt salted hash with 12 rounds)
  - `role`: `'user'` | `'admin'`
  - `createdAt`: Date
- **`games` Collection**:
  - `_id`: ObjectId
  - `user_id`: ObjectId (References `users._id`)
  - `username`: String
  - `mode`: `'ai'` | `'local'`
  - `difficulty`: `'easy'` | `'medium'` | `'hard'`
  - `player_color`: `'w'` | `'b'`
  - `result`: `'win'` | `'loss'` | `'draw'` | `'white'` | `'black'`
  - `reason`: String (`checkmate`, `stalemate`, `resignation`, etc.)
  - `moves`: Integer
  - `pgn`: String (Full PGN notation)
  - `createdAt`: Date

---

## 🛠️ API Reference

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `GET` | `/api/health` | Public | Health check and active MongoDB database name |
| `POST` | `/api/auth/register` | Public | Register new player with bcrypt hashed password |
| `POST` | `/api/auth/login` | Public | Verify credentials and return signed JWT token |
| `GET` | `/api/auth/me` | JWT | Get current signed-in user profile |
| `POST` | `/api/games` | JWT | Save a finished game to MongoDB |
| `GET` | `/api/games/me` | JWT | Retrieve player match history and win/loss totals |
| `GET` | `/api/admin/stats` | Admin | Total players, total games, 24h activity |
| `GET` | `/api/admin/users` | Admin | Aggregate player list with game and win counts |

---

## 🚀 How to Run the Project

### 1. Ensure MongoDB Compass / Service is Running
Make sure MongoDB is running locally at:
```text
mongodb://127.0.0.1:27017
```

### 2. Start the Unified Server (UI + API on Port 5000)
```bash
npm start
# Opens on http://localhost:5000
```

### 3. Or Run Frontend in Vite Development Mode
```bash
# Terminal 1: Backend
npm run server

# Terminal 2: Frontend
npm run client
# Vite dev server opens on http://localhost:5173
```
