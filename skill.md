---
name: local-landing-page
description: "Builds local landing pages (LLPs) for service businesses - the city-level hub page for [niche] [city] searches or GBP listings. Generates Bootstrap 5 HTML with niche-adaptive structure (emergency vs planning vs hybrid archetypes), live city research, and brand-colored layouts. Use when creating city pages, location pages, or geo landing pages. Triggers: /llp, /local-landing-page, build a city page, create a location page."
---

# Local Landing Page (LLP) Builder

Build city-level hub pages for local service businesses. An LLP is the page someone hits searching "[niche] [city]" or from a Google Business Profile listing. It lists all services briefly, builds geographic trust, and routes visitors to deeper service pages.

**NOT a service page** (deep single-service) and **NOT a homepage** (brand-only).

## Quick Start

```
/llp {client-slug} {city} {state}
/local-landing-page acme-plumbing gotham ny
```

## Execution Steps

### Step 1: Load Client Context

1. Read `~/.claude/config/clients/{slug}/profile.json`
2. Read `~/.claude/config/clients/{slug}/background.md` (if exists)
3. Validate required fields exist: `name`, `niche`, `services[]`
4. Extract: `brand_color`, `phone`, `business_name`, `audience`, `review_count`, `avg_rating`, `license_numbers`, `gbp_url`
5. Determine niche archetype — see `references/niche-archetypes.md`
6. Ask user for any missing critical info (phone, services list)

### Step 2: Intent Analysis

Run the 3-layer intent model for the query `"[niche] [city]"`:

**Layer 1 — Observable (literal query):** The keyword itself determines base archetype. "Emergency plumber Gotham TX" = emergency. "Kitchen remodel Gotham TX" = planning. "Dentist Gotham TX" = hybrid.

**Layer 2 — Inferred intent:** Classify as informational / commercial / transactional. This controls block depth — transactional = shorter, action-forward; informational = deeper PROCESS and CREDENTIALS blocks.

**Layer 3 — Hidden drivers:**
- Emotional: fear, hope, uncertainty, urgency
- Functional: problem resolution, decision support, resource optimization

Layer 3 output determines:
- Block ordering emphasis (fear-driven = REVIEWS and GUARANTEE early; hope-driven = RECENT_WORK and MEET_THE_TEAM early)
- CTA language (urgency = imperative "Call Now"; uncertainty = low-pressure "No obligation quote")
- Which trust signals to front-load in TRUST_BAR

### Step 3: Determine Page-Level Modifiers

After archetype detection, set 4 binary modifiers:

| Modifier | Values | Examples |
|----------|--------|---------|
| `stakes` | low / high | house cleaner = low; cosmetic dentist = high |
| `regulated` | true / false | trades, medical, financial, legal = true |
| `high_ticket` | true / false | roofing, remodels, cosmetic dentistry = true |
| `recurring` | true / false | cleaning plans, pest control, lawn care = true |

**How modifiers affect output:**
- `stakes: high` — deeper CREDENTIALS, CASE_STUDIES, PROCESS blocks; add sticky table of contents
- `regulated: true` — LICENSING_COMPLIANCE block renders
- `high_ticket: true` — PRICING block renders with ranges (not exact prices)
- `recurring: true` — plan pricing emphasis, consistency messaging in copy

### Step 4: Parse Optional Parameters

Check if user provided overrides:
- `--archetype emergency|planning|hybrid` — override auto-detection
- `--services-urls '{name: url, ...}'` — service page links for grid
- `--neighborhoods 'Area1, Area2, Area3'` — skip neighborhood research
- `--map-embed 'https://...'` — Google Maps embed URL
- `--booking-widget '<button ...>'` — booking widget HTML snippet

### Step 5: City Research (WebSearch)

Execute 4-6 parallel WebSearches for city-specific content. See `references/local-research-guide.md` for query templates per niche.

**Emergency/Hybrid archetype queries:**
1. `"{city} {state} {niche} building codes requirements"` — codes/compliance
2. `"{city} {state} neighborhoods areas communities"` — neighborhood names
3. `"{city} {state} common {niche} problems issues"` — local issues
4. `"{city} {state} climate soil water quality"` — environmental factors
5. `"{city} {state} permit requirements {niche}"` — permit info
6. `"{city} {state} zip codes population"` — demographics

