# 🔥 DuoCode

> **The All-in-One Gamified LeetCode Consistency Coach & Algorithm Solution Vault**

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-active%20development-orange.svg)]()
[![Platform](https://img.shields.io/badge/platform-Web%20%7C%20Mobile%20%7C%20Extension-green.svg)]()

---

## 📌 Overview

**DuoCode** is the complete daily habit tracker, learning coach, and algorithm solution scrapbook for software engineers.

It combines the **unhinged accountability and gamification of Duolingo** with an **integrated digital code scrapbook (The Vault)**, ensuring you not only stay consistent with daily coding challenges but also permanently retain and master the algorithms you solve.

---

## 🌟 The Unified DuoCode Experience

```
┌────────────────────────────────────────────────────────────────────────┐
│                                DuoCode                                 │
├───────────────────┬───────────────────┬────────────────────────────────┤
│    🔥 STREAKS     │    📚 THE VAULT   │       🧠 RECALL & QUIZ         │
│                   │                   │                                │
│ • Daily quests    │ • Code scrapbook  │ • SM-2 Spaced Repetition       │
│ • Sassy mascot    │ • Big-O metrics   │ • Mascot quick-fire questions  │
│ • League ranks    │ • Pattern tags    │ • Pattern flashcard drills     │
│ • XP rewards      │ • 1-click clipper │ • Weak-spot targeting          │
└───────────────────┴───────────────────┴────────────────────────────────┘
```

---

## 🚀 Core Modules & Features

### 🦉 1. The Daily Habit Coach & Emotional Mascot
- **Dynamic Mascot Moods:** The mascot reacts in real-time to your consistency. Skips result in hilarious, progressively passive-aggressive notifications across Discord, Telegram, and mobile push.
- **XP & Streaks:** Earn XP (Easy: +10, Medium: +25, Hard: +50), climb weekly competitive leagues, and unlock streak freeze shields.

### 📚 2. The Vault (Built-in Code Scrapbook & Solution Keeper)
- **Multi-Approach Scrapbook:** Save your Brute Force, Better, and Optimal solutions side-by-side with line-by-line intuition notes.
- **Big-O Complexity Badges:** Tag time $\mathcal{O}(N)$ and space $\mathcal{O}(1)$ complexities with instant runtime analysis.
- **Pattern Taxonomy:** Organize solutions by fundamental patterns (*Sliding Window, Two Pointers, Monotonic Stack, Backtracking, Tree DP*).
- **1-Click Browser Extension:** Clip LeetCode submissions directly into your DuoCode Vault with one click.

### 🧠 3. Interactive Recall & Spaced Repetition (SM-2)
- **Active Recall Drills:** The mascot uses your vaulted solutions to quiz you conversationally before interviews (*"What was your condition to advance the pointer in Trapping Rain Water?"*).
- **Spaced Repetition Engine:** Automatically schedules review sessions right before memory decay sets in.

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      Client Surfaces                        │
│  ┌─────────────────────────┐   ┌─────────────────────────┐  │
│  │ Web & Mobile App        │   │ 1-Click Browser Clipper │  │
│  │ (Next.js / React Native)│   │ (Chrome / Firefox Ext)  │  │
│  └────────────┬────────────┘   └────────────┬────────────┘  │
└───────────────┼─────────────────────────────┼───────────────┘
                │ HTTPS / REST / WebSockets   │
                ▼                             ▼
┌─────────────────────────────────────────────────────────────┐
│                    DuoCode Unified Backend                  │
│                      (FastAPI / NestJS)                     │
│  ┌───────────────────────────────────────────────────────┐  │
│  │ Habit Engine: Streaks, XP, League Ranks, Mascot AI    │  │
│  ├───────────────────────────────────────────────────────┤  │
│  │ Vault Engine: Solution Scrapbook, Big-O, Pattern Tags │  │
│  ├───────────────────────────────────────────────────────┤  │
│  │ Spaced Repetition: SuperMemo SM-2 Scheduler           │  │
│  └───────────────────────────────────────────────────────┘  │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│                      Database Layer                         │
│  • PostgreSQL + pgvector (Users, Streaks, Vault Solutions)  │
│  • Redis (Presence, Mascot Mood Cache, Rate Limits)         │
│  • Cloudflare R2 (Whiteboard diagrams & illustrations)      │
└─────────────────────────────────────────────────────────────┘
```

---

## 📚 Documentation

- [Unified Data Models & Architecture](docs/ARCHITECTURE.md)

---

## 🛠️ Tech Stack

- **Frontend:** Next.js (React 19), React Native, Tailwind CSS, Monaco Editor, Lottie Mascot Animations
- **Backend:** Node.js (NestJS) or Python (FastAPI)
- **Database:** PostgreSQL (with `pgvector` for semantic solution search) + Redis
- **Browser Extension:** WebExtension Manifest V3
- **Alert Dispatch:** Firebase Cloud Messaging (FCM), Discord Webhooks, Telegram Bot

---

## 📄 License

This project is licensed under the MIT License.
