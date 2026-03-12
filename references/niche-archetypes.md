# Niche Archetypes

LLP structure adapts based on the niche's urgency profile. Three archetypes determine which blocks appear and in what order. Page-level modifiers then refine archetype behavior based on stakes, regulation, price point, and service frequency.

## Auto-Detection Logic

```
IF niche in [plumbing, hvac, electrical, locksmith, towing, restoration, water_damage]:
    archetype = emergency

ELIF niche in [cosmetic_dentist, financial_planner, accounting, cleaning, landscaping,
               pool_service, interior_design, photography, tutoring, personal_training]:
    archetype = planning

ELIF niche in [general_dentist, auto_repair, pest_control, roofing, garage_door,
               appliance_repair, tree_service]:
    archetype = hybrid

ELSE:
    archetype = planning  # safe default
```

User can override with `--archetype emergency|planning|hybrid`.

---

## Page-Level Modifiers

Applied after archetype detection. Each modifier refines which blocks render and how they behave.

```
MODIFIERS (applied after archetype detection):

stakes:
  IF niche in [cosmetic_dentist, financial_planner, legal, surgeon, major_remodel, wedding]:
    stakes = high
  ELIF niche in [cleaning, lawn_care, car_detailing, junk_removal, pet_grooming]:
    stakes = low
  ELSE:
    stakes = medium  # default

regulated:
  IF niche in [plumbing, hvac, electrical, roofing, dental, legal, financial, medical]:
    regulated = true
  ELSE:
    regulated = false

high_ticket:
  IF niche in [roofing, kitchen_remodel, cosmetic_dentist, pool_construction, solar, landscaping_major]:
    high_ticket = true
  ELSE:
    high_ticket = false

recurring:
  IF niche in [cleaning, lawn_care, pest_control, pool_service, accounting, general_dentist]:
    recurring = true
  ELSE:
    recurring = false
```

### What Each Modifier Controls

- **`stakes`** → depth of CREDENTIALS, CASE_STUDIES, PROCESS blocks. High-stakes front-loads proof. Low-stakes keeps those blocks brief or omits them.
- **`regulated`** → LLP_LICENSING_COMPLIANCE block renders. Trust bar emphasizes license numbers.
- **`high_ticket`** → PRICING block shows market ranges + what drives variation + financing options. LLP_RECENT_WORK becomes detailed case studies rather than brief job snapshots.
- **`recurring`** → Plan/subscription pricing in PRICING block. Consistency and reliability messaging emphasized in WHY_CHOOSE.

---

## Block Catalog Changes

The block catalog has been updated. Key changes from previous version:

- **Merged:** LLP_CODES_COMPLIANCE + LLP_PERMITS_INSPECTIONS + LLP_CREDENTIALS → **LLP_LICENSING_COMPLIANCE**
- **Killed:** LLP_AWARDS (content absorbed into TRUST_BAR and WHY_CHOOSE)
- **Killed:** LLP_DIRECTIONS (absorbed into MAP_CONTACT)
- **Renamed:** LLP_SERVICE_APPROACH → **LLP_PROCESS**
- **New:** LLP_PRICING, LLP_FAQ, LLP_GUARANTEE, LLP_MID_CTA
- **LLP_WHY_CHOOSE** now appears in ALL archetypes (position varies per archetype)

---

## Emergency Archetype

**Niches:** Plumbing, HVAC, electrical, locksmith, towing, restoration

**User state:** Stressed, needs help NOW. Searching because something broke.
**Psychology:** "Who can fix this fast? Are they legit? How much?"
**Goal:** Drive immediate call or booking.

### Hero Right Column: Symptom Router
"What's going on?" with 4-5 buttons linking to page sections:
- Active leak / water damage → #emergency
- No hot water / water heater issue → #water-heater
- Clogged drain / sewer smell → #drains
- etc.

### Trust Bar Content
Licensed & Insured | Top Reviews | Clear Pricing | Warranty

