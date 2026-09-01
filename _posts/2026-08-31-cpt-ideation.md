```markdown
---
layout: post
title: Nonprofit Ideation
description: Our ideation process for the two nonprofits we selected, as well as our own idea.
breadcrumb: true
codemirror: true
permalink: /ideation
---

## **Option 1: Sentri (Poway Recovery Center)**

### Concept
A digital interface for the Poway Recovery Center (PRC) specifically tailored to the psychology of addiction recovery. It helps individuals navigate PRC's meetings and programs, while providing staff with visual tools to track patient progress without inducing shame.

### Unique Frontend Features for Addiction Recovery
- **"Low-Cognitive-Load" Meeting Finder:** People seeking addiction help are often in active crisis or withdrawal, meaning their executive function is compromised. The UI abandons complex drop-down menus in favor of a massive, one-question-per-screen flow (e.g., a giant button asking "Are you looking for yourself or a loved one?"). 
  * *Why this helps the nonprofit:* It dramatically lowers the bounce rate on the PRC website, ensuring addicts actually finish the flow and get routed to the correct AA/NA or family meeting rather than giving up out of frustration.
- **Compassionate "Sobriety Garden" Tracker:** Traditional "sobriety streak" counters rely on big numbers that reset to zero upon a relapse, which often triggers severe shame spirals. Sentri uses a visual "Sobriety Garden" UI. Logging in grows the ecosystem; a relapse doesn't "kill" the garden, but visibly shifts the "seasons."
  * *Why this helps the nonprofit:* It aligns with modern addiction psychology (harm reduction). It keeps patients engaged with PRC's ecosystem even if they slip up, ensuring they come back to their meetings instead of hiding from their counselors.
- **Meeting Room Availability Heatmap (Staff Dashboard):** A color-coded grid UI for PRC intake staff showing real-time capacity for their various group therapy and recovery meetings (Green = Seats Available, Red = Full).
  * *Why this helps the nonprofit:* PRC hosts multiple programs. This visual dashboard allows front-desk staff to instantly balance room capacities and confidently route walk-ins to the right session in seconds.

---

## **Option 2: Safe Passage Heals**

### Concept
An interactive web platform for Safe Passage Heals that centralizes community events and provides an interactive "Path to Recovery" simulation, engineered strictly around the safety, trauma responses, and educational pacing of domestic violence (DV) survivors.

### Unique Frontend Features for DV & Trauma Support
- **Interactive "Branching Pathway" Map UI:** For the "Path to Recovery" simulation, the frontend utilizes a visual, node-based map of the virtual neighborhood. As users successfully interact with characters (e.g., Trusted Adult → Therapist → DV Hotline), the path visually illuminates and unlocks new nodes.
  * *Why this helps the nonprofit:* It transforms a static educational checklist into an engaging, gamified visual journey. This keeps users actively participating in the simulation longer, ensuring Safe Passage Heals successfully delivers their full educational curriculum.
- **"Paced Learning" Content Blurs (Anti-Flooding UI):** When interacting with the virtual counselor or AI assistant, heavy topics (like legal steps or police intervention) are initially hidden behind a soft CSS blur with a "Tap to Reveal" prompt.
  * *Why this helps the nonprofit:* Trauma survivors often experience "flooding" (being overwhelmed by too much intense information at once). This UI gives the user complete agency over their exposure to heavy topics, ensuring they can pace their own learning without being triggered into a panic response.
- **Discreet "Low-Friction" Event Registration Modal:** For the Dynamic Event Calendar, clicking an event opens a minimalist UI modal that only asks for a first name and an email, intentionally omitting fields for home addresses, phone numbers, or last names.
  * *Why this helps the nonprofit:* DV survivors are highly protective of their location and identity data. By visually removing invasive input fields, the nonprofit drastically increases workshop and support group registration rates. 
- **Data-Driven Wellness Scales (Anonymized for Grants):** Replacing standard multiple-choice quizzes in the simulation with visual 1–5 scale slider assessments to measure user emotions and confidence before and after they use the platform.
  * *Why this helps the nonprofit:* The frontend automatically aggregates this slider data into a visual chart for the shelter directors. When Safe Passage Heals applies for funding, they can print out this UI chart as hard proof that their digital simulation successfully increases survivor confidence and reduces anxiety.

---

## **Our Option: InTune (Music Recommendation System)**

### Concept
 
An app that takes how a user feels (or how they *want* to feel) and returns ranked music recommendations. Recommendations are drawn from the Apple Music API and ranked using popularity and online ratings, plus a quantitative match score against the user's stated goal.


Take a look at our KanBan board to know our project plan and workflow: [Team Kanban Board](https://github.com/users/AdyaShipekar/projects/5)


 
---
 
### Core Pipeline
 

```

