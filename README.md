# Solo 🍽️
### *The intelligent food companion for people living alone.*

> Built on [Swiggy Builders Club](https://mcp.swiggy.com/builders/) — Food · Instamart · Dineout MCP APIs

---

## The Problem

50 million Indians live alone. Students, young professionals, people between cities.

Every month, the same story:
- Order impulsively at 11pm on a rainy Tuesday
- Get a wrong item, don't bother fighting for the refund
- Check your bank statement and wonder where ₹7,000 went
- Spend 20 minutes choosing between 200 restaurants and order the same thing anyway

Nobody built anything for this person. So we did.

---

## What Solo Does

**One screen. Calm. No noise.**

| Feature | What it actually does |
|---|---|
| 💸 **Spend Intelligence** | Maps every rupee — by day, time, weather, mood |
| 🧠 **Trigger Detection** | Learns *when* you impulse order. Nudges you before you do. |
| ⚠️ **Anomaly Alerts** | Wrong item? Late delivery? Auto-drafts your refund claim. |
| ✦ **One Perfect Pick** | Not 200 options. One recommendation. Based on your taste, budget, and history. |
| 📊 **Weekly Story** | A visual digest of your food week. Like Spotify Wrapped, every Sunday. |
| 🤝 **Full Swiggy Coverage** | Food + Instamart + Dineout — all tracked in one place. |

---

## Demo

🔗 **[Live Demo →](https://aquamarine-chebakia-1c8304.netlify.app/)**

<img width="323" height="647" alt="Screenshot 2026-04-28 at 2 42 20 PM" src="https://github.com/user-attachments/assets/9ec8e5ee-1d66-4c1f-8b7c-8935893b3331" />


---

## How It Works

```
User connects Swiggy account via OAuth
        ↓
Solo pulls full order history via MCP APIs
        ↓
Spending + trigger patterns computed on first load
        ↓
Dashboard renders — one calm screen
        ↓
Background cron watches for new orders in real time
        ↓
WhatsApp nudge fires if impulse pattern detected
        ↓
Weekly digest auto-generated every Sunday
```

---

## Architecture

```
┌─────────────────────────────────────────────────┐
│                  USER LAYER                      │
│        React Web App · WhatsApp Bot              │
│             Weekly Email Digest                  │
└──────────────────────┬──────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────┐
│             INTELLIGENCE LAYER                   │
│   SpendingEngine · TriggerDetector               │
│   RecommendationEngine · AnomalyDetector         │
└──────────────────────┬──────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────┐
│                DATA LAYER                        │
│  Swiggy Food MCP · Instamart MCP · Dineout MCP  │
│        PostgreSQL · Redis Cache                  │
└──────────────────────┬──────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────┐
│             EXTERNAL SIGNALS                     │
│     Weather API · Calendar · UPI SMS Parser      │
└─────────────────────────────────────────────────┘
```

---

## Tech Stack

| Layer | Tech |
|---|---|
| Frontend | React, TailwindCSS |
| Backend | Node.js + FastAPI |
| Database | PostgreSQL + Redis |
| Queue | BullMQ |
| Notifications | Twilio (WhatsApp) + Resend (Email) |
| Auth | OAuth 2.0 via Swiggy MCP |
| APIs | Swiggy Food, Instamart, Dineout MCP |

---

## Core Modules

### `SpendingEngine`
Aggregates order history into actionable financial intelligence.
```js
aggregateByMonth(orders)         → MonthlyReport
detectTopRestaurants(orders)     → RestaurantRank[]
findImpulseTriggers(orders)      → TriggerProfile
projectMonthEnd(spend, daysLeft) → Projection
```

### `AnomalyDetector`
Finds wrong orders, price hikes, refund opportunities.
```js
detectWrongItems(order)          → AnomalyReport
trackPriceDrift(restaurant)      → PriceChange[]
checkRefundEligibility(order)    → RefundClaim
```

### `RecommendationEngine`
Serves one perfect suggestion based on full user context.
```js
buildTasteProfile(orders)        → TasteProfile
getContextualSuggestion(profile) → Suggestion
avoidFatigue(recentOrders)       → FinalSuggestion
```

### `NudgeSystem`
Proactive WhatsApp alerts before bad decisions happen.
```js
detectImpulseSignal(time, profile) → boolean
sendWhatsAppNudge(userId, message) → DeliveryStatus
generateWeeklyDigest(userId)       → DigestEmail
```

---

## Database Schema

```sql
users         (id, phone, email, swiggy_token, budget, created_at)
orders        (id, user_id, restaurant, items[], total, ordered_at, issues[])
menu_snapshots(id, restaurant_id, item_id, price, captured_at)
nudges        (id, user_id, type, message, sent_at, opened)
taste_profiles(id, user_id, data JSONB, updated_at)
```

---

## Roadmap

- [x] Concept & system design
- [x] Demo UI
- [ ] Swiggy MCP API integration
- [ ] SpendingEngine v1
- [ ] Dashboard MVP
- [ ] WhatsApp nudge system
- [ ] AnomalyDetector + refund flow
- [ ] RecommendationEngine
- [ ] Weekly digest email
- [ ] Public beta

---

## Why This Exists

> *"Living alone and couldn't figure out where my money was going every month. Swiggy knew — but it wasn't telling me. So I built Solo to tell me."*

This is not a hackathon project. It's a real problem, lived daily by millions of people who deserve better tooling around the way they eat.

---

## Built With

<img src="https://img.shields.io/badge/Powered%20by-Swiggy%20MCP-FF5B14?style=for-the-badge" />
<img src="https://img.shields.io/badge/Stack-React%20%2B%20Node.js-000000?style=for-the-badge" />
<img src="https://img.shields.io/badge/Status-In%20Development-yellow?style=for-the-badge" />

---

## Contact

Built by **[Rahul Krishna]** · [LinkedIn](https://www.linkedin.com/in/rahul-krishna-709a12144/?skipRedirect=true)

---

*Solo — eat smarter, live better.*