### Block Order
1. LLP_HERO (symptom router, call CTA dominant)
2. LLP_TRUST_BAR
3. LLP_AVAILABILITY
4. LLP_EMERGENCY_SECTION
5. LLP_SERVICES_GRID (slim, with emergency tags)
6. LLP_MID_CTA (mid-page phone CTA with evolved text)
7. LLP_LOCAL_KNOWLEDGE
8. LLP_LICENSING_COMPLIANCE (if regulated)
9. LLP_NEIGHBORHOODS
10. LLP_REVIEWS
11. LLP_RECENT_WORK (2-3 short emergency jobs)
12. LLP_WHY_CHOOSE (for users who research before calling)
13. LLP_FAQ (3-5 logistics questions)
14. LLP_MAP_CONTACT
15. LLP_FINAL_CTA

> **Note:** ABOUT, TEAM, and PROCESS are minimal or omitted for emergency. Panic users rarely scroll past block 5. Structure front-loads action and proof; depth content exists for edge-case researchers.

### CTA Style
- Primary: Phone call (`tel:`) — prominent, repeated
- Secondary: Book online / booking widget
- Tone: "Call Today", "Get Help Now", "Book Urgent Service"

### Content Emphasis
- Speed and availability (same-day, 24/7, response time)
- Licensing and insurance (verifiable)
- Local codes and compliance (demonstrates expertise)
- Safety checklists (shutoff guides, hazard awareness)
- Permit knowledge (we handle it for you)

---

## Planning Archetype

**Niches:** Cleaning, financial planning, cosmetic dentist, accounting, landscaping, photography

**User state:** Researching, comparing options. Not urgent.
**Psychology:** "Who's the best fit? What's the process? Can I trust them?"
**Goal:** Build confidence, capture lead, schedule consultation.

Planning archetype splits into two sub-types based on the `stakes` modifier.

### Hero Right Column: Service Finder / Value Prop
Not a symptom router. Instead:
- Highlight key offer (e.g., "Save 20% with bi-weekly plans")
- "Get Free Quote" CTA
- Or brief service selector if many service types

### Trust Bar Content
Credentials/Certifications | Years Experience | Insured & Bonded | Satisfaction Guarantee

### Block Order — Planning (Low-Stakes)
1. LLP_HERO (quote CTA, service finder)
2. LLP_TRUST_BAR
3. LLP_SERVICES_GRID
4. LLP_PRICING (full ranges, plan pricing if recurring)
5. LLP_WHY_CHOOSE
6. LLP_GUARANTEE
7. LLP_REVIEWS
8. LLP_RECENT_WORK
9. LLP_PROCESS (condensed "How it works")
10. LLP_MEET_THE_TEAM (if available)
11. LLP_LOCAL_KNOWLEDGE + LLP_NEIGHBORHOODS (can combine for low-stakes)
12. LLP_ABOUT (short)
13. LLP_FAQ (6-8 questions)
14. LLP_MAP_CONTACT
15. LLP_FINAL_CTA

### Block Order — Planning (High-Stakes)
1. LLP_HERO (consultation CTA, not "call now")
2. LLP_TRUST_BAR (heavy on credentials)
3. LLP_SERVICES_GRID (with outcome framing)
4. LLP_MEET_THE_TEAM (practitioner-focused, full credentials)
5. LLP_LICENSING_COMPLIANCE (front-loaded for regulated industries)
6. LLP_PROCESS (detailed, process map with durations)
7. LLP_PRICING (market ranges + what drives variation + financing)
8. LLP_WHY_CHOOSE
9. LLP_GUARANTEE (process guarantees, not outcome guarantees)
10. LLP_REVIEWS (longer, narrative testimonials addressing fear/anxiety)
11. LLP_RECENT_WORK / CASE_STUDIES (detailed)
12. LLP_LOCAL_KNOWLEDGE
13. LLP_ABOUT
14. LLP_FAQ (8-10 questions, heavily weighted toward objection handling)
15. LLP_NEIGHBORHOODS
16. LLP_MAP_CONTACT
17. LLP_FINAL_CTA

> **Note:** High-stakes users read non-linearly across multiple visits. Add sticky anchor navigation for pages with `stakes=high`.

### CTA Style
- Primary: "Get Free Quote" or "Book Consultation"
- Secondary: Phone call
- Tone: "Experience the difference", "Join hundreds of satisfied customers"

### Content Emphasis
- Service quality and methodology
- Background checks / vetting (for in-home services)
- Eco-friendly / specialized products
- Community involvement and local story
- Process transparency (what to expect)
- Pricing structure (savings for recurring plans)

---

## Hybrid Archetype

**Niches:** General dentist, auto repair, pest control, roofing, garage door, appliance repair

