# 🏛️ DuoCode Unified System Architecture & Database Schema

## 1. Overview

DuoCode unifies habit-tracking, gamification, code scrapbooking (The Vault), and swipe-based discovery/matchmaking (GitMatch) into a single cohesive platform.

---

## 2. Complete Database Schema (PostgreSQL + pgvector)

```sql
-- 1. Users & Gamification State
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    username VARCHAR(64) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    github_username VARCHAR(64),
    github_access_token_enc TEXT,
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

-- 6. GitMatch: Discovery Deck Repositories
CREATE TABLE gitmatch_repos (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    github_repo_id BIGINT UNIQUE NOT NULL,
    repo_name VARCHAR(128) NOT NULL,
    owner VARCHAR(128) NOT NULL,
    description TEXT,
    stars_count INT DEFAULT 0,
    forks_count INT DEFAULT 0,
    language VARCHAR(64),
    topics TEXT[] DEFAULT '{}',
    readme_snippet TEXT,
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- 7. GitMatch: User Swipes & Developer Matches
CREATE TABLE user_swipes (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    target_type VARCHAR(16) NOT NULL, -- 'REPO' OR 'DEVELOPER'
    target_id UUID NOT NULL,
    swipe_action VARCHAR(16) NOT NULL, -- 'STAR', 'VAULT', 'SKIP', 'LIKE_DEV', 'PASS_DEV'
    created_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE dev_matches (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_a UUID REFERENCES users(id) ON DELETE CASCADE,
    user_b UUID REFERENCES users(id) ON DELETE CASCADE,
    match_status VARCHAR(16) DEFAULT 'MUTUAL_MATCH',
    created_at TIMESTAMPTZ DEFAULT NOW(),
    UNIQUE(user_a, user_b)
);
```

---

## 3. The Unified User Experience Loop

```
┌─────────────────────────────────────────────────────────────┐
│ 1. Practice & Streaks:                                      │
│    • Complete daily challenge & protect streak              │
│    • Climb weekly leagues & earn XP                         │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. The Vault:                                               │
│    • Save solutions, Big-O metrics & whiteboard notes       │
│    • SM-2 spaced repetition active recall quizzes           │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. GitMatch Discovery:                                      │
│    • Swipe right on trending GitHub repos to star them      │
│    • Swipe up to save best algorithms directly to Vault     │
│    • Match with peer devs for 1v1 mock interview battles    │
└─────────────────────────────────────────────────────────────┘
```
