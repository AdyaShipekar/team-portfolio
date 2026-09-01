---
layout: post
title: Nonprofit Ideation
description: Our ideation process for the two nonprofits we selected, as well as our own idea.
breadcrumb: true
codemirror: true
permalink: /ideation
---

## Option 1: Sentri (Poway Recovery Center)


## Option 2: Safe Passage Heals



## Our Option: InTune (Music Recommendation System)

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
- **Avoid lyrics** — instrumental-only toggle. Useful for focus and study use cases, and worth building in early rather than bolting on. Depends on whether the API exposes a reliable instrumental flag; may need a fallback heuristic.
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
 
#### Spotify integration
Link a Spotify account and export selected songs directly into a generated playlist. Turns the output from a list you read into something you actually keep.
 
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
