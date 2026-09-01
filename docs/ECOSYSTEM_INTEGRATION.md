# 🔗 DuoCode & AlgoVault Ecosystem Integration Specification

## 1. Unified Architecture & Inter-App Communication

DuoCode and AlgoVault act as two sides of the same coin:
- **DuoCode** handles motivation, daily habit consistency, gamification, and push accountability.
- **AlgoVault** handles long-term memory, structured solution archiving, pattern recognition, and spaced repetition.

---

## 2. Event-Driven Synergy Loop

```
1. Morning: DuoCode Mascot Assigns Quest
   │ (Pulls target problem from AlgoVault Spaced Repetition queue)
   ▼
2. Midday: User Solves on LeetCode & Clips to AlgoVault
   │ (AlgoVault extension saves solution, Big-O, notes)
   ▼
3. Instant Webhook: AlgoVault ──► DuoCode (EVENT: SOLUTION_VAULTED)
   │
   ▼
4. DuoCode Updates:
   • 🔥 Daily Streak Increment (+1 Day)
   • ⭐️ +50 XP Awarded
   • 🦉 Mascot changes mood from Angry ──► Happy
   • 🏆 Leaderboard position updated
   ▼
5. Evening: Mascot Quick-Fire Recall Drill
   │ DuoCode queries AlgoVault: "What was your time complexity on problem #146?"
   ▼
6. User Answers Correctly ──► AlgoVault updates SM-2 Ease Factor (EF')
```

---

## 3. Webhook & API Contract (JSON Schema)

### Event: `algovault.solution.saved` (AlgoVault ──► DuoCode)
```json
{
  "event_id": "evt_9831a98",
  "event_type": "algovault.solution.saved",
  "timestamp": 1756725000,
  "user_id": "usr_kunal_01",
  "payload": {
    "problem": {
      "id": "prob_two_sum",
      "title": "Two Sum",
      "difficulty": "EASY",
      "tags": ["Array", "Hash Table"]
    },
    "solution": {
      "language": "PYTHON",
      "time_complexity": "O(N)",
      "space_complexity": "O(N)",
      "is_optimal": true
    }
  }
}
```

### Response from DuoCode:
```json
{
  "status": "STREAK_SECURED",
  "current_streak_days": 14,
  "xp_awarded": 25,
  "mascot_state": {
    "mood": "PROUD",
    "dialogue": "Streak protected! 14 days and counting. Don't ruin it tomorrow!"
  }
}
```

---

## 4. Shared Data Sync & Single Sign-On (SSO)

- **Auth Layer:** Unified OAuth2 / NextAuth provider across `duocode.app` and `algovault.app`.
- **Shared API Token:** Cross-app bearer token enables DuoCode to query `GET /api/v1/vault/due-reviews` and `GET /api/v1/vault/solutions/{problem_id}`.
