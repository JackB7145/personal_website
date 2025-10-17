# 🚀 Jack Branston — Personal Website Revamp (Next.js)

A dynamic, API-driven personal website built with **Next.js**, integrating **GitHub**, **LinkedIn**, and **Google Calendar** to create a self-updating portfolio and an intelligent chatbot experience — all without a database.

---

## 🧭 Project Overview

This project rebuilds my personal website into a **live, data-driven portfolio** that updates automatically as my projects and experiences evolve.  
It leverages public APIs and server-side caching for performance and security, all behind a reverse-proxy DNS setup for scalability.

---

## 🧩 Core Features

### **1. Dynamic Projects**

Automatically showcase select repositories from my GitHub profile.

**Implementation:**
- Fetch repositories with a custom flag (e.g., `"showcase:true"`) using the GitHub API.
- Cache results server-side to minimize API calls.
- Rate-limit public access to prevent abuse.
- Each project opens into a modal card displaying:
  - **Project Name**
  - **Description**
  - **Tech Stack** (bubble tags)
  - **Inspiration / Problem Statement**
  - **Additional Initiatives** (e.g., research, deliverables, notes)
  - **Commit History Graph** illustrating project effort

**Result:**  
A live, visually rich portfolio that automatically reflects my latest work.

---

### **2. Chatbot Feature**

A novelty chatbot trained on my resume and background.

**Implementation:**
- Resume and experience data stored as static JSON or Markdown.
- Chat API route uses OpenAI (or a custom FastAPI endpoint) to handle questions.
- Rate-limited (e.g., 5 requests/hour per IP) to prevent spam.

**Example Prompts:**
- “Tell me about Jack’s experience at Scotiabank.”
- “What projects has Jack done using React?”

**Result:**  
An interactive, conversational way to explore my background.

---

### **3. Experience Section**

Syncs professional experience directly from LinkedIn.

**Implementation:**
- Uses LinkedIn API to fetch job titles, companies, and durations.
- Caches results on the server (refreshes daily).
- Renders a clean vertical timeline layout.

**Result:**  
Always up-to-date experience data — identical to my LinkedIn profile.

---

### **4. Landing Page & Intro**

A personalized hero section with live education info.

**Implementation:**
- Hero image, tagline, and short intro paragraph.
- Pulls school, degree, and graduation year via LinkedIn API.
- Optional static JSON fallback for offline rendering.

**Result:**  
A self-updating introduction that evolves with my profile.

---

### **5. Contact & Coffee Chat**

Turns contact requests into scheduled meetings automatically.

**Implementation:**
- Google Calendar API integration.
- Visitor selects available times; event auto-created on both calendars.
- Optional reCAPTCHA or IP rate-limit.

**Result:**  
A “Book a Coffee Chat” experience that connects instantly.

---

## ⚙️ Technical Stack

| Layer | Tech |
|-------|------|
| **Frontend** | Next.js (App Router) |
| **Deployment** | Vercel |
| **Styling** | TailwindCSS / Custom CSS |
| **APIs** | GitHub, LinkedIn, Google Calendar, OpenAI |
| **Data Storage** | None (API + in-memory cache) |
| **Rate Limiting** | `@upstash/ratelimit` or in-memory limiter |
| **Hosting** | `jackbranston.com` via Vercel & reverse proxy DNS |

---

## 🔒 Rate Limiting Rules

| Route | Limit | Description |
|--------|--------|-------------|
| `/api/projects` | 60 req/hour/IP | GitHub project fetch |
| `/api/chat` | 5 req/hour/IP | Chatbot questions |
| `/api/linkedin` | 1 req/day/server | LinkedIn data refresh |

**Implementation Options:**
- [Upstash Rate Limit](https://github.com/upstash/ratelimit)
- Custom in-memory `Map` with timestamps and TTL

---

## 🌐 Infrastructure & DNS

**Migration Plan:**
- Move DNS hosting to **Cloudflare** or **Bunny.net**
- Enable **reverse proxy routing** for scalability:
  - `jackbranston.com` → Vercel (main site)
  - `api.jackbranston.com` → backend/FastAPI
  - `mailgame.jackbranston.com` → side project
  - Future apps → subdomains or reverse-proxied paths

**Benefits:**
- SSL, caching, and DDoS protection
- Easier subdomain/project hosting
- Consistent branding under one domain

---

## 🧱 Security

- API tokens stored securely in Vercel environment variables.
- No secrets or tokens exposed in the frontend.
- CORS locked to `jackbranston.com` and trusted subdomains only.

---

## 🧩 Outcome

A **self-sustaining, intelligent personal website** that:
- Updates automatically from GitHub and LinkedIn  
- Includes a fun, resume-aware chatbot  
- Lets visitors schedule meetings instantly  
- Scales to host future projects under one domain  

---

### 📍 Next Steps

- [ ] Set up Cloudflare DNS + reverse proxy  
- [ ] Initialize Next.js app and route structure  
- [ ] Implement GitHub API integration + caching  
- [ ] Add chatbot API route + OpenAI integration  
- [ ] Connect LinkedIn and Google Calendar APIs  
- [ ] Deploy and test on Vercel  

---

**Author:** [Jack Branston](https://jackbranston.com)  
**License:** MIT
