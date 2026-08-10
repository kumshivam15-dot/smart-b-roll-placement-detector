# 🎬 Smart B-roll Placement Detector

A full-stack application that analyzes video transcripts and automatically identifies transcript segments where **B-roll footage would be visually relevant**.

The system uses an **explainable rule-based detection algorithm** to score transcript segments based on concrete visual cues such as places, objects, and actions. The results are displayed on an interactive transcript timeline where users can accept or reject suggestions.

---

## ✨ Features

- 🎥 Automatic B-roll placement detection
- 🧠 Explainable rule-based scoring algorithm
- 🔍 Detection of concrete visual cues
- 🚫 Excludes direct-to-camera content such as greetings, subscriptions, and sign-offs
- 🚫 Filters weak abstract/reflection-heavy statements
- 📊 Weighted scoring based on visual keywords
- ⏱️ Preserves original transcript segment boundaries
- 📏 Limits B-roll coverage to a maximum of 40% of the video
- ⏸️ Maintains a minimum 3-second gap between selected placements
- 💡 Displays the reason behind every B-roll recommendation
- ❌ Allows users to reject individual suggestions
- 🔄 Allows users to restore rejected suggestions
- 🧪 Includes backend unit tests

---

## 🛠️ Tech Stack

### Frontend

- React
- TypeScript
- Vite
- CSS
- Lucide React

### Backend

- Python
- FastAPI
- Pydantic
- Uvicorn

### Testing

- Python `unittest`

---

## 🏗️ Architecture

```text
                    ┌──────────────────────┐
                    │       Frontend       │
                    │ React + TypeScript   │
                    │       + Vite         │
                    └──────────┬───────────┘
                               │
                               │ POST /detect
                               ▼
                    ┌──────────────────────┐
                    │       FastAPI        │
                    │       Backend        │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   B-roll Detector    │
                    │                      │
                    │ Keyword Matching     │
                    │ Weighted Scoring     │
                    │ Exclusion Filtering  │
                    │ Coverage Limiting    │
                    │ Gap Validation       │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ B-roll Suggestions   │
                    │                      │
                    │ Start / End Time     │
                    │ Score                │
                    │ Explanation          │
                    └──────────────────────┘