**Planning archetype queries:**
1. `"{city} {state} neighborhoods communities areas"` — neighborhood names
2. `"{city} {state} demographics population"` — city overview
3. `"{city} {state} {niche} common needs challenges"` — local issues
4. `"{city} {state} zip codes service areas"` — zip codes
5. `"{city} {state} climate seasonal factors"` — seasonal considerations
6. `"{city} {state} {niche} regulations licensing"` — if regulated industry

Skip queries where user provided explicit data.

### Step 6: Block Selection

Read `references/block-catalog.md` and evaluate WHEN conditions for each block against:
- Niche archetype (emergency / planning / hybrid)
- Page-level modifiers from Step 3
- Client capabilities from profile
- Research findings from Step 5
- Trust signals available (reviews, years in business)
- Intent analysis output from Step 2

**Anti-slop rule:** If a block's required atomic facts cannot be populated with real, specific, verifiable data for this business, suppress the block entirely. A missing block is less damaging than a generic one.

### Step 7: Generate Bootstrap 5 HTML

Read `references/niche-archetypes.md` for block ordering by archetype.

For each selected block, generate HTML following the patterns in `references/block-catalog.md`:

1. **`<style>` block** — CSS custom properties from `brand_color`:
   - `--llp-primary`: brand color
   - `--llp-primary-dark`: darkened variant
   - `--llp-accent`: accent/CTA color
   - `--llp-light`: light background
   - `--llp-dark`: dark text
   - Branded button classes, utility classes
   - `.zone-group`, `.icon-circle`, `.step-number`, `.card-hover`

2. **Block HTML** — Each block wrapped in `<section>` with:
   - HTML comment header marking the section
   - Unique `id` attribute for anchor navigation
   - `zone-group` class for scroll-margin
   - Bootstrap 5 grid (container > row > col)
   - Bootstrap Icons for iconography
   - City name woven into H2s naturally (not every heading)

3. **Hero** — Full-bleed via `margin-left: calc(-50vw + 50%)` pattern
   - Background image with gradient overlay
   - H1, value prop, trust badges, dual CTAs
   - Right column: symptom router (emergency) or service finder (planning)
   - CTA matches dominant intent (see Progressive CTA system)

4. **Service grid** — Cards with images linking to provided URLs or `#`

5. **CTAs** — Phone link (`tel:`) + booking widget or "Book Online" button

6. **FAQ block** — Implement FAQ structured data (JSON-LD schema) for SEO

7. **Sticky TOC** — If `stakes: high`, render slim sticky table of contents after hero

### Step 8: Assemble and Output

1. Concatenate `<style>` block + all section blocks in archetype order
2. Wrap in `<main>` tag
3. Output complete HTML
4. Print summary: blocks included, modifiers applied, research findings used, any placeholders remaining

## Progressive CTA System

CTAs must evolve as the reader scrolls and accumulates trust. Never use the same CTA text top-to-bottom.

| Position | Reader State | CTA Strategy | Example |
|----------|-------------|--------------|---------|
| Hero | Just arrived, zero trust | Match dominant intent | Emergency: "Call Now". Planning: "Get Free Quote" |
| After SERVICES_GRID | Knows scope | Service-specific action | "Get Quote for [popular service]" |
| LLP_MID_CTA bar | Has differentiation + some trust | Social proof CTA | "Join 500+ [City] homeowners" |
| After REVIEWS | Seen peer validation | Address remaining objection | "No obligation, no pressure" |
| FINAL_CTA | Consumed everything | Closing argument referencing what they learned | "Ready for [specific benefit] in [City]?" |

**LLP_MID_CTA block:** Slim full-width inline CTA bar (similar to AVAILABILITY), placed around block 6-7. Render for Emergency and Hybrid archetypes. Contains: one trust proof point + one low-friction CTA.

## Block Catalog Summary

Full specs in `references/block-catalog.md`. Current blocks:

