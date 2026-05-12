# 🤖 AI Content Pipeline

> Send a topic. Get 3 research-backed scripts. Generate a video. All automated. ₹438/month.

---

## 📌 What This Does

You send a topic to a Telegram bot.  
The system researches the web, generates 3 ready-to-record scripts, and delivers them back — in under 30 seconds.  
Paste one script into NotebookLM and get a full 60-90 second video with voiceover.  
One operator can run 10+ content channels at this speed.

---

## 🎯 The Problem This Solves

Content teams spend hours on research and scripting every day.  
Agencies charge ₹2–5 lakh/month to run 10 channels.  
Most AI content tools are expensive and disconnected.

This pipeline automates the entire research → script → video workflow  
for ₹438/month — the cost of a single VPS.

---

## 🔁 Full Pipeline Architecture

```
Operator (Telegram)
      ↓
  Send topic as message
      ↓
[Telegram Trigger Node]
      ↓
[Extract Topic Node]
  pulls text + chat ID
      ↓
[Web Search Node]
  Serper API → top 5 trending results
      ↓
[Prepare Research Node]
  extracts titles + snippets → clean context string
      ↓
[Basic LLM Chain]
  OpenAI / self-hosted LLM
  prompt: topic + research → 3 scripts, JSON format
      ↓
[Parse Scripts Node]
  splits 3 scripts into individual items
      ↓
[Send to Telegram Node]
  delivers Script 1/3, 2/3, 3/3
  each with: angle, hook, full script
      ↓
Operator picks one script
      ↓
[NotebookLM Video Overview]
  paste script → generate 60-90 sec video
  voiceover + animations + text overlays
      ↓
Ready to post
```

**Extension layer (next iteration):**

```
Video downloaded → Google Drive folder
      ↓
[n8n Google Drive Trigger]
  detects new file
  folder name = channel name
      ↓
[LLM Node]
  generates caption + hashtags from script hook
      ↓
[Meta Graph API]
  posts to correct Instagram account
      ↓
[Telegram Notification]
  "Posted to @channel ✅"
```

---

## 🧩 n8n Workflow — Node Breakdown

| Node | Type | What It Does |
|------|------|--------------|
| Telegram Trigger | Trigger | Listens for messages 24x7 |
| Extract Topic | Set node | Parses topic text + chat ID |
| Web Search | HTTP Request | POST to Serper API with topic |
| Prepare Research | Code node | Extracts top 5 snippets into clean string |
| Basic LLM Chain | LangChain | Sends prompt + research to LLM |
| Parse Scripts | Code node | Splits JSON response into 3 separate items |
| Send to Telegram | Telegram | Delivers scripts one at a time |

Workflow JSON: [`workflow.json`](./workflow.json)

---

## 💸 Cost Breakdown

| Component | Monthly Cost | Notes |
|-----------|-------------|-------|
| n8n self-hosted (Hostinger KVM2) | ₹438/mo | Runs all automation |
| Serper API | ₹0 | Free tier — 2,500 searches/month |
| OpenAI GPT (testing) | ~₹80/mo | Testing only |
| Self-hosted LLM (production) | ₹0 | NVIDIA NIM free endpoint or Gemma |
| NotebookLM video generation | ₹0 | Google product, free |
| Google Drive | ₹0 | 15GB free |
| Meta Graph API | ₹0 | Direct posting, free |
| **TOTAL (production)** | **₹438/mo** | 10 channels · 20 reels/day |

**₹438 ÷ 600 reels/month = ₹0.73 per reel**

---

## ⚙️ How to Set It Up

### Prerequisites
- Self-hosted n8n instance
- Telegram bot (create via @BotFather)
- Serper API key → [serper.dev](https://serper.dev) (free)
- OpenAI API key (or self-hosted LLM)

### Steps

**1. Import the workflow**
- Open n8n → top right menu → Import from file
- Upload `workflow.json`

**2. Set up Telegram credentials**
- Click Telegram Trigger node
- Create new credential → paste your bot token
- Repeat for Send to Telegram node

**3. Add Serper API key**
- Click Web Search node
- Replace `YOUR_SERPER_API_KEY` with your key

**4. Connect LLM**
- Click Basic LLM Chain node
- Add your OpenAI credential
- Or swap for self-hosted LLM via HTTP node

**5. Activate workflow**
- Toggle Activate in top right
- Send any topic to your Telegram bot
- Receive 3 scripts in under 30 seconds

---

## 📈 How to Scale to 10 Channels

- Use `/generate [niche] [topic]` format in Telegram
- Each niche gets its own system prompt (finance, fitness, tech, etc.)
- NotebookLM generates video → save to channel-specific Google Drive folder
- n8n Drive trigger detects folder name = channel name → posts to correct account
- 10 channels × 2 reels/day = 20 automated posts/day from 1 operator

---

## 🔮 What's Next

- [ ] Browser automation for NotebookLM (Playwright / AI agent)
- [ ] Google Drive trigger → auto-post via Meta Graph API
- [ ] Analytics feedback loop (Instagram API → LLM → update prompts)
- [ ] Multi-niche channel management from single Telegram bot
- [ ] Replace OpenAI with fully self-hosted LLM (Gemma / NVIDIA NIM free endpoint)
- [ ] Automatic caption + hashtag generation per niche
- [ ] Weekly performance report delivered via Telegram

---

## 🏗️ Tech Stack

| Layer | Tool | Why |
|-------|------|-----|
| Orchestration | n8n (self-hosted) | Full automation, webhook support |
| Trigger | Telegram Bot API | Operator input, script delivery |
| Research | Serper API | Google search results, free tier |
| Scripting | OpenAI / Gemma | GPT for testing, self-hosted in prod |
| Video | NotebookLM Video Overview | Free, no API needed |
| Storage | Google Drive | Video handoff to n8n trigger |
| Posting | Meta Graph API | Direct Instagram publishing |
| Infrastructure | Hostinger KVM2 VPS | ₹438/month, runs n8n + LLM |

---

## 📁 Repository Structure

```
ai-content-pipeline/
├── README.md          → full documentation
├── workflow.json      → n8n workflow (import directly)
└── /images
    ├── workflow.png   → n8n workflow screenshot
    ├── pipeline.png   → architecture diagram
    └── demo.png       → scripts arriving in Telegram
```

---

## 👤 Built By

**Abhishek Sonawane** — Senior Software Engineer  
I build systems that fix problems nobody else stopped to question.

At my company, I replaced ₹50,000/month of manual ops work  
with a self-hosted AI pipeline running at ₹438/month.  
This is the same thinking applied to content.

→ [LinkedIn](https://www.linkedin.com/in/abhishek-sonawane-3a0387375)  
→ [GitHub](https://github.com/abhishekSonawane97)

---

## ⭐ If This Helped You

Star the repo — it helps others find it.  
Share it with someone building content systems.  
Connect on LinkedIn if you're working on similar problems.

---

*Built in 18 hours. Costs ₹438/month. Runs 24x7.*
