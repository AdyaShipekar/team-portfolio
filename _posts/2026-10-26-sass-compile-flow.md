---
layout: post
title: Sass Compilation Flow
description: A visual overview of how Sass source is compiled into CSS and rendered in the browser.
breadcrumb: true
permalink: /sass-compile-flow
---

<style>
    body {
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
        max-width: 800px;
        margin: 0 auto;
        padding: 40px 20px;
        color: #e0e0e0;
        background: #000;
        line-height: 1.6;
    }

    h1 {
        margin-top: 40px;
        color: #c084fc;
        border-bottom: 2px solid #6d28d9;
        padding-bottom: 10px;
    }

    h2,
    h3 {
        color: #c084fc;
    }

    p {
        margin: 10px 0;
    }

    code {
        color: #e0e0e0;
        background: #1a1a1a;
        padding: 2px 6px;
        border-radius: 3px;
    }

    a {
        color: #e0e0e0;
    }

    .mermaid {
        margin: 24px 0;
        text-align: center;
    }
</style>

This page brings together diagrams for styling, application architecture, authentication, data, interactive features, and project workflow. Each diagram is a conceptual example; the specific components shown may vary from one project to another.

## 1. Sass to Browser

Sass makes styles easier to organize with features such as variables, mixins, and nested rules. A Sass processor compiles these source files into regular CSS, which the browser applies to HTML to display the finished page.

```mermaid
flowchart TD
    subgraph Dev ["Development"]
        SassFiles["Sass Source (.scss) <br/> Variables, Mixins, Nesting"] -->|compiled by| Compiler["Sass Preprocessor / Build Tool <br/> (Dart Sass / Vite)"]
    end

    subgraph Build ["Output"]
        Compiler -->|generates| CSSFile["Compiled Standard CSS <br/> (main.css)"]
    end

    subgraph Browser ["Runtime"]
        CSSFile -->|applied to| HTML["HTML Template <br/> (Static Pages)"]
        HTML -->|renders| Render["Final UI & Visual Theme <br/> (Responsive & Consistent)"]
    end
```

## 2. Client-Server Architecture

This diagram shows a common three-layer web application. The browser sends requests to a backend API, the backend reads or writes data in a storage layer, and then returns a response. A static site such as GitHub Pages can host the frontend, but it needs a separately hosted backend service to handle API requests.

```mermaid
flowchart TB
    subgraph Client ["Client Layer (Frontend)"]
        Browser["User Browser / Static Page <br/> (GitHub Pages + Sass UI)"]
    end

    subgraph Server ["Backend Layer (API & Logic)"]
        Flask["Python / Flask Server <br/> (REST API Endpoints)"]
    end

    subgraph Data ["Data Layer (Storage)"]
        DB[(Database / JSON / SQLite <br/> User Records & Reflections)]
    end

    Browser -->|HTTP Request / Fetch API| Flask
    Flask -->|Query / Save Data| DB
    DB -->|Return Data| Flask
    Flask -->|JSON Response| Browser
```

## 3. Login Request Sequence

This sequence follows a typical login attempt from the user interface to a backend and database. The interface submits credentials, the backend checks the user record, and the result determines whether the user sees the protected area or an error. It illustrates the request-and-response order rather than prescribing a specific authentication implementation.

```mermaid
sequenceDiagram
    autonumber
    actor User as User / Member
    participant FE as Frontend (Login Page)
    participant API as Flask Backend API
    participant DB as Database

    User->>FE: Enter Credentials & Submit
    FE->>API: POST /api/login (JSON Payload)
    activate API
    API->>DB: Query User Record
    DB-->>API: Return User Data / Status

    alt Credentials Valid
        API-->>FE: HTTP 200 OK + Session Token
        FE-->>User: Redirect to Account / Profile View
    else Invalid Credentials
        API-->>FE: HTTP 401 Unauthorized Error
        FE-->>User: Display Fallback / Error Message
    end
    deactivate API
```

## 4. Data Relationships

This entity-relationship diagram sketches one possible data model for users, meetings, reflections, and registrations. A primary key (PK) uniquely identifies a record. The relationship lines show that a user may share multiple reflections and make multiple registrations, while a meeting may have multiple registrations.

```mermaid
erDiagram
    USER ||--o{ REFLECTION : shares
    USER ||--o{ REGISTRATION : reserves
    MEETING ||--o{ REGISTRATION : contains

    USER {
        string username PK
        string email
        string role_status
    }

    MEETING {
        int meeting_id PK
        string day_of_week
        string time_slot
        string location
    }

    REFLECTION {
        int reflection_id PK
        string content
        string timestamp
        boolean is_anonymous
    }

    REGISTRATION {
        int reg_id PK
        string user_ref
        string meeting_ref
    }
```

## 5. Mood Room Interaction States

This state diagram describes the main steps in a mood-selection feature: the user opens the tool, chooses an emotion, and the interface gathers grounding text and matching music before displaying a result. The reset action returns the feature to its starting state so the user can begin again.

```mermaid
stateDiagram-v2
    [*] --> Initial : Open Mood Room Tool

    Initial --> SelectingEmotion : User clicks an emotion button

    state SelectingEmotion {
        [*] --> Analyzing
        Analyzing --> MatchingPrompt : Fetch Grounding Text
        MatchingPrompt --> MatchingMusic : Select Ambient Audio
    }

    SelectingEmotion --> DisplayResult : Match Complete

    DisplayResult --> Reset : Click "Clear / Reset"
    Reset --> Initial
```

## 6. Project Workflow

This workflow represents how an idea can move through a team project: it begins in the parking lot, is prioritized and assigned, then moves through implementation and review before completion. Each transition represents a team decision or handoff, helping clarify what should happen next.

```mermaid
flowchart LR
    ParkingLot["1. Parking Lot <br/> (Design Thinking & Ideation)"] -->|Success Meeting| ToDo["2. ToDo <br/> (Weighted & Assigned)"]
    ToDo -->|Start Coding| InProgress["3. In Progress <br/> (Prototype & PR)"]
    InProgress -->|Review & Test| InReview["4. In Review <br/> (System Tested & Presented)"]
    InReview -->|Accepted| Done["5. Done <br/> (Outcome Delivered)"]

    style ParkingLot fill:transparent
    style ToDo fill:transparent
    style InProgress fill:transparent
    style InReview fill:transparent
    style Done fill:transparent
```
