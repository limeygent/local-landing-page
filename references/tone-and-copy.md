# Tone and Copy Guidelines

Voice, CTA patterns, and anti-patterns for Local Landing Pages.

## Voice

### Emergency Archetype
- **Confident and direct.** These people need help. Don't waste their time with fluff.
- Factual: use numbers, stats, license numbers, response times
- Action-oriented: every section should guide toward calling or booking
- Technically competent: demonstrate knowledge of codes, systems, methods
- Reassuring but not salesy: "We handle permits so you don't have to" vs "CALL NOW FOR AMAZING SERVICE"

### Planning Archetype
- **Warm and professional.** These people are comparing options. Build rapport.
- Conversational: "Most cleaning companies promise the world and deliver mediocre results. We do it differently."
- Community-connected: reference specific neighborhoods, local knowledge
- Results-focused: "Over 500 happy homeowners" vs "We are the best"
- Honest differentiators: explain what actually makes you different, not generic claims

### Hybrid Archetype
- Blend both voices. Emergency sections are direct and fast. Planning sections are warmer and more detailed.

---

## Intent-Driven Copy

The intent analyzer's 3-layer model determines copy tone within blocks:

**Layer 3 (Hidden Intent) → Copy Focus:**

| Emotional Driver | Copy Should... | Example |
|---|---|---|
| Fear (cost) | Lead with transparency, show value | "Upfront quotes before any work begins. No surprise fees, ever." |
| Fear (wrong choice) | Lead with proof and credentials | "Board-certified with 15 years and 2,000+ procedures in {City}" |
| Fear (safety/stranger) | Lead with vetting and accountability | "All team members are background-checked, uniformed, and insured" |
| Hope (improvement) | Lead with outcomes and transformation | "See the difference a professional clean makes" |
| Uncertainty (confusion) | Lead with clarity and process | "Here's exactly what happens when you call us" |
| Urgency (crisis) | Lead with availability and speed | "Licensed technician on the way. Average arrival: 45 minutes." |

**Functional Drivers → Content Structure:**

| Driver | Structure |
|---|---|
| Problem Resolution | Problem → Solution → Proof pattern in every block |
| Decision Support | Comparison elements, pros/cons, "best fit / not best fit" |
| Resource Optimization | Pricing transparency, value framing, savings calculations |

---

## H1 Patterns

### Emergency
- "{City}'s Experienced, Affordable {Niche Title}"
- "Licensed {Niche Title} Serving {City}, {State}"
- "{Niche Title} in {City}: Fast, Honest, Licensed"

### Planning
- "House Cleaners in {City}, {State} — {Business Name}"
- "{Business Name}: {Niche} in {City}"
- "Trusted {Niche} for {City} {Audience}"

---

## H2 Patterns

City name should appear in roughly 40-60% of H2s. Not every one.

**Good H2s:**
- "Plumbing Services in Gotham"
- "What Gotham Homeowners Say"
- "Areas We Serve in Gotham"
- "Permits & Inspections in Gotham"

**Also good (no city, natural):**
- "How it works"
- "Why permits matter"
- "Our Service Approach"

**Bad (forced):**
- "Gotham Plumbing Gotham Services for Gotham Homes"
- "Why Choose Us for Gotham"

---

## CTA Patterns

### Phone CTAs
```html
<a href="tel:+1{phone_digits}" class="btn btn-llp-primary btn-lg fw-semibold">
  <i class="bi bi-telephone me-2"></i>{cta_text}
</a>
```

**Emergency CTA text:** "Call Today", "Call for Help", "Get Help in {City}"
**Planning CTA text:** "Call for Quote", "Call (XXX) XXX-XXXX"

### Booking CTAs
```html
<a href="{booking_url}" class="btn btn-outline-llp-primary btn-lg">
  <i class="bi bi-calendar-check me-2"></i>{cta_text}
</a>
```

Or booking widget HTML if provided:
```html
<button data-token="{token}" data-orgname="{org}" class="hcp-button btn btn-lg px-4"
  onClick="HCPWidget.openModal()">
  <i class="bi bi-calendar-check me-2"></i>BOOK ONLINE
</button>
```

