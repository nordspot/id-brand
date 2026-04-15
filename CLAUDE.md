# CLAUDE.md — .brand Landing Page

## What This Project Is

This is the landing page for **.brand** — a new paradigm where brand identity files become MCP agents. It's a concept by Nord.spot (Daniel Kunz) × Brigade Studio (Nicolas Paupe). The live demo uses **SBB/CFF/FFS** (Swiss Federal Railways) as the proof of concept.

**Live URLs:**
- Primary: https://liquidbranding.pages.dev
- Legacy: https://id-brand.billowing-leaf-4d6a.workers.dev
- SBB Brand API: https://sbb-brand-api.billowing-leaf-4d6a.workers.dev/api

## Architecture & Key Concepts

### The .brand Concept
A .brand file is not a document — it's a living intelligence. An MCP agent that embodies a brand's identity, speaks to consumers directly, adapts to every audience, and learns from every interaction. The theoretical foundation builds on Irene van Nes' 6 typologies of dynamic identity, proposing a 7th: **Conscious Identity**.

### The 7-Layer Architecture (Nicolas Paupe)
1. **Core Intelligence** (Drift: Locked) — Vision, values, positioning, brand DNA. Immutable nucleus.
2. **Expression Engine** (Drift: Controlled) — Tone, visual language, narrative formats. AI operates within defined parameters.
3. **Context Adaptation** (Drift: Controlled) — Consumer typologies, cultural narratives, temporal context. Anthropological, sensory, neuro positioning.
4. **Interaction Layer** (Drift: Autonomous) — Real-time consumer-facing outputs. Every expression unique, every expression on-brand.
5. **System Network** (Drift: Controlled) — Agent-to-agent dialogue, output negotiation, cross-touchpoint synchronization.
6. **Governance** (Drift: Locked) — Human oversight, creative direction, ethics. Humans are custodians of meaning.
7. **Value Creation** (Drift: Autonomous) — Products, experiences, optimization loops, learning.

### Drift Control
Three tiers of freedom that define how much the AI can deviate:
- **Core (Locked):** AI cannot override. Human-defined, machine-enforced. Example: SBB #EB0000 is non-negotiable.
- **System (Controlled):** Adapts within defined parameters set by creative direction. Example: Bildwelt photography style, formal/informal address rules.
- **Expression (Autonomous):** Free to interpret, anchored by layers above. Example: Which image for Yuki vs. Lena, card layout, content order.

## Tech Stack

- **Single HTML file** (`public/index.html`) — ~1800 lines, HTML + CSS + JS, zero framework, zero build step
- **SBBWeb fonts** from `cdn.app.sbb.ch/fonts/`
- **SBB icon system** from `icons.app.sbb.ch/icons/{name}.svg`
- **8 static JPEG images** in `public/images/` — 800×300px, quality 82, scraped from SBB content DAM
- **Cloudflare Pages** for hosting — deploy with `npm run deploy`
- **wrangler.toml** — also configured as Cloudflare Worker (legacy deploy)

## How the Code Is Structured

Everything is in `public/index.html`. The structure is:

### CSS (~550 lines)
- SBB design tokens as CSS variables (--sbb-red, --sbb-black, etc.)
- Nav, hero, section layouts
- Typology cards, architecture layers with drift badges
- Phone mockup with screen, notch, tab bar
- 10+ visual expression modes: `vis-young`, `vis-premium`, `vis-compact`, `vis-senior`, `vis-dashboard`, `vis-discovery`, `vis-evening`, `vis-onboard`, `vis-activity`, `vis-family`, `vis-disruption`, `vis-weekend`
- Agent thinking overlay animation
- Alert banners, toast notifications, progress bars
- Annotations with color-coded tags (tone, content, product, typo, color, layout, context, drift)
- Responsive breakpoints at 1300px, 1100px, 900px, 600px

### HTML (~200 lines)
- Nav with live dot indicator
- Hero section
- The Idea (problem/solution cards + quote)
- Typologies (6 cards + 7th Conscious Identity)
- Architecture (7 interactive layers + Drift Control panel)
- Live Demo (persona strip + scenario strip + phone + annotations + reasoning)
- Competitive Landscape
- Roadmap
- Footer

### JavaScript (~700 lines)
- `personas` array — 12 personas, each with:
  - `id`, `name`, `icon`, `label`, `banner` (image or null)
  - `scenarios[]` — each scenario contains: vis config, from/to, info, title, offers, cta, section2, offers2, alert, toast, progress, annoLeft, annoRight, reasoning
  - `lang`, `tabs`
- `renderScenarioStrip()` — generates scenario chips for personas with multiple scenarios
- `transitionTo(persona, scenarioIdx)` — shows agent-thinking overlay, cycles status messages, then renders
- `render(persona, scenarioIdx)` — generates the full phone screen HTML + annotations + reasoning
- Architecture layer click interaction
- IntersectionObserver for scroll reveal

## SBB Brand Rules You Must Follow

