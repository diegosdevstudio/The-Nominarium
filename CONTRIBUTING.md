# Contributing to The Nominarium

> **An AI Brand Naming & Identity Engine — built by DiegosDev Studio**

Thank you for your interest in contributing! The Nominarium is a single-file, open web application powered by a multi-model AI router (Claude, GPT-4o, Gemini, DeepSeek). Every contribution — bug fix, feature idea, or design refinement — is genuinely appreciated.

---

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

---

## Code of Conduct

This project follows a simple rule: **be respectful**. Constructive feedback is welcome; personal attacks are not. Contributors who violate this principle may be removed from the project.

---

## Getting Started

The Nominarium is intentionally dependency-free — there is no build step, no package manager, and no local server required.

### Prerequisites

- A modern browser (Chrome, Firefox, or Edge recommended)
- At least one API key from a supported provider (Anthropic, OpenAI, Google, or DeepSeek) for testing AI features
- A code editor (VS Code recommended)
- Git

### Setup

```bash
# 1. Fork the repository on GitHub, then clone your fork
git clone https://github.com/YOUR_USERNAME/nominarium.git

# 2. Navigate into the project
cd nominarium

# 3. Open the app directly in your browser
open nominarium.html        # macOS
start nominarium.html       # Windows
xdg-open nominarium.html    # Linux
```

No `npm install`. No `build`. Just open and code.

---

## Project Structure

```
nominarium/
├── nominarium.html     # The entire application (HTML + CSS + JS, single file)
├── README.md           # Project overview and usage guide
├── CONTRIBUTING.md     # This file
└── LICENSE             # License information
```

Everything lives in `nominarium.html`. The three main sections are clearly commented inside the file:

| Section | Description |
|---|---|
| `<style>` | All CSS — design tokens, layout, animations, glassmorphism |
| `<body>` | HTML structure — nav, model engine dropdown, command panel, results, modals |
| `<script>` | All JS — multi-model router, API calls, retry logic, JSON safety, history, PDF |

---

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

| Prefix | Use for |
|---|---|
| `feat/` | New features |
| `fix/` | Bug fixes |
| `style/` | CSS / visual changes only |
| `refactor/` | Code cleanup with no behavior change |
| `docs/` | Documentation updates |

### 3. Make your changes

- Keep changes focused — one feature or fix per pull request
- Test your changes locally in at least two browsers
- If your change touches AI logic, test with a real key for the affected provider
- If your change touches the model router, test with **all four providers** if possible

### 4. Commit your changes

```bash
git add .
git commit -m "feat: add token count display per model"
```