**Emergency booking text:** "BOOK ONLINE", "BOOK URGENT SERVICE", "Schedule Service"
**Planning booking text:** "Get Free Quote", "Book Consultation", "Schedule Online"

### CTA Frequency
- Emergency: CTA every 2-3 sections (high frequency)
- Planning: CTA every 3-4 sections (moderate frequency)
- Always dual CTA in hero and final CTA
- Single CTA (phone or book, not both) between sections

---

## Progressive CTA Strategy

CTAs must NOT be identical throughout the page. They should evolve as the reader accumulates trust and information:

**Stage 1: Intent Match (Hero)**
Reader has zero trust. CTA matches their dominant search intent.
- Emergency: "Call Now: (XXX) XXX-XXXX" or "Get Help in {City}"
- Planning: "Get Your Free Quote" or "Book a Consultation"
- Hybrid: Dual-path: "Need Help Now?" + "Planning a Project?"

**Stage 2: Service-Specific (After Services Grid)**
Reader now knows what you do. CTA narrows to their likely need.
- "Get a Quote for [Most Popular Service]"
- "Need [Specific Service]? Call Today"
- "Book Your [Service] Appointment"

**Stage 3: Social Proof (Mid-Page CTA Bar)**
Reader has seen differentiation and some proof. CTA leverages that.
- "Join 500+ {City} homeowners who trust us"
- "Trusted by {City} families since {year}"
- "{X} 5-star reviews and counting"

**Stage 4: Objection Handling (After Reviews)**
Reader has seen peer validation. CTA addresses the remaining barrier.
- "No obligation, no pressure, no spam"
- "Free quote in under 2 hours"
- "See why {City} homeowners keep coming back"

**Stage 5: Closing Argument (Final CTA)**
Reader has consumed everything. CTA references what they've learned.
- "Ready for [specific benefit the page demonstrated] in {City}?"
- NOT generic "Contact Us Today"
- Must reference a specific value prop from the page content

---

## Anti-Patterns

### Signals That HURT Conversion (LLM Council consensus, GPT-4.1 + Gemini 2.5 Pro + Claude Sonnet 4 + Grok 3)

**Emergency archetype: avoid these**
- Detailed project galleries or about-us stories above the fold (they need help, not your life story)
- Pricing tables with specific numbers (too variable, creates anxiety)
- Long educational content before the first CTA
- Any friction between the visitor and the phone number

**Planning archetype: avoid these**
- Countdown timers or "Only 2 slots left!" fake urgency (cheapens the service, undermines trust for long-term relationships)
- Emergency language when the service isn't urgent (makes you seem expensive/overkill)
- Hiding prices for predictable services (comparison shoppers need ranges)
- Generic stock team photos (worse than no team photos)

**Hybrid archetype: avoid these**
- Aggressive discount offers for first-time patients/customers ("50% OFF" signals low quality)
- Mixing emergency and planning tone in the same section

### Never Do
- **Em-dashes (—)** — AI writing tell. Use colons, commas, periods, or parentheses.
- **"Nestled in"** — cliche geo writing
- **"Look no further"** — cliche CTA
- **"State-of-the-art"** — meaningless
- **"Our team of experts"** — unverifiable claim (use specific credentials instead)
- **"Best in {City}"** — superlative claims without proof
- **"Don't wait!"** — pushy urgency (let the situation create urgency)
- **"We pride ourselves on..."** — self-congratulatory filler
- **Generic service descriptions** — every card should be specific to what THIS business actually does

### Regulated Industries (Dental, Legal, Financial)
- No "specialist" or "expert" unless legally qualified
- No guaranteed outcomes or warranties on clinical results
- No "painless" or minimising language
- Include required disclaimers and registration numbers
- See AHPRA/ACCC guidelines for dental (stored in memory)

### Geographic Claims
- "For patients/customers from {City}" NOT "in {City}" (unless physically located there)
- Don't imply local presence if the business is elsewhere
- If multi-location, be transparent about which location serves this city

---

