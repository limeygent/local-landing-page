# LLP Block Catalog

Every block in the Local Landing Page system. Each block has a WHEN condition, content model, atomic facts required, and HTML pattern.

---

## Progressive CTA System

CTAs throughout the page should NOT all be identical. They progress through five stages as the reader accumulates trust and context:

| Stage | Position | CTA Pattern | Purpose |
|-------|----------|-------------|---------|
| 1. Intent-Matching | HERO | Mirrors the search query ("Need a plumber in {City} now?") | Capture immediate intent |
| 2. Service-Specific | After SERVICES_GRID | References the specific service category ("Get a free {service} quote") | Connects offer to need |
| 3. Social Proof | MID_CTA (after proof blocks) | References accumulated trust ("Join 300+ {City} homeowners we've helped") | Converts fence-sitters |
| 4. Objection-Handling | After REVIEWS / GUARANTEE | Addresses #1 fear for the archetype ("No call-out fee. No obligation.") | Removes friction |
| 5. Closing Argument | FINAL_CTA | Synthesises the page's strongest point + specific next step | Drives decision |

Each block's CTA note specifies which stage applies.

---

## LLP_HERO

**WHEN:** Always
**Position:** First
**CTA Stage:** 1 — Intent-Matching

**Content Model:**
- `h1`: "{Business Name} in {City}" or "{Niche Descriptor} in {City} — [value prop]"
- `subtitle_1`: Value prop sentence with geographic scope
- `subtitle_2`: Trust/pricing promise
- `trust_badges_inline`: 3 compact badges (license, reviews, differentiator)
- `cta_primary`: Phone or booking button
- `cta_secondary`: Phone or booking button (whichever isn't primary)
- `right_column`: Varies by archetype (see below)

**Atomic Facts Required:**
- City name present in H1
- Primary service category named
- Primary CTA with availability annotation (e.g. "Available now" / "Same-week appointments")
- Service radius stated OR implied by city
- Emergency archetype: response time for this city
- Planning archetype: anti-anxiety signal (e.g. "No lock-in contracts", "Free quote")

**Right Column Variants:**

*Emergency:* Symptom router card
```html
<div class="card shadow-sm border-0">
  <div class="card-body p-4">
    <h2 class="h5 fw-bold mb-2">What's going on?</h2>
    <p class="text-muted mb-3">Pick the closest match and we'll route you to the right service.</p>
    <div class="d-grid gap-2">
      <a class="btn btn-outline-dark text-start" href="#section-id">Symptom description</a>
      <!-- repeat 3-5 symptoms -->
    </div>
  </div>
</div>
```

*Planning:* Value prop card or service selector
```html
<div class="card shadow-sm border-0">
  <div class="card-body p-4">
    <h2 class="h5 fw-bold mb-2">Get Your Free Quote</h2>
    <p class="text-muted mb-3">Tell us about your {city} home and we'll send a custom estimate.</p>
    <ul class="list-unstyled mb-3">
      <li><i class="bi bi-check-circle text-success me-2"></i>Same-week appointments</li>
      <li><i class="bi bi-check-circle text-success me-2"></i>Save 20% with recurring plans</li>
      <li><i class="bi bi-check-circle text-success me-2"></i>Satisfaction guarantee</li>
    </ul>
    <a href="tel:{phone}" class="btn btn-llp-primary w-100">Call for Quote</a>
  </div>
</div>
```

**HTML Pattern:**
```html
<!-- HERO -->
<section class="zone-group text-white position-relative overflow-hidden" id="hero"
  style="margin-left: calc(-50vw + 50%); margin-right: calc(-50vw + 50%); width: 100vw;">
  <img src="{hero_image}" alt="{business} serving {city}" fetchpriority="high" decoding="sync"
    class="position-absolute top-0 start-0 w-100 h-100 object-fit-cover" style="z-index: 0;">
  <div class="position-absolute top-0 start-0 w-100 h-100"
    style="background: linear-gradient(to right, rgba(10,15,30,0.88) 0%, rgba(10,15,30,0.75) 50%, rgba(10,15,30,0.55) 100%); z-index: 1;"></div>
  <div class="container position-relative py-5" style="z-index: 2;">
    <div class="row align-items-center py-lg-5 g-4">
      <div class="col-lg-7 py-2 py-lg-4">
        <p class="text-uppercase fw-semibold small mb-2" style="color: var(--llp-accent);">{qualifier line}</p>
        <h1 class="display-4 fw-bold lh-sm mb-3">{headline}</h1>
        <p class="lead mb-3">{subtitle_1}</p>
        <p class="lead mb-4">{subtitle_2}</p>
        <div class="d-flex flex-wrap gap-3 mb-4">
          {cta_primary} {cta_secondary}
        </div>
        <div class="d-flex flex-wrap gap-3 small opacity-75">
          {trust_badges_inline}
        </div>
      </div>
      <div class="col-lg-5">
        {right_column}
      </div>
    </div>
  </div>
</section>
```

---

## LLP_TRUST_BAR

**WHEN:** Always
**Position:** After HERO
**CTA Stage:** N/A — trust signal, no CTA

**Content Model:**
4 badges, each with icon + title + subtitle. Award badges render conditionally when real awards exist (folded in from deprecated LLP_AWARDS).

*Emergency variant:*
- Licensed & Insured (license number)
- Top Reviews (rating + count + platform)
- Clear Pricing (upfront estimates)
- Warranty (workmanship guarantee)

*Planning variant:*
- Credentials (certifications, years)
- Experience (years serving area)
- Insured & Bonded (protection details)
- Satisfaction Guarantee

*Award badge (conditional — only when real awards exist):*
- Add a 5th badge or replace the least-differentiating badge with the award name, year, and issuing body.

**Atomic Facts Required:**
- Years in business as an integer
- Review count + rating + source platform + approximate date
- License number (format varies by state/country)
- Insurance type + policy limits
- Key affiliation or certification body name
- Awards (when present): award name, issuing body, year

**HTML Pattern:**
```html
<!-- TRUST BAR -->
<section class="py-4">
  <div class="container">
    <div class="row g-3 text-center">
      <div class="col-6 col-md-3">
        <div class="p-3 border rounded-3 h-100">
          <i class="bi bi-{icon} fs-3" style="color: var(--llp-accent);"></i>
          <div class="fw-bold mt-2">{title}</div>
          <div class="small text-muted">{subtitle}</div>
        </div>
      </div>
      <!-- repeat 4x (5x if award badge present) -->
    </div>
  </div>
</section>
```

---

## LLP_AVAILABILITY

**WHEN:** `archetype in [emergency, hybrid]`
**Position:** After TRUST_BAR, before EMERGENCY_SECTION
**CTA Stage:** 1 — Intent-Matching (urgency reinforcement)

**Council insight:** All 4 models (GPT-4.1, Gemini 2.5 Pro, Claude Sonnet 4, Grok 3) independently flagged real-time availability as the #1 missing signal. CallRail and BrightLocal data confirm real-time signals increase call volume for urgent services. For planning archetype, use "Earliest Appointment: Tomorrow 8 AM" variant instead (less pressure).

**Content Model:**
- Dynamic-style bar showing availability in the city
- Emergency: "3 licensed {niche_plural} available today in {City}" or "Next available: under 60 minutes"
- Planning: "Same-week appointments available" or "Earliest appointment: {day}"
- Compact, full-width, high-contrast background

**Atomic Facts Required:**
- Specific hours as a schedule (e.g. "Mon-Fri 7am-7pm, Sat 8am-4pm, 24/7 emergency line")
- Response time for this city specifically
- After-hours surcharge policy (or explicit "no surcharge" statement)
- Dispatch location or service hub

**HTML Pattern:**
```html
<!-- AVAILABILITY -->
<section class="py-3 text-center text-white" style="background-color: var(--llp-primary-dark);">
  <div class="container">
    <div class="d-flex justify-content-center align-items-center gap-3 flex-wrap">
      <span class="d-flex align-items-center gap-2">
        <span class="bg-success rounded-circle d-inline-block" style="width: 10px; height: 10px;"></span>
        <strong>{availability_text}</strong>
      </span>
      <span class="opacity-75">|</span>
      <a href="tel:{phone}" class="text-white fw-semibold text-decoration-none">
        <i class="bi bi-telephone-fill me-1"></i>{phone_display}
      </a>
    </div>
  </div>
</section>
```

---

## LLP_EMERGENCY_SECTION

**WHEN:** `archetype in [emergency, hybrid]`
**Position:** After TRUST_BAR, before SERVICES_GRID
**CTA Stage:** 1 — Intent-Matching (scenario routing)

**Content Model:**
- `h2`: "{Niche} Emergencies in {City}"
- `intro`: Brief explanation of when to act urgently
- `scenarios`: 4-8 named emergency scenario cards (icon + title + one-line description)
- `safety_checklist`: Sidebar card with 4-6 immediate guidance steps
- `cta`: Emergency call + book urgent service

**Atomic Facts Required:**
- 4-8 named emergency scenarios (specific, not generic)
- Immediate guidance steps per scenario (what the customer should do right now)
- Emergency-specific pricing signal (e.g. diagnostic fee, call-out fee)
- Equipment readiness fact (e.g. "stocked van with 200+ parts")

**HTML Pattern:**
```html
<!-- EMERGENCY -->
<section id="{slug}-emergency" class="py-5 bg-llp-light zone-group">
  <div class="container">
    <div class="row align-items-center g-4">
      <div class="col-lg-7">
        <h2 class="fw-bold mb-2">{h2}</h2>
        <p class="text-muted mb-4">{intro}</p>
        <div class="row g-3">
          <!-- scenario cards: col-md-6 each -->
          <div class="col-md-6">
            <div class="d-flex gap-3 p-3 border rounded-3 bg-white h-100">
              <div class="icon-circle bg-llp-primary text-white"><i class="bi bi-{icon}"></i></div>
              <div>
                <div class="fw-bold">{scenario_title}</div>
                <div class="small text-muted">{scenario_desc}</div>
              </div>
            </div>
          </div>
        </div>
        <div class="mt-4 d-flex flex-column flex-sm-row gap-2">
          {emergency_ctas}
        </div>
      </div>
      <div class="col-lg-5">
        <div class="card border-0 shadow-sm">
          <div class="card-body p-4">
            <h3 class="h5 fw-bold mb-3">{checklist_title}</h3>
            <ul class="text-muted mb-0">
              <li>{step_1}</li>
              <!-- 4-6 steps -->
            </ul>
            <div class="small text-muted mt-3"><strong>Note:</strong> {safety_note}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

---

## LLP_SERVICES_GRID

**WHEN:** Always
**Position:** After TRUST_BAR (planning) or after EMERGENCY_SECTION (emergency)
**CTA Stage:** 2 — Service-Specific

**Content Model:**
- `h2`: "{Niche} Services in {City}" or "Our {Niche} Services in {City}"
- `intro`: Brief paragraph (planning archetype adds philosophy/approach intro)
- `services[]`: 4-6 cards, each with image, h3 title, city-relevant bullets, availability flag (emergency) or deliverable (planning), link URL

**Atomic Facts Required:**
- Per card: service name, link to deep page, 1-2 city-relevant bullets, availability flag (emergency) or key deliverable (planning)
- Pricing signals (see below) — no suppression without documented reason

**Pricing signals (council consensus):**
- **Emergency archetype:** NO specific prices. Use signals only: "Clear options before work begins", "Free on-site estimates", "No surprise guarantee"
- **Planning archetype:** YES show price ranges for predictable, repeatable services. Comparison shoppers need this; hiding it creates friction.
  ```
  Bi-Weekly Cleaning (Most Popular): Starting from $150-$190 for a typical 3-bed, 2-bath home.
  Deep Cleaning / One-Time Service: Starting from $350+.
  Get your precise, no-obligation quote in 60 seconds.
  ```
- **Hybrid archetype:** Price ranges for planned services only, not emergency/variable services

**HTML Pattern:**
```html
<!-- SERVICES GRID -->
<section class="py-5 zone-group" id="{slug}-services">
  <div class="container">
    <div class="text-center mb-4">
      <h2 class="fw-bold mb-2">{h2}</h2>
      <p class="text-muted mb-0">{intro}</p>
    </div>
    <div class="row g-4">
      <!-- repeat per service: col-md-6 col-lg-4 -->
      <div class="col-md-6 col-lg-4">
        <a class="text-decoration-none text-dark" href="{service_url}">
          <div class="card card-hover h-100 border-0 shadow-sm overflow-hidden">
            <img loading="lazy" decoding="async" src="{image_url}" alt="{service} in {city}" class="card-img-top" width="100%">
            <div class="card-body p-4">
              <h3 class="h5 fw-bold">{service_title}</h3>
              <p class="text-muted mb-0">{service_description}</p>
            </div>
          </div>
        </a>
      </div>
    </div>
    <div class="text-center mt-4">
      {cta_button}
    </div>
  </div>
</section>
```

**Note for planning archetype:** Add 1-2 paragraph intro before the grid describing the approach/philosophy. Example: "Most cleaning companies in {City} promise the world and deliver mediocre results. We do it differently..."

---

## LLP_WHY_CHOOSE

**WHEN:** Always (all archetypes)
**Position:** After SERVICES_GRID (planning/hybrid); after REVIEWS (emergency — placed lower so proof comes first)
**CTA Stage:** 2 — Service-Specific (planning) / 3 — Social Proof (emergency, positioned post-reviews)

**Council change:** Previously planning-only. Now appears in ALL archetypes. For Emergency archetype, positioned after REVIEWS so social proof precedes the differentiator argument.

**Content Model:**
- `h2`: "What Makes {Business} {City}'s Go-To {Niche}"
- 4 differentiator items, each with title + description paragraph
- **Every bullet must be falsifiable** — not "we care about customers" but "we arrive on time because we only book 6 jobs per tech per day"
- At least 1 city-specific claim
- Maximum 1 soft/values statement per block
- Optional: "Best fit / not best fit" subsection for high_stakes modifier (helps self-qualify leads)
- **For in-home services (cleaning, pest control, HVAC):** Must include vetting/background check differentiator and "same person every visit" consistency claim (council consensus: #1 closer for planning archetypes)

**Atomic Facts Required:**
- 4 differentiators, each with a specific mechanism explaining WHY the claim is true
- At least 1 city-specific claim (local knowledge, local team, local history)
- No more than 1 soft/values statement (the rest must be operational)
- high_stakes modifier: include "best fit / not best fit" subsection

**HTML Pattern:**
```html
<!-- WHY CHOOSE -->
<section class="py-5 bg-llp-light zone-group" id="{slug}-why-choose">
  <div class="container">
    <h2 class="fw-bold mb-4">{h2}</h2>
    <p class="text-muted mb-4">{intro_connecting_to_city}</p>
    <div class="row g-4">
      <div class="col-md-6">
        <div class="d-flex gap-3 mb-3">
          <div class="icon-circle bg-llp-primary text-white flex-shrink-0"><i class="bi bi-{icon}"></i></div>
          <div>
            <h3 class="h6 fw-bold">{differentiator_title}</h3>
            <p class="text-muted mb-0">{differentiator_description_with_mechanism}</p>
          </div>
        </div>
      </div>
      <!-- repeat 4x in col-md-6 -->
    </div>
    <!-- Optional: high_stakes modifier only -->
    <!-- <div class="mt-4 p-4 border rounded-3 bg-white">
      <h3 class="h6 fw-bold mb-2">Is {Business} the right fit for you?</h3>
      <div class="row g-3">
        <div class="col-md-6">
          <p class="small fw-semibold text-success mb-1">Best fit if you...</p>
          <ul class="small text-muted">{best_fit_list}</ul>
        </div>
        <div class="col-md-6">
          <p class="small fw-semibold text-muted mb-1">Probably not the right fit if...</p>
          <ul class="small text-muted">{not_fit_list}</ul>
        </div>
      </div>
    </div> -->
  </div>
</section>
```

---

## LLP_ABOUT

**WHEN:** `archetype == planning`
**Position:** After WHY_CHOOSE
**CTA Stage:** N/A — narrative block

**Content Model:**
- `h2`: "About {Business} in {City}"
- 2-3 paragraphs: founding story, connection to community, mission
- Optional link to full about page

**Atomic Facts Required:**
- Founding year + founder name (or principals)
- Local origin story (why this city, how it started)
- Company size metrics (number of staff, trucks, locations, jobs completed)
- Community involvement (specific — sponsorships, local partnerships, events)
- Geographic focus statement (which areas are served, which are not)

**HTML Pattern:**
```html
<!-- ABOUT -->
<section class="py-5 zone-group" id="{slug}-about">
  <div class="container">
    <div class="row g-4 align-items-center">
      <div class="col-lg-8">
        <h2 class="fw-bold mb-3">{h2}</h2>
        <p class="text-muted">{paragraph_1}</p>
        <p class="text-muted">{paragraph_2}</p>
        <a href="{about_url}" class="fw-semibold" style="color: var(--llp-primary);">Learn more about our story →</a>
      </div>
    </div>
  </div>
</section>
```

---

## LLP_PROCESS

**WHEN:** `archetype == planning` (also useful for hybrid when scope complexity is high)
**Position:** After ABOUT
**CTA Stage:** 2 — Service-Specific

**Previously named:** LLP_SERVICE_APPROACH. Renamed and refocused on service delivery experience, not philosophy.

**Content Model:**
- `h2`: "How {Business} Works in {City}"
- 3-5 numbered steps: each with title, duration, deliverable, and what the customer must do
- Payment structure: when deposits are required, when final payment is due
- Scope change policy: what happens if scope grows after quoting
- Optional: typical completion time statement

**Atomic Facts Required:**
- Steps with estimated durations (not just names)
- Deliverable per step (what the customer receives or decides at each step)
- Payment structure (deposit %, balance timing, payment methods)
- Scope change policy (stated explicitly, not implied)
- What the customer is responsible for at each step

**HTML Pattern:**
```html
<!-- PROCESS -->
<section class="py-5 bg-llp-light zone-group" id="{slug}-process">
  <div class="container">
    <h2 class="fw-bold mb-2">{h2}</h2>
    <p class="text-muted mb-4">Here's exactly what to expect when you work with {business} in {city}.</p>
    <div class="row g-4">
      <div class="col-md-4">
        <div class="p-4 bg-white border rounded-3 h-100">
          <div class="display-6 fw-bold mb-2" style="color: var(--llp-accent);">01</div>
          <h3 class="h6 fw-bold mb-2">{step_title}</h3>
          <p class="text-muted mb-2 small">{step_description}</p>
          <div class="small text-muted"><strong>Duration:</strong> {duration}</div>
          <div class="small text-muted"><strong>You receive:</strong> {deliverable}</div>
          <div class="small text-muted"><strong>You need to:</strong> {customer_action}</div>
        </div>
      </div>
      <!-- repeat 3-5x -->
    </div>
    <div class="mt-4 p-4 bg-white border rounded-3">
      <div class="row g-3">
        <div class="col-md-6">
          <p class="small mb-1"><strong>Payment structure:</strong> {payment_structure}</p>
        </div>
        <div class="col-md-6">
          <p class="small mb-1"><strong>If scope changes:</strong> {scope_change_policy}</p>
        </div>
      </div>
    </div>
    <p class="text-muted mt-4 small"><strong>Most {city} {service_plural}</strong> are completed within {timeframe}.</p>
  </div>
</section>
```

---

## LLP_LOCAL_KNOWLEDGE

**WHEN:** Always (content depth varies by archetype)
**Position:** After SERVICES_GRID (emergency) or after PROCESS (planning)
**CTA Stage:** N/A — authority/trust signal

**Content Model:**

*Emergency:* Deep technical knowledge
- `h2`: "{City} {Niche}: Local Realities"
- 3 knowledge cards (icon + title + data-rich description with stats)
- Sidebar: "Common call-us-now signs" checklist

*Planning:* Lighter city overview
- `h2`: "About {City} & Our Service Areas"
- City demographics paragraph (population, region, communities)
- Brief description of what creates local demand

**Atomic Facts Required:**
- 3+ neighborhoods named specifically (not "surrounding areas")
- 2+ property-age or construction insights relevant to the niche (e.g. "most homes in this area were built pre-1980 and still have original copper plumbing")
- 2+ climate or seasonality insights affecting service demand
- 1+ local utility, authority, or regulatory body named with its relevance
- BANNED: "We know the local area" without backing facts

**HTML Pattern (Emergency):**
```html
<!-- LOCAL KNOWLEDGE -->
<section class="py-5 bg-llp-light zone-group" id="{slug}-local-knowledge">
  <div class="container">
    <div class="row g-4 align-items-start">
      <div class="col-lg-6">
        <h2 class="fw-bold mb-2">{h2}</h2>
        <p class="text-muted mb-4">{intro}</p>
        <!-- 3 knowledge cards -->
        <div class="d-flex gap-3 p-3 border rounded-3 bg-white mb-3">
          <div class="icon-circle bg-llp-primary text-white"><i class="bi bi-{icon}"></i></div>
          <div>
            <div class="fw-bold">{knowledge_title}</div>
            <div class="text-muted small">{knowledge_detail_with_stats}</div>
          </div>
        </div>
      </div>
      <div class="col-lg-6">
        <div class="card border-0 shadow-sm">
          <div class="card-body p-4">
            <h3 class="h5 fw-bold mb-3">Common "call us now" signs</h3>
            <ul class="text-muted mb-0">
              <li>{sign_1}</li>
              <!-- 4-6 signs -->
            </ul>
            <div class="mt-4 d-flex flex-column flex-sm-row gap-2">{ctas}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

**HTML Pattern (Planning):**
```html
<!-- LOCAL KNOWLEDGE -->
<section class="py-5 zone-group" id="{slug}-about-city">
  <div class="container">
    <h2 class="fw-bold mb-3">{h2}</h2>
    <p class="text-muted">{city_overview_paragraph}</p>
    <p class="text-muted">{demand_drivers_paragraph}</p>
  </div>
</section>
```

---

## LLP_LICENSING_COMPLIANCE

**WHEN:** `regulated == true` OR `niche in [plumbing, hvac, electrical, roofing]`
**Position:** After LOCAL_KNOWLEDGE
**CTA Stage:** N/A — credibility signal

**Merged from:** LLP_CODES_COMPLIANCE + LLP_PERMITS_INSPECTIONS + LLP_CREDENTIALS. Single block for all regulatory/compliance content.

**Content Model:**
- `h2`: "{City} {Niche} Licensing, Codes & Permits"
- 4-6 compliance cards covering: specific code adoption (chapter + version), licensing requirements, permit requirements, inspection process (named inspections), insurance/bonding, regulatory body links
- Homeowner resources section with verification URLs
- For regulated industries (dental, medical, legal): practitioner name, registration/license numbers, qualifications, verification links

**Atomic Facts Required:**
- Specific code chapter and version (e.g. "AS/NZS 3500:2021 — adopted statewide March 2022" or "2021 International Plumbing Code with local amendments")
- Named inspections required per job type (e.g. "rough-in inspection before wall closure, final inspection before occupancy")
- Consequences of non-compliance stated plainly (insurance voidance, resale problems, fines)
- Whether permit fees are included in quotes or billed separately
- License verification URL (official government or regulatory body)
- Insurance policy type and limits (not just "we're insured")
- For dental/medical: practitioner registration number and regulatory body name

**HTML Pattern:**
```html
<!-- LICENSING & COMPLIANCE -->
<section class="py-5 zone-group" id="{slug}-compliance">
  <div class="container">
    <div class="text-center mb-4">
      <h2 class="fw-bold mb-2">{h2}</h2>
      <p class="text-muted mb-0">Transparency: know exactly what regulations and requirements govern this work.</p>
    </div>
    <div class="row g-4">
      <!-- 4-6 cards: col-lg-6 each -->
      <div class="col-lg-6">
        <div class="card border-0 shadow-sm h-100">
          <div class="card-body p-4">
            <h3 class="h5 fw-bold mb-3">
              <i class="bi bi-{icon} me-2" style="color: var(--llp-accent);"></i>{card_title}
            </h3>
            <p class="text-muted mb-3">{card_content}</p>
            <div class="small text-muted">{supplementary_detail}</div>
            <a href="{verification_url}" target="_blank" class="small fw-semibold mt-2 d-inline-block" style="color: var(--llp-primary);">
              {verification_link_text} →
            </a>
          </div>
        </div>
      </div>
    </div>
    <!-- Permits subsection using details/summary for collapsible content -->
    <div class="mt-4">
      <h3 class="h5 fw-bold mb-3">Permits & Inspections in {City}</h3>
      <div class="row g-4">
        <div class="col-lg-7">
          <details class="border rounded-3 p-3 mb-2">
            <summary class="fw-semibold">{permit_category_title}</summary>
            <p class="text-muted mt-2 mb-0 small">{permit_details}</p>
          </details>
          <!-- repeat 3-4x -->
        </div>
        <div class="col-lg-5">
          <div class="card border-0 shadow-sm">
            <div class="card-body p-4">
              <h4 class="h6 fw-bold mb-3">Why permits matter</h4>
              <ul class="text-muted small mb-0">
                <li>Insurance claims can be voided for unpermitted work</li>
                <li>{local_specific_consequence}</li>
                <li>Resale inspections flag unpermitted additions</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

---

## LLP_MEET_THE_TEAM

**WHEN:** `team_photos_available == true` (all archetypes, especially planning and hybrid)
**Position:** After WHY_CHOOSE (planning) or after SERVICES_GRID (emergency/hybrid)
**CTA Stage:** N/A — trust signal

**Council insight:** All 4 models independently flagged this as the biggest missing trust signal. Directly counters the #1 fear in local services: "Who am I letting into my home?" Edelman Trust Barometer data shows neighborly identification outperforms generic team stock images. Authority Brands (Mister Sparky, One Hour HVAC) uses this extensively.

**Content Model:**
- `h2`: "Meet Your Local {City} Team" or "Your {City} {Niche} Team"
- Minimum 2-3 team member cards (do not render with only 1 person)
- Per person: full name, real photo (NOT stock), credentials with issuing body, years with this company (not just industry), local connection
- "All staff are background-checked and insured" note

**Atomic Facts Required:**
- Per person: full name, real photo (not stock), credential name with issuing body, years with THIS company, local connection (suburb/neighborhood of residence, local sports team, community tie)
- Minimum 2-3 people
- Background check policy stated
- If no real photos are available: suppress the block entirely

**HTML Pattern:**
```html
<!-- MEET THE TEAM -->
<section class="py-5 zone-group" id="{slug}-team">
  <div class="container">
    <div class="text-center mb-4">
      <h2 class="fw-bold mb-2">{h2}</h2>
      <p class="text-muted mb-0">The people behind the service. All team members are background-checked and insured.</p>
    </div>
    <div class="row g-4 justify-content-center">
      <!-- 2-4 members: col-md-6 col-lg-3 -->
      <div class="col-md-6 col-lg-3">
        <div class="card border-0 shadow-sm h-100 text-center">
          <img src="{photo_url}" alt="{name}, {role} in {city}" class="card-img-top" style="height: 200px; object-fit: cover;">
          <div class="card-body p-3">
            <h3 class="h6 fw-bold mb-1">{first_name} {last_name}</h3>
            <div class="small mb-1" style="color: var(--llp-accent);">{role}</div>
            <div class="small text-muted mb-2">{credential} · {issuing_body}</div>
            <div class="small text-muted mb-2">{years_with_company} years with {business}</div>
            <p class="small text-muted mb-0">"{local_connection_or_quote}"</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

**Fallback (no team photos available):** Suppress this block entirely. Do NOT use stock photos. The value is in authenticity.

---

## LLP_NEIGHBORHOODS

**WHEN:** Always — suppress only if neighborhood-level data cannot be produced
**Position:** After LOCAL_KNOWLEDGE (emergency) or after MEET_THE_TEAM / WHY_CHOOSE (planning)
**CTA Stage:** N/A — geographic authority signal

**Content Model:**
- `h2`: "Areas We Serve in {City}"
- Cluster neighborhoods into 3-5 groups with shared property or service characteristics
- Each card: neighborhood cluster name, property/service traits, drive time from business, observed job or service patterns
- Zip codes
- "We Also Serve" section with nearby communities and drive times (planning archetype)

**Atomic Facts Required:**
- Neighborhoods clustered into 3-5 groups (not just a flat list)
- Property type or service pattern per cluster (e.g. "predominantly federation-era homes with original clay pipes")
- Drive times from business address to each cluster
- Observed jobs or service frequency per neighborhood (e.g. "most common call type: hot water system replacement")
- If this level of specificity cannot be produced: suppress the block

**HTML Pattern:**
```html
<!-- NEIGHBORHOODS -->
<section class="py-5 bg-llp-light zone-group" id="{slug}-neighborhoods">
  <div class="container">
    <div class="text-center mb-4">
      <h2 class="fw-bold mb-2">{h2}</h2>
      <p class="text-muted mb-0">Serving all {city} neighborhoods with genuine local knowledge.</p>
    </div>
    <div class="row g-4">
      <!-- 3-5 cluster cards: col-md-6 col-lg-4 -->
      <div class="col-md-6 col-lg-4">
        <div class="p-4 bg-white border rounded-3 h-100">
          <h3 class="h6 fw-bold mb-2">
            <i class="bi bi-pin-map-fill me-2" style="color: var(--llp-accent);"></i>{cluster_name}
          </h3>
          <p class="small text-muted mb-2">{property_and_service_traits}</p>
          <ul class="text-muted mb-0 small">
            <li><strong>Drive time:</strong> {drive_time} from our base</li>
            <li><strong>Common jobs:</strong> {job_pattern}</li>
          </ul>
        </div>
      </div>
    </div>
    <div class="text-center mt-4">
      <div class="small text-muted">Serving all {city} zip codes: {zip_list}</div>
    </div>
  </div>
</section>
```

**Planning variant adds:** "We Also Serve" section below the grid with nearby communities and drive times.

---

## LLP_REVIEWS

**WHEN:** `review_count >= 5` (suppress if requirements below cannot be met)
**Position:** After NEIGHBORHOODS
**CTA Stage:** 3 — Social Proof

**Content Model:**
- `h2`: "What {City} {Audience} Say"
- Minimum 5 reviews displayed (3+ must name a suburb or specific service)
- Per review: reviewer name + suburb, review text naming a specific service, date less than 18 months old, source platform
- CTA to full Google reviews (gbp_url)

**Atomic Facts Required:**
- Reviewer name + suburb for each review
- Review text that names a specific service or technician (not generic praise)
- Date less than 18 months old
- Source platform named (Google, Facebook, etc.)
- Minimum 5 reviews shown, minimum 3 suburb-specific
- If requirements cannot be met: suppress and reduce threshold or add review acquisition note to client

**HTML Pattern:**
```html
<!-- REVIEWS -->
<section class="py-5 zone-group" id="{slug}-reviews">
  <div class="container">
    <div class="text-center mb-4">
      <h2 class="fw-bold mb-2">{h2}</h2>
      <p class="text-muted mb-0">Real feedback from real customers in {city}.</p>
    </div>
    <div class="row g-4">
      <!-- 5+ reviews: col-lg-4 each, wrap naturally -->
      <div class="col-lg-4">
        <div class="p-4 border rounded-3 h-100">
          <div class="fw-bold mb-1">{name} · {suburb}</div>
          <div class="small text-muted mb-2">{platform} · {date}</div>
          <div class="mb-2" style="color: var(--llp-accent);">
            <i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i>
          </div>
          <p class="text-muted mb-0">"{review_text}"</p>
        </div>
      </div>
    </div>
    <div class="text-center mt-4">
      <a class="btn btn-outline-llp-primary fw-semibold" href="{gbp_url}" target="_blank">
        <i class="bi bi-box-arrow-up-right me-2"></i>Read More Reviews on Google
      </a>
    </div>
  </div>
</section>
```

---

## LLP_MID_CTA

**WHEN:** `archetype in [emergency, hybrid]`
**Position:** After block 6-7 (mid-page, after proof blocks — after REVIEWS or RECENT_WORK)
**CTA Stage:** 3 — Social Proof (references accumulated trust)

**Content Model:**
- Slim full-width bar similar to AVAILABILITY styling
- CTA text references something the reader has now seen (reviews, credentials, team) — different from Hero CTA
- Emergency: "Convinced? Our techs are ready." / Planning: "Seen enough? Let's get you a quote."
- Phone number inline

**Atomic Facts Required:**
- CTA text must differ from HERO CTA (cannot be identical)
- References a specific trust signal from above on the page (review count, years in business, or guarantee)

**HTML Pattern:**
```html
<!-- MID CTA -->
<section class="py-3 text-center" style="background-color: var(--llp-primary); color: #fff;">
  <div class="container">
    <div class="d-flex justify-content-center align-items-center gap-3 flex-wrap">
      <span class="fw-semibold">{evolved_cta_text}</span>
      <a href="tel:{phone}" class="btn btn-light btn-sm fw-semibold">
        <i class="bi bi-telephone me-1"></i>{phone_display}
      </a>
    </div>
  </div>
</section>
```

---

## LLP_RECENT_WORK

**WHEN:** Always — suppress if no real job data is available
**Position:** After REVIEWS (or after MID_CTA if present)
**CTA Stage:** N/A — proof signal

**Content Model:**

*Emergency:* 3 case study cards with neighborhood/zip, property type, problem-to-solution narrative, timeframe, cost band
*Planning:* Paragraph-style project highlights or before/after card layout

**Atomic Facts Required:**
- Per job: neighborhood or zip code, property type, specific problem, specific solution, timeframe, cost band (approximate range)
- Before/after photos when available (use actual job photos, never stock)
- If no real job data is available: suppress the block

**Visual proof enhancement (council recommendation):**
When before/after photos are available, use image cards instead of text-only cards. Especially powerful for planning niches (cleaning, landscaping, cosmetic dental). Use real job photos, never stock.

**Hyper-local vehicle/landmark photos (council insight):**
If available, include a photo of the branded service vehicle at a recognizable local landmark. This is "unfakeable geographic proof" that national lead-gen sites cannot replicate. Can be placed here or in NEIGHBORHOODS.

**HTML Pattern (Emergency):**
```html
<!-- RECENT WORK -->
<section class="py-5 bg-llp-light zone-group" id="{slug}-recent-work">
  <div class="container">
    <div class="text-center mb-4">
      <h2 class="fw-bold mb-2">Recent {Niche} Jobs in {City}</h2>
      <p class="text-muted mb-0">Real examples of problems we solve in {city}.</p>
    </div>
    <div class="row g-4">
      <!-- 3 cards: col-md-6 col-lg-4 -->
      <div class="col-md-6 col-lg-4">
        <div class="card border-0 shadow-sm h-100">
          <div class="card-body p-4">
            <div class="small text-muted mb-1">{neighborhood} · {property_type} · {date}</div>
            <h3 class="h6 fw-bold mb-2">{job_title}</h3>
            <p class="text-muted mb-2 small">{problem_to_solution_narrative}</p>
            <div class="small text-muted"><strong>Timeframe:</strong> {timeframe} · <strong>Cost band:</strong> {cost_band}</div>
          </div>
        </div>
      </div>
    </div>
    <div class="text-center mt-4">{cta}</div>
  </div>
</section>
```

---

## LLP_PRICING

**WHEN:** `archetype == planning` OR (`archetype == hybrid` AND planned services exist)
**Position:** After PROCESS or after SERVICES_GRID
**CTA Stage:** 2 — Service-Specific (transparency builds confidence)

**NOT rendered for Emergency archetype** — pricing signals for emergency go in HERO and TRUST_BAR instead.

**Content Model varies by modifier:**
- `low_stakes`: Full ranges per service tier, what's included vs extra (e.g. cleaning, pest control)
- `high_stakes`: Market ranges + what drives variation + financing options (e.g. HVAC install, dental implants)
- `recurring`: Plan pricing with savings for commitment (e.g. monthly maintenance, subscription cleaning)

**Atomic Facts Required:**
- Price ranges for top 3-5 services (not "call for pricing" — if you can't show ranges, don't render this block)
- What factors influence price (so the range makes sense to the reader)
- What is included vs. what costs extra
- Payment methods accepted
- Financing options (if available) with provider name and terms
- Whether quotes are binding or estimates

**HTML Pattern:**
```html
<!-- PRICING -->
<section class="py-5 bg-llp-light zone-group" id="{slug}-pricing">
  <div class="container">
    <div class="text-center mb-4">
      <h2 class="fw-bold mb-2">{h2}</h2>
      <p class="text-muted mb-0">{intro — transparency statement, e.g. "We believe in clear pricing upfront."}</p>
    </div>
    <div class="row g-4 justify-content-center">
      <div class="col-md-6 col-lg-4">
        <div class="card border-0 shadow-sm h-100">
          <div class="card-body p-4 text-center">
            <h3 class="h5 fw-bold mb-2">{service_name}</h3>
            <div class="display-6 fw-bold mb-2" style="color: var(--llp-primary);">{price_range}</div>
            <p class="text-muted small mb-3">{what_influences_price}</p>
            <ul class="list-unstyled text-start small text-muted mb-3">
              <li><i class="bi bi-check text-success me-1"></i>{included_1}</li>
              <li><i class="bi bi-check text-success me-1"></i>{included_2}</li>
              <li><i class="bi bi-x text-muted me-1"></i>{not_included — optional}</li>
            </ul>
          </div>
        </div>
      </div>
      <!-- repeat for top 3-5 services -->
    </div>
    <div class="text-center mt-4">
      <p class="text-muted small">{pricing_disclaimer — e.g. binding vs estimate, valid period}</p>
      {cta}
    </div>
  </div>
</section>
```

---

## LLP_GUARANTEE

**WHEN:** `archetype in [planning, hybrid]`
**Position:** After PRICING or after WHY_CHOOSE
**CTA Stage:** 4 — Objection-Handling

**NOT rendered for Emergency archetype** — guarantee signals for emergency go in TRUST_BAR.

**Content Model:**
- Named guarantee (e.g. "The 24-Hour Re-Clean Promise", "The On-Time Guarantee")
- Trigger conditions: exactly when the guarantee applies
- Specific remedy: what the business will do (not just "we'll make it right")
- Time window: how long the customer has to invoke it
- Exclusions: what is not covered (honesty builds trust)

**Regulatory note:** For regulated industries (dental, medical, legal), use process guarantees ONLY. Do NOT guarantee clinical outcomes — this constitutes an AHPRA/professional body violation in Australia and equivalent violations elsewhere. Example: "We guarantee a same-day call back" is safe; "We guarantee pain-free treatment" is not.

**Atomic Facts Required:**
- Named guarantee (not generic "satisfaction guaranteed")
- Trigger conditions stated explicitly
- Specific remedy (re-clean within 24hrs, refund within 7 days, return visit at no charge)
- Time window for invoking
- Exclusions (at least 1 stated to demonstrate good faith)

**HTML Pattern:**
```html
<!-- GUARANTEE -->
<section class="py-5 zone-group" id="{slug}-guarantee">
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-lg-8 text-center">
        <div class="p-5 border rounded-3 bg-white shadow-sm">
          <i class="bi bi-shield-check display-4 mb-3" style="color: var(--llp-accent);"></i>
          <h2 class="fw-bold mb-3">{guarantee_name}</h2>
          <p class="lead text-muted mb-3">{guarantee_description — specific and operational}</p>
          <p class="text-muted mb-4">{terms_and_scope — trigger conditions, time window, exclusions}</p>
          <a href="tel:{phone}" class="btn btn-llp-primary btn-lg">
            <i class="bi bi-telephone me-2"></i>{cta_text}
          </a>
        </div>
      </div>
    </div>
  </div>
</section>
```

---

## LLP_FAQ

**WHEN:** Always (depth varies by archetype)
**Position:** Before MAP_CONTACT (replaces FAQ section that was previously embedded inside MAP_CONTACT)
**CTA Stage:** 4 — Objection-Handling

**Content Model:**
- Emergency: 3-5 questions focused on logistics (arrival time, pricing, permits, after-hours)
- Planning: 6-8 questions covering process, pricing, products, customisation, guarantees
- Every answer must contain at least one specific fact (number, policy, local reference, timeframe)
- Questions must come from real customer conversations, not generic SEO filler
- MUST NOT contain "Why should I choose you?" type questions — that belongs in WHY_CHOOSE
- Implement FAQ schema markup (JSON-LD)

**Atomic Facts Required:**
- 5-8 questions sourced from real customer objections or inquiries
- Each answer contains at least 1 specific fact (not vague reassurance)
- FAQ schema JSON-LD block present

**HTML Pattern:**
```html
<!-- FAQ -->
<section class="py-5 bg-llp-light zone-group" id="{slug}-faq">
  <div class="container">
    <div class="text-center mb-4">
      <h2 class="fw-bold mb-2">Frequently Asked Questions</h2>
      <p class="text-muted mb-0">Straight answers to the questions {city} customers ask most.</p>
    </div>
    <div class="row justify-content-center">
      <div class="col-lg-8">
        <div class="accordion" id="faq-accordion">
          <div class="accordion-item border-0 mb-2">
            <h3 class="accordion-header">
              <button class="accordion-button collapsed fw-semibold" type="button" data-bs-toggle="collapse" data-bs-target="#faq-1">
                {question}
              </button>
            </h3>
            <div id="faq-1" class="accordion-collapse collapse" data-bs-parent="#faq-accordion">
              <div class="accordion-body text-muted">{answer — must contain at least 1 specific fact}</div>
            </div>
          </div>
          <!-- repeat for each question, increment faq-N -->
        </div>
      </div>
    </div>
  </div>
</section>

<!-- FAQ Schema -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "{question}",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "{answer}"
      }
    }
  ]
}
</script>
```

---

## LLP_MAP_CONTACT

**WHEN:** Always
**Position:** After FAQ, second-to-last (before FINAL_CTA)
**CTA Stage:** 4 — Objection-Handling (contact details remove final friction)

**Content Model:**
- `h2`: "Serving {City}, {State}"
- Google Maps embed (if map_embed_url provided)
- "How it works" 3-step process (simplified — full process detail lives in LLP_PROCESS)
- Full NAP (name, address, phone)
- All contact channels with response times per channel
- Service hours
- Parking/accessibility notes (planning archetype)

**Note:** FAQs have moved out of this block to the standalone LLP_FAQ block. MAP_CONTACT now focuses purely on contact logistics and geographic confirmation.

**Atomic Facts Required:**
- Embedded map (or explicit note if not available)
- Full NAP (name, address including postcode, all phone numbers)
- All contact channels with stated response times (phone, email, form, chat)
- Service hours as a schedule (not "during business hours")
- Parking or accessibility notes for planning archetypes where customers visit the premises

**HTML Pattern:** 2-column layout. Left: map embed (ratio-1x1) + NAP. Right: contact channels + how-it-works steps.

Planning archetype adds a directions subsection after the map with text directions from 2-3 key landmarks.

---

## LLP_FINAL_CTA

**WHEN:** Always
**Position:** Last
**CTA Stage:** 5 — Closing Argument

**Content Model:**
- `h2`: "Ready for {Service} in {City}?"
- Closing pitch references something specific from the page (a guarantee, a stat, the team)
- Community proof line ("Join hundreds of satisfied {City} customers")
- Friction-reducer addressing the #1 objection for this archetype:
  - Emergency: "No call-out fee to diagnose the problem"
  - Planning: "No lock-in contracts. Cancel anytime."
  - Hybrid: "Free quote, no obligation"
- Dual CTAs: primary action + phone
- Specific next step (NOT "reach out" or "get in touch" — use "Call now", "Book online", "Get your quote in 60 seconds")
- Serving line: "Proudly serving {city}, {neighborhoods}, and surrounding communities."

**Atomic Facts Required:**
- CTA language references something specific from the page (not a generic closing)
- Friction-reducer addresses the documented #1 objection for this archetype
- Specific next step described (not "reach out")
- Serving line names at least 3 specific neighborhoods or communities

**HTML Pattern:**
```html
<!-- FINAL CTA -->
<section class="py-5 text-center zone-group" id="{slug}-cta" style="background-color: var(--llp-primary); color: #fff;">
  <div class="container">
    <h2 class="fw-bold mb-3">{h2}</h2>
    <p class="lead mb-2">{closing_pitch — references specific page content}</p>
    <p class="mb-2">{community_proof}</p>
    <p class="mb-4 opacity-75 small">{friction_reducer — addresses #1 archetype objection}</p>
    <div class="d-flex flex-wrap justify-content-center gap-3 mb-3">
      {cta_primary — specific next step} {cta_secondary — phone}
    </div>
    <p class="small opacity-75 mb-0">{serving_line — 3+ named neighborhoods}</p>
  </div>
</section>
```

---

## Block Reference: Deprecated

The following blocks have been removed from the catalog. Their content is now folded into other blocks.

| Deprecated Block | Content folded into |
|---|---|
| LLP_CODES_COMPLIANCE | LLP_LICENSING_COMPLIANCE |
| LLP_PERMITS_INSPECTIONS | LLP_LICENSING_COMPLIANCE |
| LLP_CREDENTIALS | LLP_LICENSING_COMPLIANCE |
| LLP_AWARDS | Award badges → TRUST_BAR (conditional). Award narratives → WHY_CHOOSE (as proof points). |
| LLP_DIRECTIONS | LLP_MAP_CONTACT (directions subsection) |
| LLP_SERVICE_APPROACH | LLP_PROCESS (renamed + expanded) |
