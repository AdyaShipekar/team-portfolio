---
layout: post
title: Nonprofit Ideation
description: Our ideation process for the two nonprofits we selected, as well as our own idea.
breadcrumb: true
codemirror: true
permalink: /ideation
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nonprofit Ideation</title>
    <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            line-height: 1.6;
            max-width: 800px;
            margin: 0 auto;
            padding: 40px 20px;
            color: #e0e0e0;
            background: #000000;
        }
        
        h1 { 
            font-size: 28px; 
            margin-top: 40px; 
            margin-bottom: 20px; 
            color: #c084fc;
            border-bottom: 2px solid #6d28d9;
            padding-bottom: 10px;
        }
        
        h2 { 
            font-size: 22px; 
            margin-top: 30px; 
            margin-bottom: 15px; 
            color: #c084fc;
        }
        
        h3 { 
            font-size: 18px; 
            margin-top: 20px; 
            margin-bottom: 10px; 
            color: #a78bfa;
        }
        
        p { margin: 10px 0; }
        ul, ol { margin: 10px 0 10px 20px; }
        li { margin: 6px 0; }
        
        code { 
            background: #1a1a1a; 
            padding: 2px 6px; 
            border-radius: 3px;
            font-size: 14px;
            color: #e0e0e0;
        }
        
        strong { color: #e0e0e0; }
        a { color: #e0e0e0; text-decoration: underline; }
        a:hover { text-decoration: underline; }
        
        hr { border: none; border-top: 1px solid #6d28d9; margin: 30px 0; }
    </style>
</head>
<body>
    <div id="content"></div>

    <script>
        const markdown = `# Nonprofit Ideation + Ideas

## Option 1: Sentri (Poway Recovery Center)
**Addiction Recovery Platform**

### Core Features
- **Low-Cognitive-Load Meeting Finder** — One question per screen, simple routing (self vs loved one)
- **Sobriety Garden Tracker** — Visual, shame-free progress (relapse = season shift, not reset)
- **Staff Dashboard** — Real-time meeting capacity heatmap (Green/Red availability)

### Ideas to Add
- **Sponsor Matching** — Connect newcomers with sponsors (matched by availability, recovery stage, experience)
- **Trigger Tracker** — Log cravings/situations to identify relapse patterns over time
- **Meeting Verification** — Check-in at meetings for court/probation documentation
- **Crisis Buddy System** — Real-time 1-on-1 connection when experiencing strong cravings
- **Daily Affirmations** — Personalized motivation based on recovery stage & personal goals
- **Attendance History** — Visual proof of consistency in meeting participation
- **Local Resource Hub** — Emergency hotlines, nearby NA/AA meetings, therapy options all in one place
- **Medication Reminder** — Track medications + side effects + appointment scheduling

---

## Option 2: Safe Passage Heals
**DV Survivor Support Platform**

### Core Features
- **Branching Pathway Map** — Gamified node-based recovery simulation (visual progress)
- **Paced Learning (Blur UI)** — Heavy topics hidden until user taps to reveal (anti-flooding)
- **Minimal Event Registration** — Only first name + email (no invasive fields)
- **Wellness Metrics** — Pre/post scale sliders for grant data aggregation

### Ideas to Add
- **Safety Planning Tool** — Interactive, personalized escape plans (where to go, what to pack, who to call)
- **Legal Resource Guide** — Restraining order templates, custody guidance, divorce resources
- **Housing/Job Board** — Partner with local employers/housing providers for safe opportunities
- **Trauma-Informed Therapist Locator** — Find vetted DV-specialized therapists nearby
- **Financial Independence Tools** — Budget planning, credit recovery after financial abuse
- **Child Safety Education** — Age-appropriate resources for kids to recognize abuse & reach out
- **Encrypted Journal** — Private space to process trauma and identify patterns
- **Trusted Supporter Network** — Schedule check-ins from friends/family (coordinates safety monitoring)
- **Court Companion Matching** — Connect survivors with advocates for court hearings

---

## Option 3: InTune (Music Recommendation System)
**Mood-Based Music Recommender**

### Core Pipeline
Emotion/Effect → Apple Music API → Score (traits + popularity + ratings) → Ranked List

### Key Features
- **Dual Input** — Current mood + desired effect (e.g., "Sad" → "Become energized")
- **Match % Score** — Quantitative fit based on tempo, energy, valence, era
- **Smart Filters** — Genre, era, instrumental toggle
- **LLM Situation Mapping** — Natural language input ("studying for exam") → auto-detect best mood/effect

### Data Model
- **Song** — title, artist, genre, era, popularity, rating, instrumental, audio traits
- **Mood** — label, trait profile
- **Effect** — target trait profile (desired state)
- **Match Score** — trait distance + popularity + rating + user history

### Build Order
- **v1** — Effect picker → Search → Ranked list with match %
- **v2** — Genre, era, instrumental filters + refined scoring
- **v3** — Spotify/Apple Music export + saved playlists
- **v4** — LLM situation input
- **v5** — Social layer (see what others felt/added)

### Ideas to Add
- **Mood Journal** — Track emotion changes over time + playlist effectiveness
- **Therapy Integration** — Share mood data with therapist (privacy-first)
- **Study/Focus Sessions** — Timer mode with curated playlists (Pomodoro-style)
- **Emotional Progression** — Show "journey" of mood shifts throughout the day
- **Collaborative Playlists** — Friends add songs to shared "vibe" playlists
- **Lyric Sensitivity Toggle** — Blur/hide lyrics addressing depression, heartbreak, etc.
- **Sleep Mode** — Gentle decay in energy + gradual fade-out (not jarring ends)
- **Seasonal Mood Tracking** — Detect SAD patterns, suggest light/upbeat recs in winter`;

        document.getElementById('content').innerHTML = marked.parse(markdown);
    </script>
</body>
</html>