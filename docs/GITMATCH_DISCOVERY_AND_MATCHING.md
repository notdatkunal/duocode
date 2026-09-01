# 🚀 GitMatch: Swipe-Based Repo Discovery & Developer Matchmaking

## 1. Overview

GitMatch is the discovery and social networking engine integrated directly into **DuoCode**. It provides two swipeable card modes:
1. **Repo Discovery Mode:** Tinder-style discovery for trending, rising, and hidden-gem GitHub open-source projects.
2. **Developer Matchmaking Mode:** Swipe to connect with developers for mock interviews, hackathon teams, and study squads.

---

## 2. Gesture Mapping (Repo Mode)

```
                     ⬆️ SWIPE UP
               Save to Personal Vault
                         │
                         ▲
                         │
      ⬅️ SWIPE LEFT  ─── Card ───►  ➡️ SWIPE RIGHT
       Skip to Next                  Star on GitHub
                         │
                         ▼
                    ⬇️ SWIPE DOWN
                 Expand README Drawer
```

---

## 3. Developer Matchmaking Algorithm

Developer cards are scored and ranked using a multi-factor compatibility vector:

$$\text{MatchScore}(A, B) = w_1 \cdot \text{Sim}_{\text{Stack}}(A, B) + w_2 \cdot \text{Sim}_{\text{LeetCodeStreak}}(A, B) + w_3 \cdot \text{Sim}_{\text{TargetGoal}}(A, B) + w_4 \cdot \text{Sim}_{\text{GitHubStars}}(A, B)$$

| Factor | Weight ($w_i$) | Description |
| :--- | :---: | :--- |
| **Tech Stack Overlap** | 0.35 | Cosine similarity between language/framework tags (e.g. TypeScript, Rust, Python). |
| **Streak & League Tier** | 0.25 | Matching similar consistency levels (e.g. Gold League with Gold League). |
| **Interview Goal & Timeline**| 0.25 | Users targeting FAANG/Startups in the same window (e.g. "Interviews in 3 months"). |
| **Shared Starred Repos** | 0.15 | Jaccard index of mutually starred GitHub repositories. |

---

## 4. GitHub API & Card Deck Caching

- **Card Ingestion:** Background worker continuously pulls trending GitHub repositories via GitHub GraphQL API, enriched with AI summaries, primary language tags, and star velocity.
- **Client Cache:** The mobile and web app pre-fetches a buffer deck of 20 cards into local memory to ensure 60fps buttery-smooth swipe animations without waiting on network requests.
- **GitHub OAuth Action:** Swiping right triggers an asynchronous `PUT /user/starred/{owner}/{repo}` to the user's connected GitHub account.
