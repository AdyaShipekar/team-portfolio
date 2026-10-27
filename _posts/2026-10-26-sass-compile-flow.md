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

Sass source files use variables, mixins, and nesting. A Sass preprocessor compiles them into standard CSS, which is applied to HTML and rendered as the final responsive interface.

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