Follow [Conventional Commits](https://www.conventionalcommits.org/) format:

```
type(optional scope): short description

Longer explanation if needed. Wrap at 72 characters.
Explain WHY, not just WHAT.
```

---

## Development Guidelines

### The Single-File Rule

The Nominarium is proudly a single `nominarium.html` file. **Do not introduce a build system, external JS files, or npm dependencies** without opening a discussion issue first. External fonts via Google Fonts CDN are acceptable.

### AI / API Logic

The app uses a multi-model router. Each provider has its own endpoint, auth header pattern, and response shape. The following rules apply to all providers:

- **Default model**: Claude 3.5 Sonnet (`claude-3-5-sonnet-20241022`) — the Creative Historian specialist, pre-selected on load. Do not change the default without discussion.
- **Model assignments**: Do not swap provider-to-model mappings without discussion. The specialist roles are intentional.

| Provider | Model String | Specialist Role |
|---|---|---|
| Anthropic | `claude-3-5-sonnet-20241022` | Creative Historian |
| OpenAI | `gpt-4o` | Logic Expert |
| Google | `gemini-1.5-pro` | Visual Architect |
| DeepSeek | `deepseek-chat` | Pro Manipulator |

- **Retry Loop**: The 429 retry logic (3 attempts, 2-second delay) must remain intact for every provider
- **JSON Safety**: The `safeParseJSON()` function — which strips markdown fences before `JSON.parse` — must remain as the single point of JSON parsing across all providers
- **API Keys**: Must stay in `localStorage` only, under their respective keys. Never log, transmit, or hardcode them.

```js
// Storage key convention — do not rename these
nominarium_key_anthropic
nominarium_key_openai
nominarium_key_gemini
nominarium_key_deepseek
nominarium_history
```

### CSS / Design System

The Nominarium belongs to the **Music/Creative (Orange)** department of the DiegosDevStudio suite. The Phoenix Orange accent is the primary color throughout.

```css
/* Required tokens — do not rename or remove */
--bg: #0B0F19           /* Page background — Cinematic Midnight */
--orange: #FB923C       /* Primary accent — Phoenix Orange */
--cyan: #22D3EE         /* Secondary accent */
--blue: #2563EB         /* Tertiary accent */
--text: #F8FAFC         /* Body text */
--text-muted: #94A3B8   /* Secondary text */
```

Three design rules that must always be preserved:

1. **No light backgrounds** — `--bg: #0B0F19` is non-negotiable. Never introduce white, cream, or light-mode variants without an explicit feature branch and discussion.
2. **Preserve glassmorphism** — All cards and modals use `backdrop-filter: blur()` with semi-transparent backgrounds. Never replace with solid fills.
3. **Gradient buttons only** — All action buttons use a gradient from the active department accent. No flat or outline-only primary buttons.
4. **Powered-On Rule** — Every card and modal must include `border-t-2` in the department accent color (`--orange` or provider color). This is a hard brand rule.

### Animations

The following `@keyframes` must always be present and wired to `body::before` and `body::after`:

```css
@keyframes gridDrift   { /* background-position drift on body::before */ }
@keyframes nebulaDrift { /* transform scale/translate on body::after  */ }
```

Do not remove or rename these. They are part of the Cinematic Command Center aesthetic.

### JavaScript

- Vanilla JS only — no frameworks, no libraries, no build tools
- Use `async/await` for all async operations
- Always wrap `callAPI()` invocations in `try/catch`
- Keep `safeParseJSON()` as the single JSON parsing entry point
- Keep `callAPI()` as the single API dispatch function — add new providers inside it, do not create parallel fetch functions

---

## Submitting a Pull Request

1. Push your branch to your fork:
   ```bash
   git push origin feat/your-feature-name
   ```

2. Open a Pull Request against the `main` branch of the upstream repository

3. Fill in the PR template:
   - **What does this PR do?**
   - **Which provider(s) does it affect?**
   - **How was it tested?**
   - **Screenshots** (required for any visual changes)
   - **Related issue** (e.g. `Closes #12`)

4. A maintainer will review your PR within a few days. Be prepared for feedback — this is normal and healthy.

---

## Reporting Bugs

Before opening a bug report, please:
- Check that you're using a supported browser (Chrome, Firefox, or Edge)
- Confirm your API key for the active model is valid and has quota remaining
- Search [existing issues](../../issues) to avoid duplicates

When filing a bug, include:

```
**Browser & version:**
**Operating system:**
**Active model (Claude / GPT-4o / Gemini / DeepSeek):**
**Steps to reproduce:**
**Expected behavior:**
**Actual behavior:**
**Console errors (if any):**
```

---

## Feature Requests

Feature ideas are welcome! Open an issue with the `enhancement` label and describe:

- **The problem** you're trying to solve
- **Your proposed solution**
- **Alternatives you considered**

Current ideas on the roadmap (up for grabs):

- Share a generated identity via URL (encoded in hash)
- Copy individual identity card to clipboard
- Localization / multi-language support
- Grok API support as a DeepSeek alternative
- Per-model temperature/creativity slider in the settings modal
- Custom system prompt override field for power users

---

## Style Guide

### HTML
- Use semantic elements (`<section>`, `<nav>`, `<main>`, `<footer>`)
- Keep IDs kebab-case: `id="results-area"`
- Keep classes kebab-case: `class="identity-card"`

### CSS
- Add new design tokens to `:root` — never hardcode hex values inline
- Group properties: positioning → box model → typography → visual → animation
- Comment non-obvious selectors

### JavaScript
- Use `const` by default, `let` only when reassignment is needed
- Name functions with verbs: `renderCards()`, `selectModel()`, `showError()`
- Keep functions small and single-purpose
- Add a comment block above any new provider added to `callAPI()`

---

## Questions?

Open a [Discussion](../../discussions) or reach out via the issues tab. We're happy to help you get oriented.

**Built with obsession by [DiegosDev Studio](https://github.com/diegosdevstudio)** ⚡
