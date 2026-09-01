# 🔥 DuoCode

> **Duolingo for LeetCode: Gamified Consistency, Daily Streaks, and an Unhinged Mascot Coach**

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-active%20development-orange.svg)]()
[![Ecosystem](https://img.shields.io/badge/ecosystem-AlgoVault%20Integrated-purple.svg)](https://github.com/notdatkunal/algovault)

---

## 📌 Overview

**DuoCode** is a gamified habit-building platform that forces software engineers to stay consistent with Data Structures & Algorithms. 

Featuring an **emotionally volatile mascot** (inspired by Duolingo's owl), DuoCode tracks your daily LeetCode activity, protects your streaks, awards XP, and delivers progressively unhinged, passive-aggressive reminders if you dare skip your daily problem.

DuoCode natively connects with **[AlgoVault](https://github.com/notdatkunal/algovault)** to turn your saved solutions into daily interactive quizzes and spaced-repetition interview drills.

---

## 🚀 Key Features

### 🦉 1. The Emotional Mascot & Mood States
- **Day 0 (Streak Active):** Glowing, happy mascot celebrating your achievements (*"You're a DP wizard! Keep it going!"*).
- **Day 1 Inactive (Friendly Nudge):** Mild reminder notifications (*"Hey! Two Sum misses you today."*).
- **Day 2 Inactive (Passive-Aggressive):** Sarcastic pings (*"I see you have time for 4 hours of YouTube Shorts but not 1 Sliding Window problem..."*).
- **Day 3+ Inactive (Unhinged Mode):** Emergency alerts, browser wallpaper takeovers, and roasts dispatched to your Discord or Telegram.

### 🔥 2. Gamification & Streak Mechanics
- **Streak Counters & Freezes:** Earn or purchase "Streak Freezes" using accumulated XP to save your streak during emergencies.
- **XP Progression & Leagues:** Tiered competitive leagues (Bronze, Silver, Gold, Obsidian, FAANG Tier) with weekly leaderboards.
- **XP Rewards:** Easy (+10 XP), Medium (+25 XP), Hard (+50 XP), Speed Bonus (+15 XP).

### 🔗 3. AlgoVault Ecosystem Integration
- **Automated Streak Verification:** Solving a question and capturing it in AlgoVault instantly triggers a webhook that secures your DuoCode streak.
- **Mascot Recall Drills:** The mascot pulls past solutions directly from your AlgoVault scrapbook and tests your memory (*"What was your base case for this problem 5 days ago?"*).
- **Weak-Spot Targeting:** If AlgoVault detects you are failing Tree problems in spaced repetition, DuoCode assigns Tree problems as your priority daily quest.

---

## 🏗️ Ecosystem Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      The Coder Ecosystem                    │
└──────────────────────────────┬──────────────────────────────┘
                               │
            ┌──────────────────┴──────────────────┐
            ▼                                     ▼
┌──────────────────────────────┐       ┌──────────────────────────────┐
│           DuoCode            │       │          AlgoVault           │
│   (Habit & Gamification)     │       │     (Memory & Knowledge)     │
│                              │       │                              │
│ • Daily Streak Tracker       │◄─────►│ • Solution Scrapbook         │
│ • Sassy Mascot AI Coach      │ Event │ • Pattern Taxonomy           │
│ • Discord / Push Alerts      │  Bus  │ • Spaced Repetition (SM-2)   │
│ • Daily Quest Generation     │       │ • 1-Click Extension Import   │
└──────────────────────────────┘       └──────────────────────────────┘
```

---

## 📚 Documentation

- [DuoCode x AlgoVault Ecosystem Specification](docs/ECOSYSTEM_INTEGRATION.md)

---

## 🛠️ Tech Stack

- **Frontend:** React Native (iOS/Android) & Next.js Web App with Lottie Mascot Animations
- **Backend:** Node.js (NestJS) / Python (FastAPI)
- **LeetCode Sync:** GraphQL LeetCode Profile Scraper & Webhook Listener
- **Notification Channels:** FCM Push Notifications, Discord Webhooks, Telegram Bot

---

## 📄 License

This project is licensed under the MIT License.
