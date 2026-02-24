# VoiceIQ — AI-Powered Customer Support Intelligence Platform

> Transform raw call recordings into actionable insights with AI-driven analysis, automated scoring, and a real-time dashboard for customer support teams.

---

## 📌 Overview

**VoiceIQ** is an end-to-end customer support intelligence platform that automatically ingests call recordings via **Kaleyra webhooks**, analyzes conversations using **AI agents**, and surfaces performance metrics through a **React + TypeScript** dashboard with role-based access control.

Built on a Python backend with Firebase for data persistence and Azure for cloud infrastructure, VoiceIQ empowers support managers to monitor agent performance, identify coaching opportunities, and improve customer experience — all without manual review.

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      VoiceIQ Platform                       │
├───────────────┬─────────────────────┬───────────────────────┤
│  Kaleyra API  │   Python Backend    │  React + TypeScript   │
│  (Webhooks)   │   (app.py / Flask)  │     Dashboard (UI)    │
│               │                     │                       │
│  Call events ─┼─► Transcription    │  Role-Based Access    │
│  Recordings   │   AI Agent Analysis │  Performance Scores   │
│               │   Scoring Engine    │  Call Analytics       │
│               │   Firebase Write    │  Agent Leaderboards   │
└───────────────┴────────┬────────────┴───────────────────────┘
                         │
              ┌──────────▼──────────┐
              │  Firebase / Azure   │
              │  (Storage + DB)     │
              └─────────────────────┘
```

---

## ✨ Key Features

- **Automated Call Ingestion** — Receives call recording events in real time through Kaleyra webhook integration
- **AI Conversation Analysis** — Multi-agent AI pipeline transcribes, understands, and evaluates customer-agent interactions
- **Performance Scoring Engine** — Generates objective scores across dimensions like empathy, resolution, compliance, and tone
- **Actionable Insights** — Surfaces specific coaching recommendations and call highlights for supervisors
- **Role-Based Access Control** — Separate views and permissions for Agents, Supervisors, and Admins
- **Real-Time Dashboard** — React + TypeScript frontend with live data from Firebase
- **Azure Infrastructure** — Scalable cloud deployment for transcription and AI workloads

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React, TypeScript, Vite, Tailwind CSS |
| Backend | Python (Flask / FastAPI via `app.py`) |
| Database | Firebase Firestore |
| Storage | Firebase Storage / Azure Blob Storage |
| Telephony | Kaleyra (Webhooks & Call Recordings) |
| AI / ML | Azure AI Services, LLM-based Agents |
| Dev Tooling | ESLint, PostCSS, TypeScript (strict) |

---

## 📁 Project Structure

```
VoiceIQ/
├── public/                  # Static assets
├── src/                     # React + TypeScript frontend
│   ├── components/          # Reusable UI components
│   ├── pages/               # Route-level page components
│   ├── hooks/               # Custom React hooks
│   ├── services/            # Firebase & API service layers
│   └── types/               # TypeScript interfaces & types
├── app.py                   # Python backend (webhook handler + AI pipeline)
├── .env                     # Environment variables
├── index.html               # App entry point
├── vite.config.ts           # Vite build configuration
├── tailwind.config.js       # Tailwind CSS configuration
├── tsconfig.json            # TypeScript configuration
└── package.json             # Node dependencies
```

---

## ⚙️ Getting Started

### Prerequisites

- **Node.js** v18+
- **Python** 3.10+
- **Firebase** project (Firestore + Storage enabled)
- **Kaleyra** account with webhook access
- **Azure** subscription (for AI/transcription services)

### 1. Clone the Repository

```bash
git clone https://github.com/Thameem-Mul-Ansari/VoiceIQ-AI-Powered-Customer-Support-Intelligence-Platform.git
cd VoiceIQ-AI-Powered-Customer-Support-Intelligence-Platform
```

### 2. Configure Environment Variables

Copy `.env` and fill in your credentials:

```env
# Firebase
VITE_FIREBASE_API_KEY=your_api_key
VITE_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
VITE_FIREBASE_APP_ID=your_app_id

# Azure
AZURE_SPEECH_KEY=your_azure_speech_key
AZURE_SPEECH_REGION=your_region
AZURE_OPENAI_KEY=your_openai_key
AZURE_OPENAI_ENDPOINT=your_endpoint

# Kaleyra
KALEYRA_API_KEY=your_kaleyra_api_key
KALEYRA_WEBHOOK_SECRET=your_webhook_secret
```

### 3. Install Frontend Dependencies

```bash
npm install
```

### 4. Install Backend Dependencies

```bash
pip install -r requirements.txt
```

### 5. Run the Backend

```bash
python app.py
```

The Python server will start and listen for incoming Kaleyra webhook events.

### 6. Run the Frontend

```bash
npm run dev
```

Visit `http://localhost:5173` to access the dashboard.

---

## 🔗 Webhook Setup (Kaleyra)

1. Deploy the Python backend to a publicly accessible URL (or use [ngrok](https://ngrok.com/) for local testing)
2. In your Kaleyra dashboard, configure the webhook endpoint to point to:
   ```
   https://your-backend-url/webhook/call-completed
   ```
3. Kaleyra will POST call metadata and recording URLs to this endpoint upon call completion
4. The backend will automatically download the recording, transcribe it, run AI analysis, and write results to Firebase

---

## 📊 Dashboard Views

| Role | Access |
|---|---|
| **Agent** | Personal call history, own performance scores, coaching tips |
| **Supervisor** | Team overview, individual agent scores, call playback, flagged calls |
| **Admin** | Full platform access, user management, system configuration |

---

## 🤖 AI Analysis Pipeline

Each completed call goes through the following stages:

1. **Download** — Recording retrieved from Kaleyra storage
2. **Transcription** — Audio converted to text via Azure Speech Services
3. **Diarization** — Speaker segments identified (Agent vs. Customer)
4. **AI Evaluation** — LLM agents evaluate the conversation across scoring dimensions:
   - Problem Resolution Rate
   - Communication Clarity
   - Empathy & Tone
   - Script Compliance
   - Customer Sentiment
5. **Score Generation** — Composite performance score calculated
6. **Insights** — Specific strengths and improvement areas surfaced
7. **Storage** — Results written to Firebase for real-time dashboard access

---

## 🚀 Deployment

### Frontend (Firebase Hosting / Vercel)

```bash
npm run build
# Deploy the dist/ folder to Firebase Hosting or Vercel
```

### Backend (Azure App Service / Docker)

```bash
# Build and push Docker image, or deploy app.py directly to Azure App Service
az webapp up --name voiceiq-backend --resource-group your-rg
```

---

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -m 'Add your feature'`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request

---

## 📄 License

This project is open source. See the repository for license details.

---

## 👤 Author

**Thameem Mul Ansari**
[GitHub Profile](https://github.com/Thameem-Mul-Ansari)

---

*VoiceIQ — Turning every customer conversation into a learning opportunity.*