**Core blocks:** LLP_HERO, LLP_TRUST_BAR, LLP_AVAILABILITY, LLP_MID_CTA, LLP_SERVICES_GRID, LLP_WHY_CHOOSE, LLP_PROCESS, LLP_PRICING, LLP_LICENSING_COMPLIANCE, LLP_MEET_THE_TEAM, LLP_ABOUT, LLP_LOCAL_KNOWLEDGE, LLP_NEIGHBORHOODS, LLP_REVIEWS, LLP_FAQ, LLP_GUARANTEE, LLP_RECENT_WORK, LLP_MAP_CONTACT, LLP_EMERGENCY_SECTION, LLP_FINAL_CTA

**Merged blocks (do not use old names):**
- `LLP_CODES_COMPLIANCE` + `LLP_PERMITS_INSPECTIONS` + `LLP_CREDENTIALS` → `LLP_LICENSING_COMPLIANCE`
- `LLP_DIRECTIONS` → absorbed into `LLP_MAP_CONTACT`
- `LLP_SERVICE_APPROACH` → renamed to `LLP_PROCESS`

**Killed blocks:** LLP_AWARDS (badges move to TRUST_BAR, narratives move to WHY_CHOOSE), LLP_DIRECTIONS

## Anti-Slop Content Rules

1. **Block suppression over generic content** — if a block's required atomic facts cannot be populated with real, specific, verifiable data, suppress the block. A missing block is less damaging than a generic one.
2. **Ban vague adjectives** — "best", "quality", "professional" are forbidden without supporting evidence (number, award, named entity, policy).
3. **Landmark and Local Code Rule** — every page needs 2+ specific local references (street names, landmarks, local code numbers, named neighborhoods).
4. **Quantify or Kill** — every claim needs a number, policy, named entity, or timeline. "We respond fast" = kill it. "We respond within 90 minutes" = keep it.
5. **Every claim must be falsifiable** — if the claim could appear on any competitor's page without changing a word, rewrite or remove it.

## Critical Rules

1. **Bootstrap 5 only** — All layouts use BS5 grid, utilities, and components
2. **Bootstrap Icons** — `<i class="bi bi-*">` for all icons
3. **Niche-adaptive** — Structure changes based on archetype, not one-size-fits-all
4. **City-specific content** — LOCAL_KNOWLEDGE, LICENSING_COMPLIANCE, NEIGHBORHOODS must contain real researched data, not generic filler
5. **No forced city stuffing** — City name in H2s where natural, not crammed into every sentence
6. **Service grid links OUT** — Cards link to deeper service pages, not to sections within the LLP (unless no URLs provided)
7. **Brand colors from profile** — CSS custom properties, not hardcoded hex values
8. **Full-bleed hero** — Uses `calc(-50vw + 50%)` margin trick for container breakout
9. **Mobile-first responsive** — col-12 base, col-md-6, col-lg-4 for grids
10. **HTML comments** — Mark each section with `<!-- SECTION_NAME -->` comments
11. **No em-dashes** — Use colons, commas, periods, or parentheses instead
12. **Neighborhood-tagged reviews** — Reviews should reference specific neighborhoods/areas
13. **Accessible** — Proper heading hierarchy, alt text, aria labels on interactive elements
14. **WordPress-ready** — Output is page content HTML only (no `<html>`, `<head>`, `<body>` wrapper)
15. **Progressive CTAs** — CTA text and tone must evolve as reader scrolls; never repeat the same CTA verbatim top-to-bottom
16. **FAQ schema markup** — Implement FAQ structured data (JSON-LD) whenever LLP_FAQ block is rendered
17. **Anchor navigation** — For `stakes: high` modifier, render a sticky slim table of contents after the hero

## Reference Files

Load these as needed during execution:

- **references/block-catalog.md** — All LLP blocks with WHEN conditions, content models, HTML patterns
- **references/niche-archetypes.md** — Archetype definitions, auto-detection, block ordering
- **references/local-research-guide.md** — WebSearch query templates per niche
- **references/tone-and-copy.md** — Copy voice, CTA patterns, anti-patterns
- **references/examples/** — Complete worked examples per archetype
