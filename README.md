# 🤖 AI Customer Support Automation (n8n + Gemini + Gmail + Sheets)

An end-to-end AI-powered customer support system built using n8n workflows, Google Gemini AI, Gmail API, and Google Sheets. It automatically classifies incoming queries, generates smart replies, logs data, and sends category-based emails.

---

## 🚀 Features

- 🧠 AI-powered response generation (Google Gemini)
- 🏷️ Automatic query classification (Sales / Support / Spam / Complaint / Other)
- 📩 Auto email replies via Gmail API
- 📊 Logs all interactions in Google Sheets
- 🔀 Smart routing using Switch logic in n8n
- 🌐 Webhook-based API for frontend integration
- ⚡ Real-time processing
- 🧾 Structured JSON AI output

---

## 🏗️ System Architecture

```
Frontend Form
      ↓
n8n Webhook (/customer-support)
      ↓
Validation (IF node)
      ↓
Google Gemini AI (response + category)
      ↓
Google Sheets (logging)
      ↓
Switch (category routing)
      ↓
Gmail (auto email response)
      ↓
Webhook Response (success/error)
```

---

## 📦 Tech Stack

| Tool | Purpose |
|------|---------|
| n8n | Automation platform |
| Google Gemini API | LLM / AI responses |
| Gmail API | Email automation |
| Google Sheets API | Database logging |
| HTML / JavaScript | Frontend form |
| Webhooks | API communication |

---

## ⚙️ Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/ai-customer-support-automation.git
cd ai-customer-support-automation
```

### 2. Import n8n Workflow

1. Open your n8n dashboard
2. Click **Workflows → Import**
3. Upload `workflow.json`
4. Save the workflow

### 3. Configure Credentials in n8n

#### 🔑 Google Gemini API
- Go to **Credentials → Add Credential**
- Select **Gemini / PaLM API**
- Paste your API key

#### 📧 Gmail API
- Enable Gmail OAuth2 in Google Cloud Console
- Add credentials in n8n
- Connect your Gmail account

#### 📊 Google Sheets API
- Enable Google Sheets API
- Connect your Google account
- Add spreadsheet ID in node config

### 4. Set Webhook URL

In your Webhook node:
- Method: `POST`
- Path: `customer-support`

Your production URL:

```
https://your-n8n-domain/webhook/customer-support
```

### 5. Frontend Setup (Optional)

Inside `/frontend/script.js`:

```javascript
fetch("https://your-n8n-domain/webhook/customer-support", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    name: "John",
    email: "john@example.com",
    message: "I need help with my order"
  })
});
```

---

## 🧪 Input Format (Webhook Request)

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "message": "I need help with my order"
}
```

---

## 📤 Output Response

### ✅ Success

```json
{
  "status": "success",
  "message": "Request processed successfully",
  "timestamp": "2026-05-31T10:00:00Z"
}
```

### ❌ Error

```json
{
  "status": "error",
  "message": "Field value is required"
}
```

---

## 🧠 AI Behavior

The system uses Gemini AI to:

- Generate professional email replies
- Classify user intent into:
  - `Sales`
  - `Support`
  - `Complaint`
  - `Spam`
  - `Other`

Output is strictly returned in JSON format.

---

## 📊 Google Sheets Logging

Each request is stored with:

| Field | Description |
|-------|-------------|
| Timestamp | Time of request |
| Name | Customer name |
| Email | Customer email |
| Message | Original query |
| AI Response | Generated reply |
| Category | Classified intent |

---

## 🔐 Security Notes

- Keep webhook URL private in production
- Add validation for request fields
- Enable **"Continue On Fail"** in n8n nodes
- Add rate limiting if exposing publicly

---

## 📈 Future Improvements

- [ ] JWT authentication for API security
- [ ] Rate limiting per IP/user
- [ ] Retry system for failed emails
- [ ] Dashboard for analytics
- [ ] Slack / WhatsApp integration
- [ ] Database migration (PostgreSQL instead of Sheets)

---

## 👨‍💻 Author

**Shashwat Singh** — AI + Automation + Backend Enthusiast

---

## ⚡ Summary

This project demonstrates:

- AI integration in real workflows
- Production-level automation design
- API-based architecture using webhooks
- Real-world SaaS-like backend flow