

# iSDS — Intelligent Software Development System

This project uses Docker to run the iSDS backend (Python) and frontend (React/Vite) seamlessly on any machine, without needing to manually manage Node versions or Python virtual environments.

## Prerequisites

1. **Docker Desktop**: Download and install [Docker Desktop for Windows](https://docs.docker.com/desktop/install/windows-install/).
2. **WSL 2**: Ensure the "Use WSL 2 instead of Hyper-V" option is checked during Docker installation (this is the default on Windows 11).

---

## 📁 Expected Folder Structure

Before running, ensure your project folder looks exactly like this:

```text
iSDS_build/
├─ docker-compose.yml       <-- Orchestrates the containers
├─ backend/
│  ├─ Dockerfile            <-- Python 3.13.3 setup
│  ├─ app.py                <-- Main backend script
│  ├─ requirements.txt      
│  ├─ .env                  <-- YOU MUST CREATE THIS (see Step 1)
│  └─ pyarmor_runtime_000000/ <-- Linux-compiled PyArmor runtime
└─ frontend/
   ├─ Dockerfile            <-- Static file server setup
   └─ dist/                 <-- Pre-built React frontend files

```

---

## 🚀 Quick Start Guide

### Step 1: Environment Variables

Create a file named exactly `.env` inside the `backend/` folder. Add your required backend environment variables to this file.


### Step 2: Build and Run the Application

Open a terminal (PowerShell or Command Prompt) in the root `iSDS_build` folder and run:

```bash
docker-compose up -d --build

```

* `-d` runs the containers in the background (detached mode).
* `--build` forces Docker to read your latest files and rebuild the images.

### Step 4: Access the App

Once the terminal finishes processing, your application is live! Open your web browser and go to:

* **Frontend UI:** [http://localhost:3000](https://www.google.com/search?q=http://localhost:3000)
* **Backend API:** [http://localhost:5000](https://www.google.com/search?q=http://localhost:5000)

---

## 🛑 How to Stop the App

When you are done working, you can gracefully shut down the servers. In the root `iSDS_build` folder, run:

```bash
docker-compose down

```

---

## 🛠️ Common Troubleshooting
* **Port conflicts (e.g., "bind: address already in use" or "port is already allocated")**
  This error means another background application (or a previously crashed instance of this project) is already running on port `3000` (Frontend) or `5000` (Backend). You have two ways to solve this:

  **Option A: Find and kill the blocking process (Recommended)**
  1. Open your Windows **Command Prompt** or **PowerShell** as Administrator.
  2. To find out what is using port 3000, run:
     ```cmd
     netstat -ano | findstr :3000
     ```
  3. Look at the output. The number at the very end of the line is the Process ID (PID). For example, if you see `TCP  0.0.0.0:3000  ...  LISTENING  12345`, the PID is `12345`.
  4. Force quit that specific process by running this command (replace `12345` with your actual PID):
     ```cmd
     taskkill /PID 12345 /F
     ```
  5. Repeat the exact same steps using `:5000` if your backend port is the one blocked. 
  6. Run `docker-compose up -d` again.

  **Option B: Change the ports Docker uses**
  If you know what is using the port and don't want to close it, you can simply tell Docker to host your app on different ports.
  1. Open your `docker-compose.yml` file.
  2. Locate the `ports:` mapping. Docker maps ports using the `"HOST:CONTAINER"` format.
  3. Change the **first number** (the host port) to something else. 
     * To move the frontend, change `-"3000:3000"` to `-"3001:3000"` (It will now be accessible at `http://localhost:3001`).
     * To move the backend, change `-"5000:5000"` to `-"5001:5000"` (It will now be accessible at `http://localhost:5001`).
  4. Save the file and restart your containers with `docker-compose up -d`.
