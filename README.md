# .brand — When the Brand Becomes the Agent

**A concept by [Nord.spot](https://nord.spot) × [Brigade Studio](https://brigade.studio)**

.brand is a new paradigm: brand identity files that are MCP agents. Not PDFs. Not Figma libraries. Living intelligence that embodies a brand, speaks to consumers directly, adapts to every audience, and learns from every interaction.

**Live:** https://liquidbranding.pages.dev  
**SBB API:** https://sbb-brand-api.billowing-leaf-4d6a.workers.dev/api  
**Proof of concept:** SBB/CFF/FFS (Swiss Federal Railways)

---

## What this is

A single-page landing page that demonstrates the .brand concept using SBB as the test case. The page includes:

- **Concept section** — the shift from static guidelines to living brand agents
- **Theoretical foundation** — the 7th typology of dynamic identity (building on Irene van Nes)
- **7-layer architecture** (Nicolas Paupe) — interactive, with Drift Control visualization
- **Live demo** — 12 personas × multiple scenarios, each generating a completely different SBB mobile app experience from the same brand rules
- **Competitive landscape** and roadmap

## The 7-Layer .brand Architecture

| # | Layer | Drift Control | Description |
|---|-------|--------------|-------------|
| 1 | Core Intelligence | Locked | Vision, values, positioning, brand DNA. Immutable. |
| 2 | Expression Engine | Controlled | Tone, visual language, narrative formats, sensory palette. |
| 3 | Context Adaptation | Controlled | Consumer typologies, cultural narratives, temporal context. |
| 4 | Interaction Layer | Autonomous | Real-time consumer-facing outputs. Every expression unique. |
| 5 | System Network | Controlled | Agent-to-agent dialogue, cross-touchpoint sync. |
| 6 | Governance | Locked | Human oversight, creative direction, ethics, data governance. |
| 7 | Value Creation | Autonomous | Products, experiences, optimization loops. |

**Drift Control** defines freedom levels: Core (locked — AI cannot override), System (controlled — adapts within parameters), Expression (autonomous — free to interpret, anchored by layers above).

## Personas & Scenarios

The demo has 12 personas, several with multiple scenarios that demonstrate how the same persona gets different content based on context:

| Persona | Language | Scenarios |
|---------|----------|-----------|
| Lena, 22 (Student, Lausanne) | FR | Morning commute · Disruption · Weekend |
| Thomas, 54 (Executive, Bern) | DE | Morning commute · Disruption |
| Yuki, 31 (Tourist, Tokyo) | EN | Discovery · Bad weather |
| Familie Müller (Family, Luzern) | DE | Family outing · With toddler |
| Marco, 28 (Tech, Zürich) | DE | Morning commute · Late night |
| Isabelle, 67 (Retiree, Bellinzona) | IT | Day trip |
| Ahmed, 35 (Expat, Geneva) | EN | Onboarding · 3 months later |
| Sophie, 17 (Teenager, Biel) | FR | Night out |
| Reto, 42 (Cyclist, Thun) | DE | Bike tour |
| Chen Wei, 45 (VIP, Davos) | EN | Airport arrival |
| Petra, 38 (Commuter, Winterthur) | DE | Morning commute |
| Luigi, 72 (Pensioner, Lugano) | IT | Morning ritual |

Each scenario changes: content, layout, tone, visual expression, annotations, and agent reasoning.

## Tech Stack

- **Single HTML file** — `public/index.html` (~1800 lines, zero dependencies, zero build step)
- **SBB Web fonts** — loaded from `cdn.app.sbb.ch`
- **SBB icon system** — loaded from `icons.app.sbb.ch`
- **Static images** — 8 JPEG photographs (800×300, q82) scraped from SBB content DAM
- **Hosting** — Cloudflare Pages (static assets)
- **Companion API** — Cloudflare Worker at `sbb-brand-api.billowing-leaf-4d6a.workers.dev`

## Local Development

```bash
npm install
npm run dev
# Opens at http://localhost:8788
```

## Deployment

```bash
# Cloudflare Pages (primary — liquidbranding.pages.dev)
npm run deploy

# Legacy Cloudflare Worker (id-brand.billowing-leaf-4d6a.workers.dev)
npm run deploy:worker
```

Requires `CLOUDFLARE_API_KEY` and `CLOUDFLARE_EMAIL` env vars, or `CLOUDFLARE_API_TOKEN`.

## Project Structure

```
liquidbranding/
├── public/
│   ├── index.html          # The entire landing page (HTML + CSS + JS)
│   └── images/
│       ├── lena-lausanne.jpg
│       ├── yuki-alps.jpg
│       ├── family-engelberg.jpg
│       ├── isabelle-ticino.jpg
│       ├── sophie-bern-night.jpg
│       ├── reto-thunersee.jpg
│       ├── hans-davos.jpg
│       └── lucia-lugano.jpg
├── .github/
│   └── workflows/
│       └── deploy.yml      # Auto-deploy on push to main
├── wrangler.toml            # Cloudflare Worker config
├── package.json
├── CLAUDE.md                # Prompt for Claude Code
└── README.md
```

## Key Design Decisions

- **Single file** — Everything in one HTML file. No framework, no build, no dependencies. This is a concept demo, not a production app. It should be instantly inspectable, forkable, and understandable.
- **SBB as test case** — Swiss Federal Railways has a rich, well-documented brand system with 4 languages, strict color rules (#EB0000), detailed photography guidelines (Bildwelt), and a wide range of customer segments. Perfect for demonstrating adaptive brand intelligence.
- **Real SBB images** — Not stock photography. Images scraped from SBB's content DAM following their Bildwelt guidelines (authentic, warm, Swiss, human scale).
- **Agent thinking animation** — When switching personas/scenarios, a thinking overlay shows the .brand agent "processing" — reinforces that this is intelligence, not templates.
- **Annotations** — Left and right columns explain what the agent is doing and why, using categorized tags (Tone, Content, Product, Typography, Color, Layout, Context, Drift).

## References

- Irene van Nes, *Dynamic Identities* — the 6 typologies of dynamic identity
- Alina Wheeler, *Designing Brand Identity* (5th ed., 2018) — brand governance, architecture, ideals
- Nicolas Paupe (Brigade Studio) — 7-layer .brand architecture, Drift Control, meaning systems
- SBB Brand Guidelines — Bildwelt, typography, color system, tone of voice

## Authors

- **Daniel Kunz** — Nord.spot (concept, product, engineering)
- **Nicolas Paupe** — Brigade Studio (brand architecture, theory, creative direction)

Fribourg, 2026
