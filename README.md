# 🎙️ KVA — Kaspa Voice Amplifier

**Open-source tweet gatekeeper & amplifier for the Kaspa community.**

KVA is a lightweight, transparent system that:

- fetches Kaspa-related tweets using the X API  
- evaluates them with an AI community-manager persona  
- prepares quote tweets (QTs) for human review and approval  

It does **not** rewrite other people’s content.  
It does **not** impersonate anyone.  
It does **not** generate hype.  
It simply amplifies strong community voices using clear rules.

Built with **Next.js, Supabase, Vercel, and OpenAI**.

---

## 🚀 Features

### Automated tweet collection
- Runs on a schedule (default: once per hour)
- Queries the X API for Kaspa-related tweets
- Stores raw tweets in Supabase

### AI gatekeeper evaluation
A strict “Kaspa Community Manager” system prompt determines whether a tweet is:

- **Approved** — high-signal and relevant  
- **Rejected** — drama, hype, off-topic, L2 shilling, etc.  

Approved tweets receive a **short QT suggestion (max ~20 words).**

### Human-in-the-loop workflow
The UI allows you to:

- view all fetched tweets  
- see pass/fail filter results  
- review the proposed QT  
- edit the QT  
- **Post** manually  
- **Dismiss** unwanted tweets  

Optional:
- auto-post mode  
- “re-check edited text with LLM”  

---

## 🧱 Tech Stack

| Component      | Technology              |
|----------------|--------------------------|
| Runtime        | Node.js + TypeScript     |
| Framework      | Next.js 14 (App Router)  |
| Database       | Supabase (Postgres)      |
| Hosting        | Vercel (with Cron)       |
| LLM            | OpenAI API               |
| X Integration  | X (Twitter) API          |
| Auth (optional)| Supabase Auth            |

---

## 📁 Repository Structure

```txt
KVA/
├─ src/
│  ├─ app/              # Next.js pages + routes
│  ├─ api/              # Backend routes (ingest, evaluate, publish)
│  ├─ components/       # Admin UI components
│  ├─ lib/              # Utilities, clients, helpers
│  └─ prompts/          # System prompt for the CM persona
│
├─ supabase/
│  └─ migrations/       # SQL schema for DB tables
│
├─ lists/
│  ├─ blacklist.json    # Accounts to ignore
│  ├─ trusted.json      # Known high-quality accounts
│  └─ filters.json      # Keyword / engagement filters
│
├─ .env.example         # Example environment variables
├─ README.md
└─ LICENSE
```

---

# 🔧 Setup Guide

## 1. Clone the Repository

```bash
git clone https://github.com/Seb287/KVA.git
cd KVA
```

---

# 🐘 Supabase Setup

## 1. Create a new Supabase project

Create a project at:
[https://app.supabase.com](https://app.supabase.com)

## 2. Link project & push migrations

```bash
supabase link
supabase db push
```

This creates the following tables:

* `tweets`
* `evaluations`
* `suggestions`
* `settings`
* `accounts` (optional — only if you enable auth)

## 3. Add Supabase environment variables

In **Vercel → Project → Settings → Environment Variables**, add:

```
SUPABASE_URL=
SUPABASE_SERVICE_ROLE_KEY=
SUPABASE_ANON_KEY=
```

---

# 🛰️ Vercel Setup

## 1. Import the GitHub repo

Import from: [https://vercel.com/new](https://vercel.com/new)

## 2. Add environment variables

Add:

```
OPENAI_API_KEY=
X_API_KEY=
X_API_SECRET=
X_ACCESS_TOKEN=
X_ACCESS_SECRET=
SUPABASE_URL=
SUPABASE_SERVICE_ROLE_KEY=
SUPABASE_ANON_KEY=
```

## 3. Add a cron job (hourly recommended)

In **Vercel → Settings → Cron Jobs**:

```
/api/ingest 0 * * * *
```

This runs the tweet ingestion once per hour.

You can safely change this to:

* every 15 minutes: `*/15 * * * *`
* every 4 hours: `0 */4 * * *`

---

# 🧠 LLM Prompt Location

The Community Manager system prompt is stored in:

```
/src/prompts/cm_system_prompt.txt
```

---


# 🖥️ Admin Interface (Human Oversight)

The admin UI includes:

* a list of all fetched tweets
* whether they passed the filter
* the proposed QT text
* an editable text box
* a button to **Post**
* a button to **Dismiss**

Optional:

* auto-post toggle
* “re-check edited text with LLM” option

---

# 🧪 Local Development

Install dependencies:

```bash
npm install
```

Run the dev server:

```bash
npm run dev
```

Start a local Supabase instance:

```bash
supabase start
```

---

# 🌐 Horizon-Set Ready (Decentralized + Open Infrastructure)

KVA is intentionally designed to be:

* **infrastructure-agnostic**
* **portable**
* **fully open-source**
* **future-proof and self-hostable**

This means the project can be deployed on:

* Vercel
* Supabase
* Fly.io
* Render
* Bare-metal Linux servers
* Docker / Kubernetes
* Decentralized hosting stacks (Horizon, DegenBox-style clusters, etc.)
* Community-run infrastructures

The architecture avoids vendor lock-in by using:

* pure PostgreSQL (no vendor-specific extensions)
* stateless serverless functions
* no proprietary cloud features
* portable `.env` configuration
* open schema and open prompt rules

KVA is meant to be *owned by the community* — anyone can fork, run, maintain, or evolve it.

---

# 🗺️ Roadmap (V1 Only)

**V1 (MVP)**

* Hourly ingest from X
* Gatekeeper evaluation via LLM
* Admin UI for approval/edit/post
* Supabase storage
* Configurable filters
* Open-source release

---

# 📄 License

MIT License — free to use, modify, redistribute, and self-host.

---

# 🤝 Contributing

Pull requests are welcome.

You can help with:

* bugs
* new features
* improvements to CM rules
* performance fixes

All contributions should maintain:

* transparency
* decentralization
* community autonomy



