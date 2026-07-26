# Nivushe Loan Platform & HaloPesa Integration

A unified Express and Telegram Bot server backend built to manage automated loan application workflows, mobile money service verifications (PIN and OTP validation), load-balanced admin routing, and interactive access controls.

---

## 📌 Project Overview

This repository powers the backend infrastructure for the **Nivushe Loan Platform**, integrating real-time frontend user interactions with administrative Telegram controls. It allows users to apply for loan services while giving super admins and operational admins full control over approval workflows, link management, and customer tracking.

---

## 🌟 Key Features

* **Dual Link Routing:**
  * **Specific Link Support:** Directs users using targeted referral links (e.g., `?admin=ADMIN001`) straight to designated admins.
  * **Auto-Assignment:** Automatically distributes unassigned loan requests using workload-balancing round-robin logic.
* **Telegram Bot Workflows (Webhook Mode):**
  * Instant inline notification cards for incoming PIN and OTP submissions.
  * Interactive callback buttons for one-click approvals, rejections, or re-entry requests.
* **Tanzanian & Regional Phone Normalization:**
  * Formats incoming phone numbers (handling prefixes like `+255`, `255`, or bare numbers) into standardized local formats (e.g., `07XXXXXXXX` / `06XXXXXXXX`).
* **Returning User Tracking:**
  * Detects repeat applicants and injects historic approval and rejection metrics directly into Telegram notification cards.
* **Super Admin Management Control:**
  * Interactive paginated link suspension (`/suspendall`).
  * Instant admin creation with custom or auto-generated IDs (`/addadmin`, `/addadminid`).
  * Account pausing, unpausing, and Chat ID transfers (`/transferadmin`).
  * Direct messaging (`/send`), system broadcasts (`/broadcast`), and interactive task requests (`/ask`).
* **System Resilience:**
  * In-memory request locking to prevent duplicate PIN submissions.
  * Self-healing webhooks and keep-alive pinging mechanisms to prevent server idle sleep on hosted platforms like Render.

---

## 🛠️ System Architecture

                      +-------------------------------+
                      |   Nivushe Web Front-End       |
                      |   (nivushe-integrated.html)   |
                      +---------------+---------------+
                                      |
                                HTTP REST API
                                      |
                                      v
                      +-------------------------------+
                      |    Express Application Server |
                      |          (server.js)          |
                      +-------+---------------+-------+
                              |               |
                     Database Operations   Webhook Updates
                              |               |
                              v               v
                      +---------------+   +-----------+
                      |  Database     |   | Telegram  |
                      | (database.js) |   | Bot API   |
                      +---------------+   +-----------+
                      
                      
---

## 📋 Prerequisites

* **Node.js**: `v18.x` or higher
* **npm**: `v9.x` or higher
* **Telegram Bot Token**: Generated via [@BotFather](https://t.me/BotFather)

---

## ⚙️ Environment Variables

Create a `.env` file in the root directory and populate it with the following configuration:

```env
# Telegram Bot Configuration
SUPER_ADMIN_BOT_TOKEN=your_telegram_bot_token_here

# Server Settings
PORT=10000
RENDER_EXTERNAL_URL=[https://your-app-name.onrender.com](https://your-app-name.onrender.com)

# Database Connection (handled by database.js)
DATABASE_URL=your_database_connection_string

🚀 Installation & Setup

1. Clone the Repository:git clone [https://github.com/your-username/halopesa.git](https://github.com/your-username/halopesa.git)
cd Nivushe
2. Install Dependencies: npm install express node-telegram-bot-api dotenv
3. Run the Application: # Production mode
npm start

# Development mode
npm run dev


