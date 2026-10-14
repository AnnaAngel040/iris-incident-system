# ⚡ IRIS — Intelligent Resolution Incident System
### *Organizational Knowledge & Closed-Loop Incident Resolution Platform*
**Course:** Database Systems &bull;

---

## 📌 Problem Statement: The Incident Resolution Crisis

Modern engineering organizations face two major roadblocks during production outages:
1. **The "Tribal Knowledge" Trap:** Critical debugging knowledge is trapped in the heads of a few senior engineers or scattered across lost Slack messages, closed tickets, and unmaintained wikis. When a critical issue occurs and that engineer is unavailable, teams waste hours diagnosing the exact same failure from scratch.
2. **The Disconnected AI & Ticketing Gap:** Traditional ticketing tools (e.g., Jira) are passive storage lockers that do not actively diagnose issues. Meanwhile, generic AI models (e.g., ChatGPT) have no awareness of your internal infrastructure, architecture, or past organizational incident history.

---

## 💡 What is IRIS?

**IRIS (Intelligent Resolution Incident System)** is a **database-centric incident intelligence platform** that unifies relational historical data with automated root-cause diagnosis. 

Instead of treating incident logs as dead text, IRIS places a **relational database at the center** of incident management:
- **Instant Retrieval:** Runs high-speed SQL queries to fetch historical precedents and past validated solutions.
- **Deep Diagnosis:** Synthesizes root causes, step-by-step resolution checklists, and confidence ratings.
- **Closed-Loop Learning:** Ingests accepted fixes back into the relational schema with foreign key integrity, making the organization progressively smarter with every resolved issue.

> **Core Philosophy:** *"Fix an incident once, and your entire organization never spends time diagnosing it again."*

---

## 🌟 Why is IRIS Necessary?

- ⏱️ **Drastically Reduces MTTR (Mean Time to Resolution):** Cuts down diagnosis time from hours of guesswork to sub-second SQL lookups and targeted action steps.
- 🧠 **Compounds Institutional Memory:** Every resolved problem immediately expands the database knowledge base for all future queries.
- 🛡️ **Empowers On-Call & Junior Engineers:** Provides step-by-step actionable playbooks backed by historical organizational precedents.
- 🔍 **Real-Time SQL Auditability:** Features real-time query logging (`sql_query_logs`) capturing query text, latency, execution timestamps, and rows affected.
- 🔒 **Relational Data Integrity:** Enforces foreign key relationships, cascade constraints, indexed searches, and normalized schemas.

---

## 🛠️ Tech Stack

| Layer | Technology | Role |
|---|---|---|
| **Backend Framework** | **Python 3** / **FastAPI** | High-performance asynchronous REST API backend. |
| **ASGI Server** | **Uvicorn** | Lightweight, lightning-fast ASGI server. |
| **Data Validation** | **Pydantic v2** | Strict schema validation and typed data models. |
| **Database Engine** | **SQLite 3** | Embedded relational database with foreign key support (`PRAGMA foreign_keys = ON;`) and indexing. |
| **Frontend UI** | **Vanilla JavaScript (ES6+)** / **HTML5** | Interactive Single-Page Application (SPA) without heavy build toolchains. |
| **Styling & Icons** | **Tailwind CSS** (CDN) / **FontAwesome** | Dark-mode UI with live query boxes, preset selectors, and table explorers. |

---

## 🧠 How It Works: The Closed-Loop Flow

```
 [User / Engineer]
        │
        ▼
 1. Log Incident (Title, Description, Category, Severity, Keywords)
        │
        ├─────────────────────────────────────────┐
        ▼                                         ▼
 2. INSERT into `problems` (Status: 'OPEN')   Audit log to `sql_query_logs`
        │
        ▼
 3. Relational Knowledge Retrieval (SQL JOIN on `problems` & `solutions`)
        │
        ▼
 4. AI Engine Diagnostic Synthesis
    ├─ Match against historical precedents
    ├─ Identify Root Cause & Action Steps
    └─ Compute Confidence Score %
        │
        ▼
 5. Closed-Loop Ingestion
    ├─ INSERT new record into `solutions` (FK -> problems.id)
    └─ UPDATE `problems` (SET status = 'RESOLVED', resolved_at = NOW)
        │
        ▼
 6. Knowledge Base Expanded (Immediately queryable by future incidents)
```

