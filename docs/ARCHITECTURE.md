# 🏛️ DuoCode Unified System Architecture & Database Schema

## 1. Overview

DuoCode unifies habit-tracking, gamification, code scrapbooking, and spaced repetition into a single cohesive platform.

---

## 2. Complete Database Schema (PostgreSQL + pgvector)

```sql
-- 1. Users & Gamification State
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    username VARCHAR(64) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    current_streak_days INT DEFAULT 0,
    longest_streak_days INT DEFAULT 0,
    total_xp INT DEFAULT 0,
    league_tier VARCHAR(32) DEFAULT 'BRONZE', -- BRONZE, SILVER, GOLD, OBSIDIAN, FAANG
    streak_freezes_available INT DEFAULT 2,
    last_active_date DATE DEFAULT CURRENT_DATE,
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- 2. Mascot Mood & Activity Log
CREATE TABLE mascot_logs (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    mascot_mood VARCHAR(32) DEFAULT 'HAPPY', -- HAPPY, NUDGE, PASSIVE_AGGRESSIVE, UNHINGED
    message_dispatched TEXT NOT NULL,
    channel VARCHAR(32) NOT NULL, -- PUSH, DISCORD, TELEGRAM
    dispatched_at TIMESTAMPTZ DEFAULT NOW()
);

-- 3. The Vault: Problems & Categorization
CREATE TABLE vault_problems (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    source_platform VARCHAR(32) DEFAULT 'LEETCODE',
    problem_number INT,
    title TEXT NOT NULL,
    slug VARCHAR(128) NOT NULL,
    difficulty VARCHAR(16) NOT NULL, -- EASY, MEDIUM, HARD
    pattern_tags TEXT[] DEFAULT '{}', -- ['Sliding Window', 'Two Pointers']
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- 4. The Vault: Solutions & Code Snippets
CREATE TABLE vault_solutions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    problem_id UUID REFERENCES vault_problems(id) ON DELETE CASCADE,
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    approach_name VARCHAR(64) NOT NULL, -- 'Optimal: 2 Pointers with hashmap'
    language VARCHAR(32) NOT NULL, -- PYTHON, CPP, RUST, TYPESCRIPT
    code_content TEXT NOT NULL,
    time_complexity VARCHAR(32) NOT NULL, -- 'O(N)'
    space_complexity VARCHAR(32) NOT NULL, -- 'O(1)'
    intuition_notes TEXT,
    visual_diagram_markdown TEXT,
    is_optimal BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- 5. Spaced Repetition (SuperMemo SM-2) Tracker
CREATE TABLE spaced_reviews (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    problem_id UUID REFERENCES vault_problems(id) ON DELETE CASCADE,
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    ease_factor NUMERIC(4, 2) DEFAULT 2.50,
    interval_days INT DEFAULT 1,
    repetition_count INT DEFAULT 0,
    next_review_due TIMESTAMPTZ DEFAULT NOW(),
    last_reviewed_at TIMESTAMPTZ
);
```

---

## 3. The Unified User Journey

1. **Daily Push Reminder:** DuoCode's mascot checks if the user has practiced today. If not, it sends a targeted reminder recommending a problem due in their Spaced Repetition queue.
2. **1-Click Clipper:** The user solves the problem on LeetCode and uses the DuoCode browser extension to clip the solution into **The Vault**.
3. **Automated Streak & XP Reward:**
   - Saving a solution to **The Vault** automatically marks today's streak as completed.
   - Rewards +25 XP / +50 XP and increments league rank.
   - Mascot transitions from `PASSIVE_AGGRESSIVE` to `PROUD`.
4. **Mascot Quick-Quiz Drill:** In spare moments, the user opens the mobile app for a 2-minute flashcard quiz where the mascot tests their recall on previously vaulted solutions.