Emotion
→ Desired characteristics
→ Search (candidate LIST)
→ Iterate over candidates
→ Select
→ Calculate match %
→ Recommendation LIST
→ Output

```
 
**Stage notes**
 
| Stage | What happens |
|---|---|
| Emotion input | User picks current mood or target effect |
| Desired characteristics | Mood maps to audio/metadata traits (tempo, energy, valence, instrumental, era) |
| Search | Query Apple Music API for candidates matching traits |
| Iterate | Score each candidate against the trait profile |
| Select | Filter to top N, dedupe artists so one artist doesn't dominate |
| Match % | Quantitative fit score shown to user |
| Output | Ranked list with match %, popularity, rating |
 
---
 
### Input Model
 
#### Mood (how you feel now)
- Happy
- Sad
- Anxious
- Calm
- Unmotivated
- Angry
#### Desired effect (how you want to feel) — likely the better primary axis
- Calm down
- Focus
- Become energized
- Improve mood
- Maintain current mood

We plan to use an LLM to be able to TAKE your desired effect and CONVERT it into a mood, to reduce the primary vector into a smaller number of one-word inputs to the actual system.

**Design tension:** mood and effect are not the same input. "Sad" doesn't tell you whether the user wants to be lifted out of it or sit in it. Sorting by *desired effect* captures intent directly, which is probably the stronger default. A possible resolution: ask for mood first (easy, low-friction), then ask what they want to do with it. Two taps, and the pair together is far more informative than either alone.
 
#### Additional filters
- Genre
- Age group / era
- Avoid lyrics — instrumental-only toggle. Useful for focus and study use cases.
---
 
### Variables & Classes
 
Each variable has associated songs, and each emotion has songs mapped to it. Sketch of the data model:
 
- **Song** — id, title, artist, genre, era, popularity score, rating, instrumental (bool), audio traits
- **Mood** — label, associated trait profile
- **Effect** — label, target trait profile (the state we're steering toward)
- **User** — saved preferences, listening history, playlists
- **Match** — song × goal → score
The match score is the piece that makes this more than a genre filter. It's worth deciding early what goes into it and in what proportion: trait distance from the target profile, popularity, rating, and possibly personal history.
 
---
 
### Ranking Signals
 
- Apple Music popularity
- Online ratings / aggregate critical scores
- Trait distance from the target profile
- (Later) user's own history and saves
Popularity alone will push everything toward the same few hundred tracks. Trait distance is what keeps results feeling specific to the request.
 
---
 
### Future Directions
 
#### App integration
Link a Spotify/Apple Music account and export selected songs directly into a generated playlist. Turns the output from a list you read into something you actually keep.

#### LLM situation matching
Let users describe a *situation* in natural language — "studying for an exam tomorrow," "long drive at night," "cleaning the apartment" — and have an LLM map it to the appropriate mood, genre, and age group, then feed that into the existing pipeline. This handles the long tail of contexts that a fixed mood menu can't cover, and it reuses the whole backend as-is.
 
#### Social / transactional layer
Users can see what others are listening to and what they've added to their playlists. Options to explore:
- Public activity feed
- "Others who felt anxious added…" — aggregate, anonymous, tied to the mood taxonomy
- Followable playlists
The aggregate version is interesting because it feeds back into ranking: if a track consistently gets saved by people asking to calm down, that's a real signal the recommender can learn from.
 
---
 
### Rough Build Order
 
**v1** — Effect picker → Apple Music search → ranked list with match %
**v2** — Genre, era, and instrumental filters; refined scoring
**v3** — Spotify export; accounts and saved playlists
**v4** — LLM situation input
**v5** — Social layer

```