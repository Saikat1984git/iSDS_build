# iSDS — Intelligent Software Development System

A clear, step-by-step README to get the project running locally (backend: Python, frontend: React + Vite). Designed so even a beginner can follow it.

---

## Prerequisites (install these first)

* **Git** — to clone the repo.
* **Python 3.10+** (or 3.8+) — includes `venv`. Verify with `python --version`.
* **Node.js 18+** and **npm** — verify with `node --version` and `npm --version`.
* Basic terminal/command prompt comfort.

---

## Quick start (copy-paste these commands)

Open **TWO separate terminals** (one for backend, one for frontend).

### 1) Clone the repo

```bash
git clone https://github.com/Saikat1984git/iSDS-intelligent-software-development-system.git
cd iSDS-intelligent-software-development-system
```

---

### 2) Backend (Python)

*Assumes backend code is inside a folder named `backend` (adjust paths if your layout differs).*

**Important:** paste the given `.env` file into the backend folder with the exact file name `.env` (no extension). Example path:

```
iSDS-intelligent-software-development-system/backend/.env
```

#### Create & activate virtual environment

Linux / macOS:

```bash
cd backend
python -m venv venv
source venv/bin/activate
```

Windows (Command Prompt):

```cmd
cd backend
python -m venv venv
venv\Scripts\activate
```

Windows (PowerShell):

```powershell
cd backend
python -m venv venv
.\venv\Scripts\Activate.ps1
# If you get an execution policy error, run PowerShell as admin and:
# Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

#### Install Python dependencies

```bash
# from backend folder
pip install -r requirements.txt
```

> If you see a filename mismatch like `requiremnets.txt`, list files in the folder (`ls` or `dir`) and use the exact filename you find.

#### Run the backend

```bash
# from backend folder with venv activated
python app.py
```

This typically starts the Python server (commonly on `http://127.0.0.1:5000` or a port printed to your terminal). Check the terminal logs for the exact URL.

---

### 3) Frontend (React + Vite)

Open the second terminal.

```bash
cd iSDS-intelligent-software-development-system/frontend
npx serve -s dist
```

Vite typically serves at `http://localhost:3000` (check the terminal for the exact URL).

---

## Notes for next time

You **do not need** to run `npm i` or `pip install -r requirements.txt` every time. Do those **once** (or whenever dependencies change). Next time:

* Activate the Python venv and run `python app.py`.
* Start frontend with `npm run dev`.

---

## Typical folder structure (expected)

```
iSDS-intelligent-software-development-system/
├─ backend/
│  ├─ app.py
│  ├─ requirements.txt
│  └─ .env         <-- paste your provided .env here
└─ frontend/
   ├─ package.json
   └─ (Vite + React source files)
```

If your repository has different folder names, adjust the `cd` paths above.

---

## Common issues & fixes

* **`python` command not found**

  * Use `python3` on some systems, or add Python to PATH during install.
* **Virtualenv activation fails on Windows PowerShell**

  * Run: `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` in an elevated PowerShell (only if you trust the scripts).
* **`requirements.txt` not found**

  * Check folder contents with `ls` / `dir`. Use the exact filename. If the repo uses a different name, adapt the command.
* **Port conflicts**

  * If port `5173` or `5000` is already in use, Vite or Flask will show that — either stop the process using that port or run on a different port. For Flask you can often set `FLASK_RUN_PORT=XXXX` or edit `app.py` to bind a different port.
* **Frontend can’t reach backend**

  * Ensure backend is running and that frontend requests target the correct backend URL/port. If the frontend uses a proxy, check `vite.config.js` or environment variables.
* **Dependency installation slow or fails**

  * Use a stable network; for `pip` consider `pip install --upgrade pip` then `pip install -r requirements.txt`.
  * For node, remove `node_modules` and `package-lock.json` then `npm i` if broken.

---

## Helpful commands summary

From repository root:

```bash
# Backend
cd backend
python -m venv venv
# Activate (choose appropriate command above)
pip install -r requirements.txt
python app.py

# Frontend (in a new terminal)
cd frontend
npm i         # only first time
npx serve -s dist
```

To stop servers: use `Ctrl+C` in the terminal where they're running.

---

## Testing & sanity checks

* After backend starts, open its URL from the terminal (likely `http://127.0.0.1:5000`) and confirm a health or root endpoint responds.
* After frontend starts, open the Vite URL (likely `http://localhost:3000`) and verify the UI loads.
* If UI shows errors related to API calls, open browser DevTools → Network / Console to inspect failing requests and their target URLs.

---

## If something still fails

* Copy the terminal error and search the message (or paste here) — include the error text and which step you ran. I’ll debug it with you.
* If you prefer, paste the exact `.env` keys (NOT secrets) or the output of `ls backend` and `ls frontend` so I can tailor steps.

---

## License & credits

Keep or add a license file if you plan to publish. Credit authors and libraries in `package.json` and `requirements.txt`.

---

That’s it — you should be up and running. I kept the steps explicit and cross-platform so a newbie can follow them. If you want, I can also:

* create a one-liner script to start both servers, or
* produce a `.bat` / `.sh` helper for your machine.
