# DataBridge AI – Chat Interface

DataBridge AI is an **AI-driven data access platform** that allows users to connect third-party services like **Stripe, Zoho CRM, and GitHub**, and query their data using **natural language**.
The system securely fetches data using official APIs and presents **summaries and visualizations** through a chat-style interface.

---

## 🚀 Project Overview

### What This Project Does

* Connects to external platforms using user-provided credentials
* Accepts questions in plain English
* Makes **multiple API calls internally if required**
* Returns a **single meaningful result** with summaries and charts

### Key Principle

> The system does **not store or modify any business data**.
> It only fetches data temporarily using official APIs and user credentials.

---

## 🧱 Tech Stack

| Layer           | Technology               |
| --------------- | ------------------------ |
| Frontend        | HTML, CSS, JavaScript    |
| Backend         | Django REST Framework    |
| AI / Reasoning  | OpenAI / Gemini          |
| Workflow Engine | LangGraph                |
| Platforms       | Stripe, Zoho CRM, GitHub |
| Auth            | API Keys / OAuth Tokens  |

---

## 📌 Important Links & Credentials

### Zoho API Console

Used to manage OAuth client credentials.

* **Console Link**
  [https://api-console.zoho.in/client/1000.KIP35Q5XY5NCCSLHDHT1J4PZ9VI2BM](https://api-console.zoho.in/client/1000.KIP35Q5XY5NCCSLHDHT1J4PZ9VI2BM)

* **Client ID**
  `1000.KIP35Q5XY5NCCSLHDHT1J4PZ9VI2BM`

* **Redirect URI (Local)**

```text
http://localhost:8000/api/platforms/zoho/callback/
```

---

### Stripe Dashboard (Test Mode)

* **Dashboard Link**
  [https://dashboard.stripe.com/acct_1SpQgM2f4RjAwI8m/test/dashboard](https://dashboard.stripe.com/acct_1SpQgM2f4RjAwI8m/test/dashboard)

* Used for:

  * Viewing test transactions
  * Managing API keys
  * Monitoring invoices and payments

---

## 🔑 GitHub Personal Access Token (PAT) Guide

Used for accessing GitHub repositories via API.

### Steps to Generate a PAT

1. Log in to GitHub: [https://github.com](https://github.com)
2. Click profile photo → **Settings**
3. Go to **Developer settings**
4. Select **Personal access tokens**
5. Choose **Tokens (classic)**
6. Click **Generate new token (classic)**

### Recommended Settings

* **Name**: `DataBridge AI Token`
* **Expiration**: 30–90 days
* **Scopes**:

  * `repo`
  * `workflow`
  * `read:user`

⚠️ **Important**: Copy the token immediately. It cannot be viewed again.

---

## 🛠️ Project Setup

### 1️⃣ Backend (Django REST Framework)

```bash
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt

cp .env.example .env
# Add API keys and secrets in .env

python manage.py migrate
python manage.py runserver
```

Backend runs at:

```text
http://localhost:8000
```

---

### 2️⃣ Frontend (Static SPA)

```bash
# From project root
python -m http.server 5500
```

Access frontend at:

```text
http://localhost:5500
```

---

## 🔄 Architecture & Query Flow

The system uses a **multi-agent architecture** to process queries.

### Agent Flow

1. **Request Handler**

   * Receives user query from frontend

2. **Agent 1 – Classifier**

   * Detects target platform (Stripe / Zoho / GitHub)
   * Uses AI with keyword fallback

3. **Agent 2 – Planner**

   * Converts query into API actions & filters
   * Example:

     ```json
     {
       "action": "list_deals",
       "filters": {
         "amount_gt": 10000
       }
     }
     ```

4. **Agent 3 – Fetcher**

   * Calls platform APIs
   * Handles pagination and retries

5. **Agent 4 – Analyst**

   * Determines if visualization is needed
   * Prepares chart data (Bar, Line, Doughnut)

6. **Agent 5 – Summarizer**

   * Generates human-readable explanation
   * Uses AI only for summarization

---

## 🤖 OpenAI / Gemini Usage

* **Model**: `gpt-4o-mini`
* Used for:

  * Platform detection
  * Query interpretation
  * Result summarization

📌 **Security Note**
User credentials are **never shared** with OpenAI or Gemini.

---

## 📂 Project Structure

```text
frontend/
 ├── index.html
 ├── style.css
 └── app.js

backend/
 ├── manage.py
 ├── project_name/
 │   ├── settings.py
 │   └── urls.py
 └── app/
     ├── views.py
     ├── serializers.py
     └── models.py

agents/
 ├── ai_agent.py
 └── workflow.py
```

---

## ❓ Example Queries

### Stripe

* “Show unpaid invoices”
* “How much revenue did we make last week?”
* “List failed charges”

### Zoho CRM

* “Show won deals over 10k”
* “List contacts from Mumbai”
* “Breakdown deals by stage” *(Doughnut chart)*

### GitHub

* “Summarize facebook/react repository”
* “Show open pull requests”
* “List recent commits”

---

## 📦 Demo & Output

🎥 **Project Demo Videos**
[https://drive.google.com/drive/folders/1_h3QJw6ZSBbwxnYO4mf__wsdwwz0V49a](https://drive.google.com/drive/folders/1_h3QJw6ZSBbwxnYO4mf__wsdwwz0V49a)

---

## 📤 Pushing to GitHub

```bash
git init
git add .
git commit -m "Initial commit: DataBridge AI chat interface"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/REPO_NAME.git
git push -u origin main
```

🔑 Use **GitHub PAT** as password when prompted.

---

## ✅ Conclusion

DataBridge AI demonstrates:

* Secure API integration
* Multi-step AI reasoning
* Real-world backend workflows
* Scalable, platform-agnostic architecture

The project is designed to be **extensible**, **secure**, and **production-ready**.

---

