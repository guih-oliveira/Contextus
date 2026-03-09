# last update 09/03/2025

# Architecture

## System Overview

Contextus operates on six layers working simultaneously:

```
┌─────────────────────────────────────────┐
│         General Language Base           │
│   Pre-trained on broad language data    │
├─────────────────────────────────────────┤
│          Personal User Profile          │
│   Weighted memory + habit detection     │
├─────────────────────────────────────────┤
│     Social Context (Optional Layer)     │
│  Public writing patterns from socials   │
├─────────────────────────────────────────┤
│        Local Conversation Context       │
│         Recent message history          │
├─────────────────────────────────────────┤
│          External Variables             │
│    Time of day, day of week, partner    │
├─────────────────────────────────────────┤
│       Emotional Tone Recognition        │
│        Read-only, non-manipulative      │
└─────────────────────────────────────────┘
```

---

## Layer Descriptions

### 1. General Language Base
Pre-trained on broad language data to understand standard patterns, common phrases and linguistic structure. This is the foundation every user shares.

### 2. Personal User Profile
Learns each user's individual habits over time — vocabulary, shortcuts, tone. Uses **weighted memory**, meaning old patterns are never deleted, only adjusted as behavior evolves.

> Example: if a user gradually shifts from "bora" to "vamos", the system detects the transition and begins suggesting both — reflecting the real gradual change.

### 3. Social Context (Optional Layer)
With explicit user consent, integrates public writing patterns from social media to enrich the personal profile. This layer makes the profile significantly more accurate from the start — reducing the cold start problem where the system has little data to learn from initially.

> This layer is strictly opt-in. It enriches suggestions, never surveillance.

### 4. Local Conversation Context
Reads the recent message history in real time to understand what is being discussed and how the conversation is flowing before making any suggestion.

### 5. External Variables (Exogenous Variables)
Factors outside the message itself that influence behavior:
- Time of day → suggests "bom dia" vs "boa noite"
- Day of week → weekday vs weekend communication patterns
- Conversation partner → formal vs informal vocabulary

### 6. Emotional Tone Recognition
Recognizes shifts in emotional tone across the conversation and adjusts suggestions accordingly. **This layer reads emotion as a signal, not a directive** — it never pushes the user toward a specific emotional state.

---

## Key Design Decisions

### Habit vs. Error Detection
The system distinguishes between a linguistic habit and a genuine mistake. Habits are preserved. Errors are corrected.

### Stable Learning Model
Suggestions are not updated after every single interaction. The system is resistant to noise — an ignored suggestion on a rushed morning does not rewrite the user's profile. Patterns are confirmed over time.

### Ethical Scope
The corrector improves communication. It does not make decisions for the user, push emotional states, or manipulate behavior. Informed consent is required before personalization activates.

---

## Privacy Architecture — Federated Learning

All personal profile data stays on the user's device. No readable user data is ever transmitted to external servers.

```
User Device                          Central Server
┌─────────────────────┐             ┌──────────────────┐
│  Personal Profile   │             │   General Model  │
│  (never leaves)     │──────────▶  │  (improves from  │
│                     │  abstract   │  abstract math   │
│  Conversation data  │  math only  │  adjustments,    │
│  (never leaves)     │             │  not raw data)   │
└─────────────────────┘             └──────────────────┘
```

**What this means in practice:**
- The developer cannot access user profiles
- Investors have no data to buy
- Governments have nothing to subpoena
- A data breach exposes nothing readable

> Contextus is the first corrector that knows you without exposing you.
