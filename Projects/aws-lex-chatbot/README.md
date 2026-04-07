# 🤖 Project 3 — AWS Lex Quiz Chatbot

> **Client:** CloudLearners Inc. | **Platform:** Amazon Lex | **Team:** Phenyo, Tumelo, Nhlanhla, Grace

---

## 📌 Project Overview

As part of the **AWS re/Start Special Projects** series, our team was tasked by fictional client **CloudLearners Inc.** to design and deploy an interactive, AI-powered quiz chatbot using **Amazon Lex**. The chatbot tests learners on their knowledge of AWS services through multiple-choice questions with instant feedback.

---

## 🎯 Client Requirements

CloudLearners Inc. needed:
- An interactive chatbot for learners
- A knowledge quiz focused on Amazon S3
- Multiple-choice questions (A / B / C format)
- Instant feedback for correct and incorrect answers
- A simple, engaging, and scalable learning experience

---

## 💡 Our Solution

We built a fully functional quiz bot in **Amazon Lex** that:

| Feature | Description |
|---|---|
| **Quiz Trigger** | Users start with phrases like "Start quiz" or "Quiz me on S3" |
| **Multiple Choice** | Users respond with A, B, or C |
| **Instant Feedback** | Bot confirms correct answers or explains the right answer |
| **Branching Logic** | Conditional responses route users based on their answers |
| **Multi-question Flow** | Bot progresses through questions seamlessly |

---

## 🏗️ How It Was Built

### Amazon Lex Core Components

```
┌─────────────────────────────────────────────────┐
│                   Amazon Lex Bot                 │
│                                                 │
│  🎯 Intent: S3Quiz                              │
│  ├── Utterances: "Start quiz", "Quiz me on S3"  │
│  ├── Slots: Capture A / B / C responses         │
│  ├── Responses: Correct / Incorrect feedback    │
│  └── Branching: Route to next question          │
└─────────────────────────────────────────────────┘
```

### Quiz Interaction Flow

```
User: "Start Quiz"
        │
        ▼
Bot: "What does S3 stand for?"
     A) Simple Storage Service
     B) Secure Server Storage
     C) Smart Storage System
        │
   ┌────┴────┐
   A         B or C
   │         │
   ▼         ▼
✅ Correct  ❌ Incorrect
"S3 = Simple  "The answer is
Storage       Simple Storage
Service"      Service"
   │         │
   └────┬────┘
        ▼
"What is Amazon S3 mainly used for?"
     A) Cloud storage
     B) Web hosting
     C) Cloud computing
        │
       ...
```

### Intents & Utterances

**Intent: `S3Quiz`**
- "Start quiz"
- "Quiz me on S3"
- "I'm ready for the quiz"
- "Let's begin"

**Intent: `S3Info`** *(Part 1 — simple bot)*
- "What is S3?"
- "Tell me about Amazon S3"

---

## ⚡ Why This Solution Is Valuable

- 🤖 **Automates learning assessments** — no instructor needed for basic knowledge checks
- 🎮 **Interactive education** — conversational format keeps learners engaged
- ⚡ **Instant feedback** — learners know immediately if they're right or wrong
- 📈 **Scales to thousands** — Lex handles concurrent users without extra infrastructure
- 💰 **Cost-effective** — reduces reliance on manual trainers for repetitive quiz content

---

## 🚧 Challenges & Solutions

### Challenge 1 — Exact Slot Naming
**Problem:** Slot values had to match exactly — incorrect wording prevented the bot from recognising responses correctly.

**Solution:** Standardised all slot values and response strings throughout the bot configuration. Consistent naming conventions were enforced across all intents.

### Challenge 2 — Slot Type Confusion
**Problem:** Initially attempted to create custom slot types, which caused unexpected errors in the branching logic.

**Solution:** Discovered and switched to Amazon Lex's pre-configured built-in slot types, which resolved the errors and simplified the configuration.

---

## 📊 Presentation

This project included a **PowerPoint presentation and live demo** delivered to a simulated client audience.

📄 [View Presentation](./AWS_Lex_Chatbot_Presentation.pptx)

**Presentation covered:**
- Introduction to Amazon Lex
- Client requirements (CloudLearners Inc.)
- Solution overview & quiz structure
- Technical approach: intents, utterances, branching
- Live demo walkthrough
- Challenges faced and solutions applied
- Key takeaways

**Presenters:** Phenyo (slides 1–3) · Tumelo (slides 4–5) · Nhlanhla (slides 6–8) · Grace (slides 9–10)

---

## 🔑 Key Takeaways

1. **Amazon Lex makes conversational AI accessible** — no ML background required to build a functional chatbot.
2. **Intent + Utterance design is everything** — the more natural your utterances, the better users interact.
3. **Branching logic creates dynamic experiences** — conditional responses transform a static Q&A into an actual quiz.
4. **Slot types need careful planning** — always explore built-in types before creating custom ones.
5. **Testing covers all paths** — test correct *and* incorrect answer flows to catch broken branches.

---

## 🛠️ AWS Services Used

| Service | Purpose |
|---|---|
| **Amazon Lex** | Core chatbot and NLP engine |
| **AWS Management Console** | Bot configuration and testing |

---

## 📁 Project Files

```
aws-lex-chatbot/
├── README.md                          ← This file
└── AWS_Lex_Chatbot_Presentation.pptx  ← Client presentation
```
