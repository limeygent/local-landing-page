# Local Landing Page (LLP) Builder

A Claude Code skill that generates city-level landing pages for local service businesses. An LLP is the page someone hits searching "[niche] [city]" (e.g., "plumber gotham", "house cleaner gotham") or from a Google Business Profile listing.

It lists all services briefly, builds geographic trust with real local research, and routes visitors to deeper service pages or to call/book.

**Not a service page** (deep single-service focus) and **not a homepage** (brand-only).

## What It Does

- Detects the niche archetype (emergency, planning, or hybrid) and adapts page structure accordingly
- Runs live city research via WebSearch for local codes, neighborhoods, climate factors, and demographics
- Selects from 20 content blocks based on archetype, modifiers, and available data
- Generates Bootstrap 5 HTML with brand-colored CSS custom properties
- Outputs WordPress-ready page content (no wrapper markup)

## Quick Start

```
/llp {client-slug} {city} {state}
/local-landing-page acme-plumbing gotham ny
```

Requires a client profile at `~/.claude/config/clients/{slug}/profile.json` with business name, niche, services, brand color, and phone number.

## Niche Archetypes

| Archetype | Niches | Behavior |
|-----------|--------|----------|
| **Emergency** | Plumbing, HVAC, electrical, locksmith, towing, restoration | Urgency-first: symptom router in hero, availability bar, emergency section, fast CTAs |
| **Planning** | Cleaning, financial, accounting, cosmetic dentist, landscaping | Research-friendly: service finder in hero, process/pricing blocks, deeper about section |
| **Hybrid** | General dentist, auto repair, pest control, roofing | Dual-path triage: hero routes users to emergency or planning flows |

## Page-Level Modifiers

Four binary modifiers refine output beyond the base archetype:

| Modifier | Effect |
|----------|--------|
| `stakes: high` | Deeper credentials, process blocks; sticky table of contents |
| `regulated: true` | Licensing/compliance block renders |
| `high_ticket: true` | Pricing block with ranges (not exact prices) |
| `recurring: true` | Plan pricing emphasis, consistency messaging |

## Content Blocks

20 blocks, each with defined WHEN conditions, required atomic facts, and HTML patterns:

LLP_HERO, LLP_TRUST_BAR, LLP_AVAILABILITY, LLP_MID_CTA, LLP_SERVICES_GRID, LLP_WHY_CHOOSE, LLP_PROCESS, LLP_PRICING, LLP_LICENSING_COMPLIANCE, LLP_MEET_THE_TEAM, LLP_ABOUT, LLP_LOCAL_KNOWLEDGE, LLP_NEIGHBORHOODS, LLP_REVIEWS, LLP_FAQ, LLP_GUARANTEE, LLP_RECENT_WORK, LLP_MAP_CONTACT, LLP_EMERGENCY_SECTION, LLP_FINAL_CTA

Blocks without sufficient real data are suppressed entirely (missing > generic).

## Key Features

- **Progressive CTAs**: CTA text evolves as the reader scrolls and accumulates trust, from intent-matching ("Call Now") through social proof ("Join 500+ homeowners") to closing arguments
- **Intent-driven ordering**: 3-layer intent analysis (observable, inferred, hidden drivers) determines block order and CTA language
- **Anti-slop rules**: Ban vague adjectives, require falsifiable claims, quantify or kill, suppress blocks lacking atomic facts
- **FAQ schema markup**: JSON-LD structured data on FAQ blocks
- **Live city research**: WebSearch queries for local codes, neighborhoods, climate, permits, and demographics

## File Structure

```
skill.md                              # Main skill definition (execution steps, rules)
references/
  block-catalog.md                    # All 20 blocks: WHEN conditions, content models, HTML patterns
  niche-archetypes.md                 # Archetype detection, block ordering, modifier logic
  local-research-guide.md             # WebSearch query templates per niche type
  tone-and-copy.md                    # Copy voice, CTA patterns, anti-slop rules
  examples/
    plumbing-emergency-example.html   # Emergency archetype reference (full BS5 HTML)
    cleaning-planning-example.txt     # Planning archetype reference (content structure)
```

## Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI
- A client profile directory at `~/.claude/config/clients/{slug}/` containing:
  - `profile.json` with `name`, `niche`, `services[]`, `brand_color`, `phone`
  - `background.md` (optional, for richer content generation)

## Installation

Clone into your Claude Code skills directory:

```bash
git clone https://github.com/limeygent/local-landing-page.git ~/.claude/skills/local-landing-page
```

The skill registers automatically via the `skill.md` frontmatter. Invoke with `/llp` or `/local-landing-page`.

## License

MIT
