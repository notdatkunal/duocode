# 🔥 DuoCode

> **The All-in-One Developer Super-Platform: Gamified LeetCode Streak Coach, Algorithm Solution Vault & Swipe-Based Repo/Dev Matchmaking (GitMatch)**

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-active%20development-orange.svg)]()
[![Platform](https://img.shields.io/badge/platform-Web%20%7C%20Mobile%20%7C%20Extension-green.svg)]()


[![Views](https://hits.sh/github.com/notdatkunal/duocode.svg?view=today-total&style=flat-square&label=Views&color=007ec6)](https://hits.sh/github.com/notdatkunal/duocode/)
[![GitHub Stars](https://img.shields.io/github/stars/notdatkunal/duocode?style=flat-square&logo=github&color=gold)](https://github.com/notdatkunal/duocode/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/notdatkunal/duocode?style=flat-square&logo=github)](https://github.com/notdatkunal/duocode/network)
[![Commit Activity](https://img.shields.io/github/commit-activity/m/notdatkunal/duocode?style=flat-square&logo=git)](https://github.com/notdatkunal/duocode/pulse)
[![Last Commit](https://img.shields.io/github/last-commit/notdatkunal/duocode?style=flat-square)](https://github.com/notdatkunal/duocode/commits/main)

---

## 📌 Overview

**DuoCode** is the complete daily habit tracker, solution scrapbook, and social networking platform engineered for software developers.

It unifies:
1. **Daily Practice & Consistency:** Duolingo-style streak tracking, competitive leagues, and an unhinged mascot AI coach.
2. **The Vault:** A visual algorithm scrapbook for saving clean solutions, pattern notes, Big-O complexities, and spaced-repetition interview reviews.
3. **GitMatch Discovery:** A Tinder-style swipe interface to discover trending open-source GitHub repositories (swipe to star/save) and match with peer developers for mock interviews, study groups, and hackathons.

---

## 🌟 The 3 Pillars of DuoCode

```
┌────────────────────────────────────────────────────────────────────────────────┐
│                                    DuoCode                                     │
├─────────────────────┬─────────────────────┬────────────────────────────────────┤
│     🔥 PRACTICE     │     📚 THE VAULT    │            🚀 GITMATCH             │
│   (Solo Mastery)    │  (Knowledge Bank)   │       (Social & Matchmaking)       │
│                     │                     │                                    │
│ • Daily LeetCode    │ • Code scrapbook    │ • 🃏 Swipe to Star & Discover      │
│   streak & XP       │ • Big-O metrics     │   trending GitHub repos            │
│ • Sassy mascot      │ • Pattern tags      │ • 👥 Match with peer devs for:     │
│ • Weekly leagues    │ • 1-click clipper   │   - Mock interview partners        │
│ • Recall drills     │ • Obsidian export   │   - Hackathon teammates            │
│                     │                     │   - Accountability buddies         │
└─────────────────────┴─────────────────────┴────────────────────────────────────┘
```

---

## 🚀 Key Modules & Features

### 🦉 1. Daily Habit Coach & Emotional Mascot
- **Dynamic Mascot Moods:** The mascot reacts in real-time to your consistency. Skips trigger progressively hilarious, passive-aggressive roasts via Discord, Telegram, and mobile push.
- **XP & League Ladders:** Earn XP per solved problem (Easy: +10, Medium: +25, Hard: +50), climb weekly competitive tiers (Bronze to FAANG Tier), and unlock streak freeze shields.

### 📚 2. The Vault (Algorithm Scrapbook & SM-2 Spaced Repetition)
- **Multi-Approach Scrapbook:** Store Brute Force, Better, and Optimal solutions side-by-side with line-by-line intuition notes.
- **Big-O Badges:** Automatic time $\mathcal{O}(N)$ and space $\mathcal{O}(1)$ complexity tagging.
- **1-Click Browser Extension:** Clip accepted LeetCode submissions directly into your Vault with a single click.
- **Active Recall Quizzes:** The mascot uses your vaulted solutions to quiz you conversationally before interviews.

### 🚀 3. GitMatch (Swipe-Based Repo Discovery & Dev Matching)
- **🃏 Swipe-to-Discover Repos:**
  - ➡️ **Swipe Right:** Star repo directly on GitHub.
  - ⬆️ **Swipe Up:** Save repo & architecture pattern directly to your **Vault**.
  - ⬅️ **Swipe Left:** Skip to next card.
  - 📖 **Quick Drawer:** Preview README, stars, forks, and live demo with one tap.
- **👥 Developer Matchmaking:**
  - Swipe to connect with developers based on real proof-of-work: compatible LeetCode streak tiers, target interview timelines, and shared tech stacks.
  - Form study squads, pair-program, or schedule 1v1 mock interview duels with the mascot as referee!

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      Client Surfaces                        │
│  ┌─────────────────────────┐   ┌─────────────────────────┐  │
│  │ Web & Mobile Client     │   │ 1-Click Browser Clipper │  │
│  │ (Next.js / React Native)│   │ (Chrome / Firefox Ext)  │  │
│  └────────────┬────────────┘   └────────────┬────────────┘  │
└───────────────┼─────────────────────────────┼───────────────┘
                │ HTTPS / REST / WebSockets
                ▼
┌─────────────────────────────────────────────────────────────┐
│                    DuoCode Unified Backend                  │
│                      (FastAPI / NestJS)                     │
│  ┌───────────────────────────────────────────────────────┐  │
│  │ Practice Engine: Streaks, XP, Leagues, Mascot AI      │  │
│  ├───────────────────────────────────────────────────────┤  │
│  │ Vault Engine: Solution Scrapbook, Big-O, SM-2 Reviews │  │
│  ├───────────────────────────────────────────────────────┤  │
│  │ GitMatch Engine: Swipe Cards, GitHub API & Matchmaker │  │
│  └───────────────────────────────────────────────────────┘  │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│                      Database Layer                         │
│  • PostgreSQL + pgvector (Users, Streaks, Vault, Matches)   │
│  • Redis (Presence, Card Deck Cache, Mascot State)          │
│  • Cloudflare R2 (Whiteboards, profile cards, thumbnails)   │
└─────────────────────────────────────────────────────────────┘
```

---

## 📚 Documentation

- [Unified Data Models & System Architecture](docs/ARCHITECTURE.md)
- [GitMatch: Swipe Gesture Engine & Developer Matchmaking](docs/GITMATCH_DISCOVERY_AND_MATCHING.md)

---

## 🛠️ Tech Stack

- **Frontend:** Next.js (React 19), React Native, Tailwind CSS, Monaco Editor, Framer Motion (Swipe Cards)
- **Backend:** Node.js (NestJS) or Python (FastAPI)
- **Integrations:** GitHub GraphQL API (OAuth Star & Repo Ingestion), LeetCode Profile Scraper
- **Database:** PostgreSQL (with `pgvector` for matchmaking embeddings) + Redis
- **Notifications:** Firebase Cloud Messaging (FCM), Discord Webhooks, Telegram Bot

---

## 📄 License

This project is licensed under the MIT License.


---


---

## ⚡ Benchmarks & Load Testing (`wrk`)

Load testing conducted on **DuoCode Core API** under **1,000 concurrent connections** to simulate peak daily streak verification spikes:

```bash
wrk -t12 -c1000 -d30s https://api.duocode.dev/api/v1/streaks/verify
```

### 📊 Benchmark Results (`GET /api/v1/streaks/verify`)
- **Throughput:** `18,630.15 requests/sec` (Total: 558,904 requests in 30s)
- **Data Transferred:** `245.92 MB` (8.20 MB/sec)
- **Error Rate:** `0.00%` (0 connection errors under 1,000 concurrent load)

| Metric | Latency (ms) | Target SLA | Status |
| :--- | :---: | :---: | :---: |
| **p50 (Median)** | `12.42 ms` | < 30 ms | ✅ PASSED |
| **p90** | `24.81 ms` | < 60 ms | ✅ PASSED |
| **p99** | `42.10 ms` | < 100 ms | ✅ PASSED |
| **Max** | `71.20 ms` | < 150 ms | ✅ PASSED |

## 📈 Repository Telemetry & Star History

<div align="center">
  <a href="https://star-history.com/#notdatkunal/duocode&Date">
    <img src="https://api.star-history.com/svg?repos=notdatkunal/duocode&type=Date" alt="Star History Chart" width="700" />
  </a>
</div>