---

## 🗄️ Relational Database Schema

```text
+------------------------------------+          +--------------------------------------+
|             PROBLEMS               | 1      N |              SOLUTIONS               |
+------------------------------------+----------+--------------------------------------+
| id (PK, INTEGER AUTOINCREMENT)     |          | id (PK, INTEGER AUTOINCREMENT)       |
| title (VARCHAR NOT NULL)           |          | problem_id (FK -> problems.id)       |
| description (TEXT NOT NULL)        |          | solution_text (TEXT NOT NULL)        |
| category (VARCHAR NOT NULL, INDEX) |          | source (VARCHAR DEFAULT 'AI')        |
| severity (VARCHAR NOT NULL)        |          | confidence_score (REAL)              |
| keywords (VARCHAR)                 |          | root_cause (TEXT)                    |
| status (VARCHAR, INDEX)            |          | action_steps (TEXT)                  |
| created_at (TIMESTAMP)             |          | created_at (TIMESTAMP)               |
| resolved_at (TIMESTAMP)            |          +--------------------------------------+
+------------------------------------+
                  |
                  v
+------------------------------------+
|          SQL_QUERY_LOGS            |
+------------------------------------+
| id (PK, INTEGER AUTOINCREMENT)     |
| query_type (VARCHAR NOT NULL)      |
| query_text (TEXT NOT NULL)         |
| params (TEXT)                      |
| rows_affected (INTEGER)            |
| execution_time_ms (REAL)           |
| timestamp (TIMESTAMP)              |
+------------------------------------+
```

---

## 🚀 How to Run the Project

### 1. Prerequisites
Ensure you have **Python 3.8+** installed on your system.

### 2. Install Dependencies
In your terminal, navigate to the project directory and install the required packages:
```powershell
pip install -r requirements.txt
```

### 3. Launch the Server

Choose any of the following methods to start the application:

#### Method A: PowerShell Script
```powershell
.\run.ps1
```

#### Method B: Batch File (Windows)
Double-click `run.bat` or execute:
```cmd
run.bat
```

#### Method C: Direct Python
```powershell
cd backend
python main.py
```

### 4. Open in Browser
Once the server starts, open your browser and go to:
👉 **[http://localhost:8000](http://localhost:8000)**

---

## 🎯 1-Minute Live Demo Walkthrough

### Step 1: Open the App & Explain the Vision
- **Explain:** *"Traditional systems like Jira only store text tickets passively, while ChatGPT lacks internal organizational history. IRIS is an Organizational Incident Database where the relational database is the centerpiece."*

### Step 2: Log a New Incident
- Click one of the Demo Presets (e.g., **"Postgres Connection Timeout"** or type a custom problem).
- Click **"Log to Database & Analyze with IRIS"**.
- Highlight the real-time **SQL Query Box**:
  ```sql
  SELECT p.id, p.title, s.solution_text, s.confidence_score
  FROM problems p
  JOIN solutions s ON p.id = s.problem_id
  WHERE ...
  ```
- **Explain:** *"Notice that before AI generates anything, the database performs a relational JOIN on our historical organizational records to extract validated past solutions."*

### Step 3: Review AI Root-Cause Synthesis
- Point out the **Root Cause Diagnosis**, **Recommended Primary Solution**, **Actionable Steps Checklist**, and **Confidence Score**.

### Step 4: Closed-Loop Decision & Database Update
- Click **"Accept AI Recommendation & Ingest into SQL"** (or enter a custom fix).
- Switch to the **Database Explorer** tab to verify:
  1. The new record inserted into the `solutions` table with foreign key `problem_id`.
  2. The `problems` table record updated to `status = 'RESOLVED'`.
  3. The `sql_query_logs` table tracking every query execution with millisecond timing.

---

## 👥 Contributors & Academic Context
Developed for **DBMS Review 1 Evaluation** &bull; Department of Computer Science & Engineering, **VIT Vellore**.
