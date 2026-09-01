---
layout: post
title: Nonprofit Ideation
description: Our ideation process for the two nonprofits we selected, as well as our own idea.
breadcrumb: true
codemirror: true
permalink: /ideation
---

## **Our Option: InTune (Music Recommendation System)**

### Concept
 
An app frontend that takes how a user feels (or how they *want* to feel) and returns ranked music recommendations visually, acting as an active tool for emotional regulation and mental health management. 

Take a look at our KanBan board to know our project plan and workflow: [Team Kanban Board](https://github.com/users/AdyaShipekar/projects/5)

---
 
### Core UI Pipeline
 
| Stage | User Interface Action |
|---|---|
| Emotion input | User clicks/selects current mood or target effect from buttons |
| Match % | UI displays a quantitative fit score next to track items |
| Output | Renders a ranked list view with match %, popularity, and rating |
 
---
 
### Frontend Input Model & Mental Health Features
 
#### Mood (how you feel now) - Button Selectors
- Happy
- Sad
- Anxious
- Calm
- Unmotivated
- Angry

#### Desired effect (how you want to feel) - Primary Axis
- Calm down (Anxiety reduction)
- Focus (ADHD/Executive dysfunction support)
- Become energized (Depressive episode countering)
- Improve mood
- Maintain current mood

**Design tension:** Ask for mood first (easy, low-friction UI), then prompt what they want to do with it. Two taps, highly intuitive frontend flow. 
*Why this is helpful:* When users are experiencing a panic attack or depressive crash, long forms cause immediate app abandonment. A two-tap visual interface bypasses this friction entirely.
 
#### Mental Health UI Filters & Tools
- **"Breathe & Sync" Audio-Visualizer:** A UI element on the playback screen that generates a softly pulsing circle synced exactly to the BPM of calming tracks (ideally around 60 BPM). 
  * *Why this is helpful:* Guides users through box breathing or paced respiration during an anxiety attack.
- **Content/Trigger Warning Toggles:** Visual toggle switches allowing users to strictly filter out lyrical themes (e.g., filtering out songs tagged with "grief," "substance use," or "high intensity").
  * *Why this is helpful:* Prevents the algorithm from surfacing a song that could trigger a PTSD flashback.

---
 
### Rough Frontend Build Order
 
**v1** — Effect picker UI → Ranked list view with match %
**v2** — Genre, trigger warning, and instrumental filter toggles
**v3** — "Breathe & Sync" visualizer and Spotify export
**v4** — Text-based situation input box
**v5** — Social feed layer

---

## **Our Option: Sentri (Poway Recovery Center)**

### Concept

A digital interface for the Poway Recovery Center (PRC) specifically tailored to the psychology of addiction recovery. It helps individuals navigate PRC's meetings and programs, while providing staff with visual tools to track patient progress without inducing shame.

---

### Unique Frontend Features for Addiction Recovery

- **"Low-Cognitive-Load" Meeting Finder:** People seeking addiction help are often in active crisis or withdrawal, meaning their executive function is compromised. The UI abandons complex drop-down menus in favor of a massive, one-question-per-screen flow (e.g., a giant button asking "Are you looking for yourself or a loved one?"). 
  * *Why this helps the nonprofit:* It dramatically lowers the bounce rate on the PRC website, ensuring addicts actually finish the flow and get routed to the correct AA/NA or family meeting rather than giving up out of frustration.
- **Compassionate "Sobriety Garden" Tracker:** Traditional "sobriety streak" counters rely on big numbers that reset to zero upon a relapse, which often triggers severe shame spirals. Sentri uses a visual "Sobriety Garden" UI. Logging in grows the ecosystem; a relapse doesn't "kill" the garden, but visibly shifts the "seasons."
  * *Why this helps the nonprofit:* It aligns with modern addiction psychology (harm reduction). It keeps patients engaged with PRC's ecosystem even if they slip up, ensuring they come back to their meetings instead of hiding from their counselors.
- **Meeting Room Availability Heatmap (Staff Dashboard):** A color-coded grid UI for PRC intake staff showing real-time capacity for their various group therapy and recovery meetings (Green = Seats Available, Red = Full).
  * *Why this helps the nonprofit:* PRC hosts multiple programs. This visual dashboard allows front-desk staff to instantly balance room capacities and confidently route walk-ins to the right session in seconds.

---

## **Our Option: Safe Passage Heals**

### Concept

An interactive web platform for Safe Passage Heals that centralizes community events and provides an interactive "Path to Recovery" simulation, engineered strictly around the safety, trauma responses, and educational pacing of domestic violence (DV) survivors.

---

### Unique Frontend Features for DV & Trauma Support

- **Interactive "Branching Pathway" Map UI:** For the "Path to Recovery" simulation, the frontend utilizes a visual, node-based map of the virtual neighborhood. As users successfully interact with characters (e.g., Trusted Adult → Therapist → DV Hotline), the path visually illuminates and unlocks new nodes.
  * *Why this helps the nonprofit:* It transforms a static educational checklist into an engaging, gamified visual journey. This keeps users actively participating in the simulation longer, ensuring Safe Passage Heals successfully delivers their full educational curriculum.
- **"Paced Learning" Content Blurs (Anti-Flooding UI):** When interacting with the virtual counselor or AI assistant, heavy topics (like legal steps or police intervention) are initially hidden behind a soft CSS blur with a "Tap to Reveal" prompt.
  * *Why this helps the nonprofit:* Trauma survivors often experience "flooding" (being overwhelmed by too much intense information at once). This UI gives the user complete agency over their exposure to heavy topics, ensuring they can pace their own learning without being triggered into a panic response.
- **Discreet "Low-Friction" Event Registration Modal:** For the Dynamic Event Calendar, clicking an event opens a minimalist UI modal that only asks for a first name and an email, intentionally omitting fields for home addresses, phone numbers, or last names.
  * *Why this helps the nonprofit:* DV survivors are highly protective of their location and identity data. By visually removing invasive input fields, the nonprofit drastically increases workshop and support group registration rates. 
- **Data-Driven Wellness Scales (Anonymized for Grants):** Replacing standard multiple-choice quizzes in the simulation with visual 1–5 scale slider assessments to measure user emotions and confidence before and after they use the platform.
  * *Why this helps the nonprofit:* The frontend automatically aggregates this slider data into a visual chart for the shelter directors. When Safe Passage Heals applies for funding, they can print out this UI chart as hard proof that their digital simulation successfully increases survivor confidence and reduces anxiety.