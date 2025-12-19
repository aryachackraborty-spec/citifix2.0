# Hackspire (Citifix) — Local Run Instructions

This repository contains a Vite + React frontend and an Express backend in the `backend/` folder.

**Prerequisites**
- Node.js (>= 18 recommended)
- npm (comes with Node.js)

**Quick Start (one-time setup)**
1. Install root and frontend dependencies:

```powershell
cd "c:\Users\user\Pictures\hackathon\portfolio\hackspire 2.0"
npm install
```

2. Install backend dependencies:

```powershell
cd "c:\Users\user\Pictures\hackathon\portfolio\hackspire 2.0\backend"
npm install
```

**Run the project**
- Start frontend only (Vite dev server):

```powershell
cd "c:\Users\user\Pictures\hackathon\portfolio\hackspire 2.0"
npm run dev
```

- Start backend only (Express):

```powershell
cd "c:\Users\user\Pictures\hackathon\portfolio\hackspire 2.0\backend"
npm start
```

- Start both frontend and backend together (recommended for development):

```powershell
cd "c:\Users\user\Pictures\hackathon\portfolio\hackspire 2.0"
npm run dev:all
```

This uses the `concurrently` package. The frontend listens by default on port `3000` (Vite may choose an alternate port if `3000` is in use). The backend listens on port `5000` (or `process.env.PORT`).

**Build / Preview**
- Build frontend for production:

```powershell
npm run build
```

- Preview the production build:

```powershell
npm run preview
```

**Environment variables**
- The backend uses `process.env.PORT` if set. If your backend requires a database (Prisma), create a `.env` file under `backend/` containing something like:

```
PORT=5000
DATABASE_URL="postgresql://user:pass@localhost:5432/dbname"
```

Adjust the `DATABASE_URL` to your database setup. If you are not using a database locally, the backend currently responds at `/` for a health check.

**Health checks**
- Frontend (dev): `http://localhost:3000/` (or the port Vite prints when starting, e.g. `3001`)
- Backend: `http://localhost:5000/` (returns `Backend running successfully`)

**Troubleshooting**
- If the frontend auto-switches ports (e.g., to `3001`) it usually means `3000` was in use. To find the process using a port on Windows:

```powershell
netstat -ano | findstr ":3000"
```

Then kill the process (replace `<PID>` with the number):

```powershell
taskkill /PID <PID> /F
```

- If you want the frontend forced to a specific port, edit the `dev` script in `package.json` or pass `--port <port>` directly to `vite`.

**Stopping servers**
- In any terminal running a server, press `Ctrl+C`.

**Notes**
- `dev:all` runs two commands concurrently: `npm run dev` (frontend) and `npm --prefix backend start` (backend). If one of them fails, `concurrently` will keep the others running by default; check the terminal output for details.

If you'd like, I can:
- Automatically open the browser to the running frontend URL.
- Add a tiny health-check script to verify both services after startup.
- Add a `Makefile` or PowerShell script to simplify commands.
