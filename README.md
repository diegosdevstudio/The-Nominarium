# 🔥 The Nominarium — AI Brand Identity Engine

> *Forge premium brand names from four precision vectors and a multi-model AI engine.*

The Nominarium is a high-end, single-file brand naming and identity tool built by **DiegosDev Studio**. It transforms strategic briefs into curated brand identities — complete with names, brand philosophies, and visual palettes — using your choice of four AI model specialists. Part of the DiegosDevStudio luxury app suite.

---

## ✨ Key Features

- **4-Vector Parameter System** — Structured input across Entity, Identity, Conceptual Vectors, and Constraint Parameters for precision-guided naming
- **Multi-Model AI Router** — Switch between Claude 3.5 Sonnet, GPT-4o, Gemini 1.5 Pro, and DeepSeek/Grok from a live nav dropdown; each model has a specialist role
- **Smart Default** — Claude 3.5 Sonnet pre-selected as the Creative Historian, the ideal specialist for naming and brand storytelling
- **Dynamic Forge Button** — Button label and gradient shift to reflect the active model engine in real time
- **6 Luxury Essence Chips** — Clickable signature tags (Heritage, Avant-Garde, Minimalist, Sustainable, Disruptive, Bespoke) injected directly into the AI prompt
- **Identity Cards** — Results render as glassmorphic cards with the brand name, Soul philosophy line, HEX color swatches, and texture descriptors
- **Download PDF** — Clean white-page brand identity report generated via `window.print()` with print-only CSS
- **History Tab** — Up to 30 past sessions persisted in `localStorage`, each collapsible with per-session PDF export and individual/bulk deletion; model used is logged per session
- **Phoenix Orange Aesthetic** — Powered-On `border-t-2` rule applied to all cards and modals; Music/Creative department accent color throughout
- **Zero Dependencies** — Pure HTML, CSS, and vanilla JS. No build system, no npm, no frameworks

---

## 🏗 Technical Architecture

### AI Model Router

| # | Provider | Model | Specialist Role | Dept. Color |
|---|---|---|---|---|
| 1 | Anthropic | `claude-3-5-sonnet-20241022` | Creative Historian | Orange `#FB923C` |
| 2 | OpenAI | `gpt-4o` | Logic Expert | Emerald `#10B981` |
| 3 | Google | `gemini-1.5-pro` | Visual Architect | Cyan `#22D3EE` |
| 4 | DeepSeek | `deepseek-chat` | Pro Manipulator | Indigo `#818CF8` |

### Design System

| Token | Value | Usage |
|---|---|---|
| `--bg` | `#0B0F19` | Page background |
| `--orange` | `#FB923C` | Primary accent — Phoenix Orange |
| `--cyan` | `#22D3EE` | Secondary accent |
| `--blue` | `#2563EB` | Tertiary accent |
| `--text` | `#F8FAFC` | Body text |
| `--text-muted` | `#94A3B8` | Secondary text |

- **Glassmorphism** — All cards use `backdrop-filter: blur()` with semi-transparent backgrounds
- **Powered-On Rule** — Every card and modal uses `border-t-2` in the department accent color
- **Animations** — `@keyframes gridDrift` and `@keyframes nebulaDrift` run persistently on the page background
- **Typography** — Outfit (display/UI), Rajdhani (labels/headings), Space Mono (mono/badges)

### Security & Storage

- All API keys are stored exclusively in `localStorage` — never logged, transmitted, or hardcoded
- Each provider key is stored under its own key: `nominarium_key_anthropic`, `nominarium_key_openai`, `nominarium_key_gemini`, `nominarium_key_deepseek`
- Session history stored under `nominarium_history` (max 30 sessions, FIFO)

### Performance

- Single-file architecture — zero network requests beyond Google Fonts and the active AI API
- All rendering is synchronous DOM injection — no virtual DOM, no re-renders
- Retry logic: 3 attempts, 2-second delay on 429 responses, per provider

---

## 🚀 Quick Start

1. Download `nominarium.html`
2. Open it directly in Chrome, Firefox, or Edge (no server needed)
3. Click **API Keys** in the top-right and add your key for the desired model
4. Select your active model from the **Model Engine** dropdown in the nav
5. Fill in the 4-Vector Parameter brief
6. Select any Luxury Essence chips
7. Click **Forge with Claude** (or whichever engine is active)

---

## 📄 License

MIT — see `LICENSE` for details.

---

## 👤 Author

**DiegosDev Studio**
Built with obsession. Part of a growing suite of luxury AI-powered web tools.
[github.com/diegosdevstudio](https://github.com/diegosdevstudio)
