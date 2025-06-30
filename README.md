
# 💬 RBI Legal Chatbot

An AI-powered legal assistant that answers queries related to **RBI regulations**, including Acts, Rules, and Case Laws from the **Supreme Court, High Court, NCLT, and NCLAT**.

It features:

* 🧠 LLM-based answers using LangChain + Chroma
* ⚡ Auto-start and auto-shutdown of FastAPI backend
* 🖥️ React frontend with a modern legal research UI
* 🔁 Node.js proxy server with idle timeout management

---

## 📁 Project Structure

```
RBI-catbot-main/
├── backend/
│   ├── main.py              # FastAPI backend app
│   ├── diffchroma.py        # Builds Chroma vectorstore from data
│   ├── start_fastapi.bat    # Windows startup script for backend
│   └── start_fastapi.sh     # Unix/MacOS startup script for backend
├── data/                    # 📂 Pre-uploaded PDFs (Acts, Rules, Case Laws)
├── frontend/
│   └── IBChatbot.js         # React chatbot UI
├── server.js                # Node.js proxy server with auto backend control
└── README.md
```

---

## 📦 Setup Instructions

### 1. 🧾 Data Preparation (No download needed)

All required PDFs (Acts, Rules, and Case Laws) are already uploaded under the `data/` folder.

To create the Chroma vector DB:

```bash
python backend/diffchroma.py
```

This will embed the documents and prepare them for fast retrieval using LangChain + Chroma.

---

### 2. ⚙️ FastAPI Backend

Make sure `main.py` contains your FastAPI app (not `check.py`).
Startup command in `start_fastapi.bat` or `start_fastapi.sh` should be:

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

> This is automatically used by `server.js`.

---

### 3. 🚀 Node.js Proxy (Backend Manager)

Start the Node proxy server:

```bash
npm install
node server.js
```

This will:

* Automatically start the FastAPI server using the correct OS script
* Shut it down after **2 minutes** of inactivity
* Forward all `/api` requests to the FastAPI backend

---

### 4. 🖥️ React Frontend (Chatbot UI)

```bash
cd frontend
npm install
npm start
```

Access the chatbot at: [http://localhost:3000](http://localhost:3000)

---

## 🔁 Backend Lifecycle (via `server.js`)

| Endpoint                     | Purpose                             |
| ---------------------------- | ----------------------------------- |
| `POST /api/start-backend`    | Manually start FastAPI backend      |
| `POST /api/shutdown-backend` | Manually stop FastAPI backend       |
| `GET  /api/backend-status`   | Health check of FastAPI backend     |
| All `/api/*` requests        | Proxied to FastAPI running on :8000 |

---

## ✅ Features

* Multi-source legal Q\&A (Acts, Rules, SC, HC, NCLT, NCLAT)
* React UI with clipboard, notes, download options
* FastAPI auto-managed from Node.js
* Efficient embedding via LangChain + Chroma