## Anti-Slop Content Rules

Every block must contain atomic facts: specific, verifiable data points. Generic claims without evidence must not appear.

**Three Core Rules:**

1. **Ban Vague Adjectives** — "best", "quality", "professional", "experienced", "trusted" are FORBIDDEN as standalone claims. Replace with verifiable specifics:
   - Instead of: "We provide high-quality service"
   - Use: "We provide a 2-year warranty on all parts and labor"
   - Instead of: "Our experienced team"
   - Use: "Our 5 lead technicians average 12 years in the trade"

2. **Landmark & Local Code Rule** — Every page must contain at least 2 specific local references:
   - One geographical tie-in: "Our office is 10 minutes from [landmark]" or "We specialize in homes near [local feature]"
   - One verifiable local fact: "All work compliant with [specific code]" or "We handle permit applications with [city department name]"

3. **Quantify or Kill** — Every claim of superiority must be backed by a number, policy, named entity, or timeline:
   - Instead of: "We have a great team"
   - Use: "Our 5 lead technicians have an average of 12 years of experience"
   - Instead of: "Fast response times"
   - Use: "Average 47-minute response time in [City] (tracked over last 90 days)"

**Falsifiability Test:** Every differentiator must have a mechanism. Not "we arrive on time" but "we arrive on time because we only book 6 jobs per tech per day, not 10."

**Block Suppression Rule:** If a block's required atomic facts cannot be populated with real data, suppress the block entirely. A missing block is less damaging than a generic one.

---

## Content Depth per Block

| Block | Word Count | Depth |
|-------|-----------|-------|
| HERO | 50-80 | Punchy, value prop only |
| TRUST_BAR | 30-50 | Labels + one-liners |
| EMERGENCY_SECTION | 100-150 | Scenarios + checklist |
| SERVICES_GRID | 15-25 per card | One-sentence descriptions |
| WHY_CHOOSE | 100-150 | 4 differentiators with brief explanation |
| ABOUT | 80-120 | Story paragraphs |
| PROCESS | 80-100 | 3 methodology points |
| LOCAL_KNOWLEDGE | 150-250 | Data-rich, stats, specifics |
| LICENSING_COMPLIANCE | 200-400 | Detailed, factual — combines codes, permits, credentials |
| NEIGHBORHOODS | 80-120 | Brief per neighborhood |
| REVIEWS | 50-80 per review | Quotes with attribution |
| RECENT_WORK | 40-60 per case | Brief outcome stories |
| PRICING | 80-120 | Ranges, inclusions, what affects cost |
| FAQ | 40-60 per answer | 5-8 questions, collapsible format |
| GUARANTEE | 60-100 | Specific policy, not vague assurance |
| MID_CTA | 20-30 | Social proof hook + single action |
| MAP_CONTACT | 150-250 | Steps + FAQs |
| FINAL_CTA | 40-60 | Closing pitch referencing page value prop |

---

## Service Descriptions

Keep service grid card descriptions to ONE sentence. They should tell the visitor what this service covers, not sell it.

**Good:**
- "Diagnosis-first approach for under-slab leaks and water loss."
- "Comprehensive cleaning that tackles those spots you've been avoiding."
- "Perfect for Gotham renters and new homeowners."

**Bad:**
- "We offer the best slab leak detection and repair services in the area with cutting-edge technology."
- "Our amazing team provides incredible deep cleaning services that will blow your mind."

---

## FAQ Writing

### Emergency archetype (3-4 FAQs)
Focus on logistics: same-day service, estimates, permits, service area.

### Planning archetype (6-8 FAQs)
Focus on process, pricing, products, frequency, what's included, customization.

**FAQ format:** Question as `<summary>`, answer as paragraph in `<details>` body. Include city name in most questions naturally.

**Good FAQ questions:**
- "How much do house cleaners charge in Gotham?"
- "Do you offer same-day service in Gotham?"
- "Do you handle permits for plumbing work in Gotham?"

**Bad FAQ questions:**
- "Why should I choose your company?" (not a real question people ask)
- "What is plumbing?" (too generic)
