# Contributing to The Nominarium

> **An AI Brand Naming & Identity Engine — built by DiegosDev Studio**

Thank you for your interest in contributing! The Nominarium is a single-file, open web application powered by Gemini 2.0 Flash. Every contribution — bug fix, feature idea, or design improvement — is genuinely appreciated.

-----

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [How to Contribute](#how-to-contribute)
- [Development Guidelines](#development-guidelines)
- [Submitting a Pull Request](#submitting-a-pull-request)
- [Reporting Bugs](#reporting-bugs)
- [Feature Requests](#feature-requests)
- [Style Guide](#style-guide)

-----

## Code of Conduct

This project follows a simple rule: **be respectful**. Constructive feedback is welcome; personal attacks are not. Contributors who violate this principle may be removed from the project.

-----

## Getting Started

The Nominarium is intentionally dependency-free — there is no build step, no package manager, and no local server required.

### Prerequisites

- A modern browser (Chrome, Firefox, or Edge recommended)
- A [Gemini API key](https://aistudio.google.com/app/apikey) for testing AI features
- A code editor (VS Code recommended)
- Git

### Setup

```bash
# 1. Fork the repository on GitHub, then clone your fork
git clone https://github.com/YOUR_USERNAME/nominarium.git

# 2. Navigate into the project
cd nominarium

# 3. Open the app directly in your browser
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```

No `npm install`. No `build`. Just open and code.

-----

## Project Structure

```
nominarium/
├── index.html          # The entire application (HTML + CSS + JS, single file)
├── README.md           # Project overview and usage guide
├── CONTRIBUTING.md     # This file
└── LICENSE             # License information
```

Everything lives in `index.html`. The three main sections are clearly commented inside the file:

|Section   |Description                                                     |
|----------|----------------------------------------------------------------|
|`<style>` |All CSS — design tokens, layout, animations, glassmorphism      |
|`<body>`  |HTML structure — nav, command panel, results, modals            |
|`<script>`|All JavaScript — API calls, retry logic, JSON parsing, rendering|

-----

## How to Contribute

### 1. Find something to work on

- Browse [open issues](../../issues) and look for ones labeled `good first issue` or `help wanted`
- Check the [feature requests](#feature-requests) section below
- Spotted a bug? [Report it](#reporting-bugs) first, then fix it

### 2. Create a branch

```bash
# Always branch off main
git checkout main
git pull origin main
git checkout -b feat/your-feature-name
# or
git checkout -b fix/bug-description
```

**Branch naming conventions:**

|Prefix     |Use for                             |
|-----------|------------------------------------|
|`feat/`    |New features                        |
|`fix/`     |Bug fixes                           |
|`style/`   |CSS / visual changes only           |
|`refactor/`|Code cleanup with no behavior change|
|`docs/`    |Documentation updates               |

### 3. Make your changes

- Keep changes focused — one feature or fix per pull request
- Test your changes locally in at least two browsers
- If your change touches the AI logic, test with a real Gemini API key

### 4. Commit your changes

```bash
git add .
git commit -m "feat: add export-to-PDF for identity cards"
```

Follow [Conventional Commits](https://www.conventionalcommits.org/) format:

```
type(optional scope): short description

Longer explanation if needed. Wrap at 72 characters.
Explain WHY, not just WHAT.
```

-----

## Development Guidelines

### The Single-File Rule

The Nominarium is proudly a single `index.html` file. **Please do not introduce a build system, external JS files, or npm dependencies** without opening a discussion issue first. External fonts (Google Fonts) and CDN scripts are acceptable.

### AI / API Logic

- **Model**: Always use `gemini-2.0-flash` — do not change the model without discussion
- **Retry Loop**: The 429 retry logic (3 attempts, 2s delay) must remain intact
- **JSON Safety**: The regex strip before `JSON.parse` must remain in place
- **API Key**: Must stay in `localStorage` only — never log, transmit, or hardcode it

### CSS / Design System

The Nominarium uses a strict design token system via CSS custom properties:

```css
--bg: #0B0F19          /* Page background */
--cyan: #22D3EE        /* Primary accent */
--blue: #2563EB        /* Secondary accent */
--text: #F8FAFC        /* Body text */
--text-muted: #94A3B8  /* Secondary text */
```

- **Do not introduce white or light backgrounds** — the dark luxury aesthetic is intentional
- Glassmorphism cards use `backdrop-filter: blur()` — preserve this on all new card elements
- Buttons must use the cyan → blue gradient

### JavaScript

- Vanilla JS only — no frameworks or libraries
- Use `async/await` for all async operations
- Always wrap API calls in `try/catch`
- Keep the `safeParseJSON()` function as the single point of JSON parsing

-----

## Submitting a Pull Request

1. Push your branch to your fork:
   
   ```bash
   git push origin feat/your-feature-name
   ```
1. Open a Pull Request against the `main` branch of the upstream repository
1. Fill in the PR template:
- **What does this PR do?**
- **How was it tested?**
- **Screenshots** (if visual changes)
- **Related issue** (e.g. `Closes #12`)
1. A maintainer will review your PR within a few days. Be prepared for feedback and revision requests — this is normal and healthy.

-----

## Reporting Bugs

Before opening a bug report, please:

- Check that you’re using a supported browser
- Confirm your Gemini API key is valid and has quota remaining
- Search [existing issues](../../issues) to avoid duplicates

When filing a bug, include:

```
**Browser & version:**
**Operating system:**
**Steps to reproduce:**
**Expected behavior:**
**Actual behavior:**
**Console errors (if any):**
```

-----

## Feature Requests

Feature ideas are welcome! Open an issue with the `enhancement` label and describe:

- **The problem** you’re trying to solve
- **Your proposed solution**
- **Alternatives you considered**

Current ideas on the roadmap (up for grabs):

- Export identity cards as PNG or PDF
- Share a generated identity via URL (encoded in hash)
- Dark/light theme toggle
- Additional AI model support (Claude, OpenAI)
- Localization / multi-language support

-----

## Style Guide

### HTML

- Use semantic elements (`<section>`, `<nav>`, `<main>`, `<footer>`)
- Keep IDs kebab-case: `id="results-area"`
- Keep classes kebab-case: `class="identity-card"`

### CSS

- Add new design tokens to `:root` — don’t hardcode colors inline
- Group properties: positioning → box model → typography → visual → animation
- Comment non-obvious selectors

### JavaScript

- Use `const` by default, `let` only when reassignment is needed
- Name functions with verbs: `renderCards()`, `fetchIdentities()`, `showError()`
- Keep functions small and single-purpose

-----

## Questions?

Open a [Discussion](../../discussions) or reach out via the issues tab. We’re happy to help you get oriented.

**Built with obsession by [DiegosDev Studio](https://github.com/diegosdevstudio)** ⚡
