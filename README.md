









![Python](https://img.shields.io/badge/Python_3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask_3.1-000000?style=for-the-badge&logo=flask&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Groq](https://img.shields.io/badge/Groq_AI-F55036?style=for-the-badge&logo=groq&logoColor=white)
![Railway](https://img.shields.io/badge/Railway-0B0D0E?style=for-the-badge&logo=railway&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)




![Status](https://img.shields.io/badge/Status-Live_%26_Deployed-22c55e?style=flat-square&logo=checkmarx&logoColor=white)
![Built](https://img.shields.io/badge/Built_In-48_Hours-f59e0b?style=flat-square&logo=lightning&logoColor=white)
![AI](https://img.shields.io/badge/AI-Llama_3.1_Powered-8b5cf6?style=flat-square&logo=openai&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)
![Commits](https://img.shields.io/badge/Commits-16-orange?style=flat-square&logo=git&logoColor=white)





[🔗 **Live Demo**](https://care-connect-production-6258.up.railway.app)  · 
[📂 **Source Code**](https://github.com/sumit90asa-coder/Care-Connect)  · 
[👤 **Author**](#-author)  · 
[🚀 **Quick Start**](#-quick-start)




---

## 📖 About The Project

> 🏆 **Built and deployed solo at Tech Fest Hackathon in under 48 hours** using an AI-augmented development workflow.

**Care-Connect** is a full-stack health and wellness community platform where users receive **real AI-powered wellness guidance** through Groq's ultra-fast LLM inference, yoga content, personalised daily tips, and a fully secure authenticated experience.

What makes this stand out:
- 🤖 **Real AI** — Groq + Llama 3.1 for millisecond AI responses, not scripted chatbots
- 🔐 **Production security** — Werkzeug bcrypt hashing, Flask sessions, protected routes throughout
- 🚀 **Actually deployed** — live on Railway with a managed MySQL production database
- ⚡ **Built fast** — complete full-stack application in 48 hours using AI-assisted development

```
📊 Language Breakdown
████████████████████████████░░░░░░░░░░░░░░░  HTML   52.4%
██████████████░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  CSS    26.0%
███████████░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  Python 21.5%
```

---

## ✨ Features




### 🤖 AI Wellness Chatbot
Real-time chatbot powered by **Groq API + Llama 3.1 (8B Instant)**. Groq's LPU delivers millisecond inference — far faster than standard OpenAI calls. Returns supportive, wellness-focused responses via JSON endpoint.

	

### 🔐 Secure Authentication
Full register/login flow with **Werkzeug bcrypt** password hashing. Duplicate email detection, proper error messaging, and Flask session-based auth guards on every protected page.




### 👤 Detailed User Profiles
Stores user **title, full name, nationality, gender, date of birth, mobile, and email** in a structured MySQL schema. Auto-created on first run.

	

### 🧘 Yoga & Wellness Section
Dedicated **yoga page** with guided content + a bank of **10 rotating daily wellness tips** served randomly each session to keep content fresh.




### 🛡️ Protected Routes
**Every** post-login page is session-guarded. Unauthenticated requests are automatically redirected to login — no unauthorized access possible.

	

### 🚀 Production Deployed
Live on **Railway** with Railway-managed MySQL, environment variables, Gunicorn WSGI server, Procfile config, and a `/health` health check endpoint.




---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Backend** | Python 3.10+, Flask 3.1, Werkzeug 3.1, python-dotenv |
| **AI / LLM** | Groq API, Llama 3.1 8B Instant, httpx |
| **Frontend** | HTML5, CSS3, JavaScript ES6+, Jinja2 |
| **Database** | MySQL (Railway managed), mysql-connector-python |
| **Deployment** | Railway, Gunicorn 21.2, Procfile, railway.toml |

---

## 🏗️ Architecture

```
┌─────────────┐     HTTP      ┌─────────────────────────┐
│   Browser   │ ───────────► │      Flask App (app.py)  │
│  HTML/CSS/JS│ ◄─────────── │  Routes · Auth · Sessions│
└─────────────┘   Jinja2 HTML └────────────┬────────────┘
                                            │
                          ┌─────────────────┼──────────────┐
                          ▼                 ▼              ▼
                    ┌──────────┐    ┌──────────────┐  ┌──────────┐
                    │  MySQL   │    │   Groq API   │  │ Railway  │
                    │(Railway) │    │  Llama 3.1   │  │  Deploy  │
                    └──────────┘    └──────────────┘  └──────────┘
```

---

## 🔌 API Routes

| Method | Route | Auth | Description |
|:---:|---|:---:|---|
| `GET` | `/` | ✗ | Redirects to login |
| `GET` `POST` | `/register` | ✗ | User registration with validation |
| `GET` `POST` | `/login` | ✗ | Secure login with bcrypt hash check |
| `GET` | `/dashboard` | ✅ | User profile dashboard |
| `GET` | `/wellness` | ✅ | Random daily wellness tip |
| `GET` | `/yoga` | ✅ | Yoga & mindfulness page |
| `GET` | `/chatbot` | ✅ | AI chatbot UI |
| `POST` | `/chat` | ✅ | **Groq AI JSON endpoint** |
| `GET` | `/logout` | ✅ | Clear session + redirect |
| `GET` | `/health` | ✗ | Railway health check |

---

## 🤖 AI Integration

The `/chat` endpoint uses **Groq API** with **Llama 3.1 (8B Instant)** for near-instant AI wellness responses:

```python
@app.route("/chat", methods=["POST"])
def chat():
    message = request.json.get("message", "")
    
    # Ultra-fast inference via Groq's LPU hardware
    response = client.chat.completions.create(
        model="llama-3.1-8b-instant",
        messages=[
            {
                "role": "system",
                "content": "You are a friendly, supportive wellness assistant. Be calm and encouraging."
            },
            {"role": "user", "content": message}
        ],
        temperature=0.6,
        max_tokens=200
    )
    
    reply = response.choices[0].message.content
    return jsonify({"response": reply})
```

> 💡 **Why Groq?** Groq's LPU (Language Processing Unit) hardware delivers token generation speeds far beyond standard GPU inference — making the chatbot feel instant.

---

## 🚀 Quick Start

### Prerequisites
- Python 3.10+
- MySQL running locally  
- Free Groq API key → [console.groq.com](https://console.groq.com)

```bash
# 1️⃣ Clone the repo
git clone https://github.com/sumit90asa-coder/Care-Connect.git
cd Care-Connect

# 2️⃣ Create virtual environment
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # Mac / Linux

# 3️⃣ Install all dependencies
pip install -r requirements.txt
```

**4️⃣ Create `.env` file:**
```env
SECRET_KEY=your_secret_key_here
GROQ_API_KEY=your_groq_api_key_here
MYSQLHOST=localhost
MYSQLUSER=root
MYSQLPASSWORD=your_mysql_password
MYSQLDATABASE=careconnect
MYSQLPORT=3306
```

```bash
# 5️⃣ Create MySQL database (tables auto-created on first run)
mysql -u root -p -e "CREATE DATABASE careconnect;"

# 6️⃣ Run the app
python app.py
# ✅ Visit → http://localhost:8080
```

---

## 📦 Dependencies

```
Flask==3.1.0
gunicorn==21.2.0
mysql-connector-python==8.3.0
python-dotenv==1.0.1
groq==0.28.0
httpx==0.27.2
Werkzeug==3.1.0
```

---

## 📁 Project Structure

```
Care-Connect/
│
├── 📄 app.py               # Flask app — all routes, DB logic, AI integration
├── 📄 requirements.txt     # All Python dependencies
├── 📄 Procfile             # Gunicorn config for Railway deployment
├── 📄 railway.toml         # Railway build & deploy settings
├── 📄 .gitignore           # Excludes .env, venv, __pycache__
│
├── 📁 static/              # CSS stylesheets, JavaScript, images
└── 📁 templates/           # Jinja2 HTML templates
    ├── login.html          # Login page
    ├── register.html       # Registration form
    ├── dashboard.html      # User profile dashboard
    ├── chatbot.html        # AI wellness chat interface
    ├── wellness.html       # Daily wellness tips
    └── yoga.html           # Yoga & mindfulness content
```

---

## 🌐 Deployment

Deployed on **Railway** with full production setup:

| Config | Detail |
|---|---|
| **Server** | Gunicorn WSGI (`gunicorn app:app`) |
| **Database** | Railway managed MySQL |
| **Env Vars** | Set via Railway dashboard |
| **Auto Deploy** | On every `git push` to main |
| **Health Check** | `/health` endpoint |

---

## 👨‍💻 Author




**Sumit Soni** — BSc IT Student @ KC College Mumbai

*"Built this in 48 hours at a hackathon using Python, Flask, Groq AI, and AI-augmented development. Always building something new."*




[![LinkedIn](https://img.shields.io/badge/LinkedIn-sumit--soni--dev-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/sumit-soni-dev)
[![GitHub](https://img.shields.io/badge/GitHub-sumit90asa--coder-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/sumit90asa-coder)
[![Internship](https://img.shields.io/badge/Open_To-Remote_Internships-22c55e?style=for-the-badge&logo=briefcase&logoColor=white)](https://linkedin.com/in/sumit-soni-dev)




---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---






**⭐ If Care-Connect helped or inspired you, please star the repo!**

*Built with Python 🐍 · Flask 🌶 · Groq AI 🤖 · and coffee ☕ at 3am during a hackathon*