**User state:** Could be urgent OR planning. Depends on the specific problem.
**Psychology:** Mix of "fix it now" and "I should schedule this"
**Goal:** Handle both paths — emergency gets fast action, planners get information.

### Dual-Path Triage

The hybrid hero MUST present two distinct, clearly labeled paths. The page does not assume which mode the user is in.

- **Path 1 (Urgent):** "Need Help Now? Call for Immediate Dispatch" → prominent phone number
- **Path 2 (Planning):** "Planning a Project? Get a Free Estimate" → form or scheduler link

The rest of the page serves both paths, but emergency content comes first. Emergency-intent users should get what they need before scrolling past block 6. Planners are rewarded for reading further.

### Hero Right Column: Dual-Path Triage
- "Need Help Now? Call for Immediate Dispatch" → phone
- "Planning a Project? Get a Free Estimate" → form/scheduler
- Dual CTAs are visually distinct (e.g., red/urgent vs. neutral/calm)

### Trust Bar Content
Licensed | Reviews | Same-Day Available | Insurance Accepted

### Block Order
1. LLP_HERO (dual-path triage: "Need Help Now?" + "Planning a Project?")
2. LLP_TRUST_BAR
3. LLP_AVAILABILITY
4. LLP_EMERGENCY_SECTION (shorter than full emergency archetype)
5. LLP_SERVICES_GRID (split: urgent vs. routine)
6. LLP_MID_CTA
7. LLP_PRICING (ranges for planned services only)
8. LLP_PROCESS
9. LLP_LICENSING_COMPLIANCE (if regulated)
10. LLP_REVIEWS
11. LLP_RECENT_WORK
12. LLP_WHY_CHOOSE
13. LLP_LOCAL_KNOWLEDGE + LLP_NEIGHBORHOODS
14. LLP_MEET_THE_TEAM (if available)
15. LLP_GUARANTEE
16. LLP_FAQ (mix of urgent + planned questions)
17. LLP_MAP_CONTACT
18. LLP_FINAL_CTA

### CTA Style
- Primary: Phone call (covers both urgent and non-urgent)
- Secondary: Book online / schedule
- Tone: "Call for same-day service" + "Schedule your appointment"

---

## Intent-Driven Block Ordering

The intent analyzer produces 3 layers. Layer 3 (hidden intent) directly affects which blocks get priority within the archetype ordering above.

### How Intent Drives Block Order

| Hidden Driver | Block Impact |
|---|---|
| Fear (cost escalation) | Front-load PRICING, move GUARANTEE up |
| Fear (wrong choice) | Front-load LICENSING_COMPLIANCE, REVIEWS, CASE_STUDIES |
| Fear (safety/stranger) | Front-load MEET_THE_TEAM, GUARANTEE (vetting signals) |
| Hope (solution/improvement) | Front-load RECENT_WORK, PROCESS |
| Uncertainty (confusion) | Front-load PROCESS, FAQ, simplify SERVICES_GRID |
| Urgency (crisis) | Front-load AVAILABILITY, EMERGENCY_SECTION, phone CTA |

### Trust Heuristics to Block Emphasis

| Heuristic | Primary Block |
|---|---|
| Social Proof | REVIEWS + TRUST_BAR (review count) |
| Authority | LICENSING_COMPLIANCE + CREDENTIALS |
| Risk Mitigation | GUARANTEE + WHY_CHOOSE |

---

## Progressive CTA by Page Position

CTA text evolves as the user scrolls deeper into the page. Each position targets a different psychological state.

| Page Position | Emergency CTA | Planning CTA | Hybrid CTA |
|---|---|---|---|
| Hero | "Call Now: (XXX) XXX-XXXX" | "Get Your Free Quote" | Dual: "Call Now" + "Get Estimate" |
| After Services Grid | "Need [specific service]? Call Today" | "Get a Custom Quote for Your Home" | "Book [service] or Call for Urgent Help" |
| Mid-page CTA bar | "Trusted by [X]+ [City] homeowners" | N/A (natural CTAs in blocks) | "[X] [City] families trust us" |
| After Reviews | "See why [City] homeowners call us" | "No obligation, no pressure" | "Join [X]+ satisfied customers" |
| Final CTA | "Ready? Get help in [City] today" | "Ready for [specific benefit] in [City]?" | "Emergency or planned: we're here for [City]" |