### Color
- **SBB Red: #EB0000** — primary, non-negotiable. Used for red zone, CTAs, highlights, accent.
- **SBB Black: #000** — text, dark backgrounds
- **SBB Anthracite: #4C4C4C** — secondary text
- **SBB Milk: #F6F6F6** — light backgrounds
- **SBB Cloud: #E5E5E5** — borders, dividers
- Never use red for body text. Never use gradients on the logo.

### Typography
- **SBBWeb** font family (loaded from CDN). Weights: 100 (UltraLight), 200 (Thin), 300 (Light), 400 (Roman), 700 (Bold).
- Headlines: weight 200-300, large sizes, tight letter-spacing (-.03em to -.04em)
- Body: weight 300, 15-17px
- Section titles end with a period ("Für Sie.", "Pour toi.", "Per lei.")

### Tone of Voice by Persona
- **Under 30:** "tu" (FR), "du" (DE) — informal
- **Over 30 business/senior:** "Sie" (DE), "Lei" (IT), "vous" (FR) — formal
- **Tourists:** clear English, no Swiss abbreviations
- **Teenagers:** direct, no upsells, night-oriented content
- **Families:** warm, factual, budget-first
- **Executives:** formal, data-dense, no prices (GA holders)
- **Seniors:** calm pacing, heritage content, large text, no tech

### Bildwelt (Photography)
- Authentic, not staged. Warm but restrained. Switzerland-specific. Human scale.
- High contrast for text overlay. Red panel system: #EB0000 with multiply blend mode.
- Categories: Landscapes, Trains, People, Stations, Seasonal, Cultural.

## Personas Quick Reference

| ID | Name | Lang | Visual Mode | Key Feature |
|----|------|------|-------------|-------------|
| lena | Lena, 22 | FR | vis-young | 3 scenarios (commute/disruption/weekend) |
| thomas | Thomas, 54 | DE | vis-premium | 2 scenarios (commute/disruption with calendar sync) |
| yuki | Yuki, 31 | EN | vis-discovery | 2 scenarios (discovery/bad weather) |
| mueller | Familie Müller | DE | vis-family | 2 scenarios (outing/with toddler) |
| marco | Marco, 28 | DE | vis-dashboard | 2 scenarios (commute/late night hackathon) |
| isabelle | Isabelle, 67 | IT | vis-senior | Day trip |
| ahmed | Ahmed, 35 | EN | vis-onboard | 2 scenarios (onboarding/3 months later learning loop) |
| sophie | Sophie, 17 | FR | vis-evening | Night out |
| reto | Reto, 42 | DE | vis-activity | Bike tour |
| chen | Chen Wei, 45 | EN | vis-premium | Airport arrival VIP |
| petra | Petra, 38 | DE | vis-compact | Morning commute |
| luigi | Luigi, 72 | IT | vis-senior | Morning ritual |

## Common Tasks

### Add a new persona
1. Add an entry to the `personas` array in the `<script>` section
2. Include at least one scenario with: vis config, from/to, info, title, offers (3), cta, section2, offers2 (1), annoLeft (3), annoRight (3), reasoning
3. Set the visual mode class (`vis-*`) — reuse an existing one or create new CSS

### Add a new scenario to an existing persona
1. Find the persona in the `personas` array
2. Add a new object to their `scenarios[]` array
3. Include a unique `id`, `name`, `color` (for the chip dot)
4. Fill in all the same fields as other scenarios
5. The scenario strip auto-renders when a persona has >1 scenario

### Add a new visual expression mode
1. Add CSS rules prefixed with `.vis-newmode` targeting `.sbb-section-title`, `.sbb-offer-card`, etc.
2. Reference it in a persona scenario's `vis.cls` field

### Add a new annotation tag
1. Add CSS for `.anno-tag.newtag` with background and color
2. Use `{tag:'newtag',cat:'Display Name',text:'...'}`

### Add interactive elements to a scenario
- `alert`: `{text:'<strong>Bold</strong> rest of text'}` — red alert banner at top
- `toast`: `{icon:'icon-name',text:'<strong>Bold</strong> text'}` — dark notification bar
- `progress`: `{label:'Label',value:75}` — progress bar with percentage

### Deploy
```bash
npm run deploy
```

### Local dev
```bash
npm run dev
# http://localhost:8788
```

## Image Naming Convention
`{persona-name}-{location}.jpg` — e.g., `lena-lausanne.jpg`, `yuki-alps.jpg`
All images are 800×300px, JPEG quality 82, center-cropped from SBB source photography.

## What NOT To Do
- Don't add a build step or framework — this is intentionally a single file
- Don't change SBB Red (#EB0000) — it's the locked core of the brand
- Don't remove the SBBWeb font or replace with system fonts
- Don't add external JS libraries — everything is vanilla
- Don't break the persona/scenario data structure — the render function depends on it
- Don't remove annotations — they're the educational layer that explains what the agent does
- Don't commit .env files or API keys
