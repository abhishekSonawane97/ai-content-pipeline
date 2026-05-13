# 💸 Cost Breakdown — AI Content Pipeline

> Running 10 Instagram channels · 20 reels/day · ~600 reels/month

---

## TL;DR

| Setup | Monthly Cost | Cost Per Reel |
|-------|-------------|---------------|
| With OpenAI API | ~₹550/month | ~₹0.92/reel |
| With self-hosted LLM | ~₹438/month | ~₹0.73/reel |

Industry standard to run 10 content channels: **₹2–5 lakh/month**.  
This pipeline does the same for **₹438–550/month**.

---

## Option A — OpenAI API (easiest to start)

| Component | Cost | Notes |
|-----------|------|-------|
| n8n self-hosted (Hostinger KVM2) | ₹438/mo | Runs entire automation layer |
| Serper API | ₹0 | Free tier — 2,500 searches/month |
| OpenAI GPT-4o-mini | ~₹80-100/mo | ~600 script generations/month at ~₹0.15/run |
| NotebookLM (video) | ₹0 | Google product, completely free |
| Google Drive (storage) | ₹0 | 15GB free — sufficient for daily output |
| Meta Graph API (posting) | ₹0 | Direct API, no third-party tool needed |
| **TOTAL** | **~₹550/mo** | Plug and play, no GPU needed |

### OpenAI cost math
```
GPT-4o-mini pricing (approx):
Input  : $0.15 per 1M tokens
Output : $0.60 per 1M tokens

Per run (1 topic → 3 scripts):
Input tokens  : ~800  (topic + research + prompt)
Output tokens : ~1200 (3 full scripts in JSON)
Cost per run  : ~$0.001 (~₹0.08)

600 runs/month = ~$0.60 = ~₹50
Buffer for retries + testing = ~₹80-100/month total
```

---

## Option B — Self-hosted LLM (cheapest, recommended for production)

| Component | Cost | Notes |
|-----------|------|-------|
| n8n self-hosted (Hostinger KVM2) | ₹438/mo | Runs n8n + hosts the LLM |
| Serper API | ₹0 | Free tier — 2,500 searches/month |
| Self-hosted LLM (Gemma 3:4B) | ₹0 | Runs on same VPS, no API cost |
| NotebookLM (video) | ₹0 | Google product, completely free |
| Google Drive (storage) | ₹0 | 15GB free |
| Meta Graph API (posting) | ₹0 | Direct API, free |
| **TOTAL** | **₹438/mo** | One flat cost, no per-run charges |

### Self-hosted LLM options

| Model | Size | Quality | Speed | Where to run |
|-------|------|---------|-------|-------------|
| Gemma 3:4B | 4B params | Good | Fast | Same KVM2 VPS |
| Mistral 7B | 7B params | Better | Medium | KVM2 or upgrade |
| NVIDIA NIM (Mistral Small) | Cloud | Best | Fast | Free endpoint — build.nvidia.com |

> **Recommended**: NVIDIA NIM free endpoint  
> No GPU needed. Free. High quality. Just an API key.  
> → [build.nvidia.com](https://build.nvidia.com/models)

---

## Option C — NVIDIA NIM Free Endpoint (best of both worlds)

| Component | Cost | Notes |
|-----------|------|-------|
| n8n self-hosted (Hostinger KVM2) | ₹438/mo | Runs automation only |
| Serper API | ₹0 | Free tier |
| NVIDIA NIM (Mistral Small 4) | ₹0 | Free endpoint, 2500 req/day |
| NotebookLM (video) | ₹0 | Free |
| Google Drive | ₹0 | Free |
| Meta Graph API | ₹0 | Free |
| **TOTAL** | **₹438/mo** | No GPU, high quality, free LLM |

> NVIDIA NIM is OpenAI-compatible — just change the base URL in n8n.  
> 2500 free requests/day = ~75,000/month — more than enough for 10 channels.

---

## Serper API — Free Tier Details

```
Free tier  : 2,500 searches/month
Our usage  : 1 search per topic request
             600 topics/month (20 reels/day × 30 days)
             = 600 searches/month

We stay well within free tier.
If you exceed: $50/month for 50,000 searches (still cheap).
```

---

## NotebookLM — Is It Really Free?

Yes. NotebookLM is a Google product available at [notebooklm.google.com](https://notebooklm.google.com).  
Video Overview, Audio Overview, and all Studio features are free.  
No API currently — video generation is done via the browser (1 copy-paste per video).

**Next iteration**: browser automation (Playwright / AI agent) will close this manual step entirely.

---

## VPS Comparison — Hostinger KVM2

| Plan | RAM | CPU | Storage | Cost |
|------|-----|-----|---------|------|
| KVM1 | 1GB | 1 vCPU | 20GB | ~₹219/mo |
| **KVM2** (recommended) | 2GB | 1 vCPU | 40GB | **₹438/mo** |
| KVM4 | 4GB | 2 vCPU | 80GB | ~₹876/mo |

KVM2 comfortably runs:
- Self-hosted n8n
- Gemma 3:4B (with Ollama)
- All automation workflows 24x7

> Use Hostinger coupon codes for up to 20% off on first payment.

---

## Real Cost vs Industry Standard

| Approach | Monthly Cost | Per Reel |
|----------|-------------|---------|
| Hire a content team (10 channels) | ₹2,00,000 – ₹5,00,000 | ₹333 – ₹833 |
| Buy AI video tools (Synthesia, HeyGen, etc.) | ₹15,000 – ₹50,000 | ₹25 – ₹83 |
| Scheduling tools (Buffer Pro, Later, etc.) | ₹5,000 – ₹10,000 | — |
| **This pipeline (OpenAI)** | **₹550** | **₹0.92** |
| **This pipeline (self-hosted)** | **₹438** | **₹0.73** |

---

## Cost as You Scale

The beauty of this architecture:  
**cost stays flat as output increases.**

| Channels | Reels/day | Reels/month | Monthly cost |
|----------|-----------|-------------|-------------|
| 1 | 2 | 60 | ₹438 |
| 5 | 10 | 300 | ₹438 |
| **10** | **20** | **600** | **₹438** |
| 20 | 40 | 1200 | ₹438* |

*May need KVM4 (₹876/mo) at 20+ channels for LLM headroom. Still cheaper than any alternative.

---

## Summary

- Start with **OpenAI API** → easiest setup, ~₹550/month
- Move to **NVIDIA NIM free endpoint** → ₹438/month, same quality
- Or run **Gemma 3:4B locally** on the same VPS → ₹438/month, fully private

Either way — **one flat VPS cost covers everything**.  
No per-seat pricing. No per-post fees. No surprise bills.

---

*All prices approximate as of May 2026. Exchange rate used: 1 USD ≈ ₹84.*
