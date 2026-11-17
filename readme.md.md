# 🤖 Virtual Chatbot Trigger (Serverless Cloud Alert System)

> A modern, serverless cloud architecture built on **AWS (Amazon Web Services)** that bridges web dashboard triggers to **Discord Webhooks** in real-time, eliminating the need for physical hardware sensors. Developed as part of the SR University Cloud Computing Lab Project.

---

## 🚀 Overview
Traditional IoT alerting systems rely heavily on physical microcontrollers (like ESP32/Arduino) and wired sensors, which can be prone to maintenance overhead and setup friction. This project transitions from physical hardware to a **fully serverless cloud architecture**. 

When a user interacts with the web dashboard (`trigger.html`), an asynchronous HTTP POST request is dispatched to **AWS API Gateway**, which invokes an **AWS Lambda (Python)** function. The function securely formats the payload and pushes real-time notifications to a designated **Discord channel** with precise UTC timestamps.

---

## 🏗️ System Architecture Flow

```text
[ Web Dashboard (trigger.html) ] 
       │
       ▼  (HTTP POST /trigger with CORS)
[ AWS API Gateway (HTTP API v2) ]
       │
       ▼  (JSON Payload Routing)
[ AWS Lambda (Python Logic & urllib Headers) ]
       │
       ▼  (Secure HTTPS POST)
[ Discord Webhook Channel (#general) ]
```

---

## 🛠️ Tech Stack & Services Used

| Component | Technology / AWS Service | Description |
| :--- | :--- | :--- |
| **Frontend** | HTML5, CSS3, JavaScript (Vanilla) | Modern dark-mode control center with live status feedback and session logs. |
| **API Layer** | **AWS API Gateway (HTTP API)** | Routes incoming POST requests and handles CORS preflight configurations. |
| **Compute / Logic** | **AWS Lambda (Python 3.x)** | Serverless execution environment that processes incoming events and crafts Discord payloads. |
| **Notification Channel** | **Discord Webhooks** | Receives real-time alerts and renders formatted chat embeds with timestamps. |
| **Region** | `us-east-1` (N. Virginia) | AWS deployment region. |

---

## 📂 Project Structure

```text
Virtual-Chatbot-Trigger/
│
├── trigger.html          # Frontend dashboard UI with preset triggers and custom message broadcaster
├── lambda_function.py    # Python backend script running inside AWS Lambda
└── README.md             # Project documentation (this file)
```

---

## ⚙️ Setup & Deployment Guide

### 1. Configure the AWS Lambda Function
* Create a new Lambda function in the **`us-east-1`** region using **Python 3.x**.
* Paste your Discord Webhook URL inside the environment or function code securely.
* Ensure your Python script includes standard headers (`User-Agent`) to prevent `403 Forbidden` errors from Discord's API.

### 2. Set Up AWS API Gateway
* Create an **HTTP API**.
* Add a `POST` route mapped to `/trigger`.
* Integrate the route with your Lambda function (`ChatbotTriggerFunction`).
* Enable **CORS** under API Gateway with the following settings:
  * **Access-Control-Allow-Origin:** `*`
  * **Access-Control-Allow-Methods:** `POST`, `OPTIONS`
  * **Access-Control-Allow-Headers:** `Content-Type`

### 3. Connect the Frontend (`trigger.html`)
* Copy your API Gateway **Invoke URL** (e.g., `https://l0wahgs1g3.execute-api.us-east-1.amazonaws.com/trigger`).
* Open `trigger.html` and verify the `API_URL` variable points to your endpoint:
  ```javascript
  const API_URL = "https://l0wahgs1g3.execute-api.us-east-1.amazonaws.com/trigger";
  ```
* Open `trigger.html` in any web browser or via Live Server to start testing!

---

## 💡 Key Features of the Dashboard
* **Preset Virtual Sensors:** One-click simulation buttons for *Front Door Alert*, *Smart Doorbell*, *High Temp Alert*, and *System Diagnostics*.
* **Custom Broadcast Box:** Type any custom message and press Enter to push instant alerts to Discord.
* **Live Latency Tracking:** Measures round-trip response times (`ms`) from browser to cloud.
* **Session Activity Log:** Real-time visual log tracking successful and failed transmissions.

---

## 👥 Team Members (CloudPulse - Batch 67)

* **Nishant Vaibhav** (`2503A520Q7`) — *Frontend Dashboard Developer*
* **Shibu Kumar Singh** (`2503A520R4`) — *Cloud API & Connectivity Lead*
* **Shad Imam** (`2503A520R5`) — *AWS Lambda & Backend Engineer*
* **Md. Raiyaan** (`2503A520R6`) — *Integration & Testing Lead*

---

## 🎓 Academic Review
* **Institution:** SR University — School of Computer Science & AI
* **Course:** AWS Lab / Cloud Computing Product Review