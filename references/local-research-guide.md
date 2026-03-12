# Local Research Guide

WebSearch query templates for gathering city-specific content during LLP generation. Execute 4-6 queries in parallel, skip any where user provided explicit data.

## Universal Queries (All Archetypes)

### Neighborhoods & Areas
```
"{city} {state} neighborhoods areas communities map"
```
**Extract:** Neighborhood names, notable landmarks per area, character descriptions (historic, suburban, downtown, etc.)

### Demographics & Overview
```
"{city} {state} population demographics 2025"
```
**Extract:** Population, region name, notable features, economic profile, housing stock age

### Zip Codes
```
"{city} {state} zip codes"
```
**Extract:** All zip codes serving the city

### Climate & Environment
```
"{city} {state} climate weather seasonal"
```
**Extract:** Temperature extremes, seasonal patterns, precipitation, environmental factors affecting the niche

---

## Emergency Archetype Queries

### Building Codes & Requirements
```
"{city} {state} {niche} building codes requirements {current_year}"
"{city} {state} adopted building code IPC IMC NEC"
```
**Extract:** Which code edition adopted, effective date, ordinance number, local amendments

### Permit Requirements
```
"{city} {state} {niche} permit requirements residential"
"{city} {state} building inspections permits"
```
**Extract:** What work needs permits, inspection process, building department contact info, online portal name

### Common Problems (Niche-Specific)
```
"{city} {state} common {niche} problems homeowners"
"{city} {state} soil type foundation issues" (plumbing)
"{city} {state} water hardness quality report" (plumbing)
"{city} {state} power outage frequency grid issues" (electrical)
"{city} {state} average age HVAC systems homes" (hvac)
```
**Extract:** Local issues, stats with numbers, seasonal patterns, common failure modes

### Licensing Verification
```
"{state} {niche} license verification board"
```
**Extract:** State licensing board name, URL, license verification link, requirements for licensure

---

## Planning Archetype Queries

### Local Market & Demand
```
"{city} {state} {niche} common needs challenges"
"{city} {state} homeowner demographics income"
```
**Extract:** Why locals need this service, common pain points, market characteristics

### Regulations (If Regulated Industry)
```
"{state} {niche} licensing regulations requirements"
"{city} {state} business license {niche}"
```
**Extract:** Required certifications, regulatory body, disclosure requirements

### Local Competitors Context
```
"{city} {state} {niche} reviews common complaints"
```
**Extract:** What competitors get wrong (use for differentiator content), common customer pain points

---

## Hybrid Archetype Queries

Use a mix of emergency and planning queries based on which services are emergency vs planned. For example, a general dentist would research:
- Emergency: `"{city} {state} emergency dentist after hours"`
- Planning: `"{city} {state} dental insurance accepted dentists"`
- Codes: `"{state} dental board regulations"`

---

## Niche-Specific Query Additions

### Plumbing
- `"{city} water quality report hardness GPG"` — water hardness stats
- `"{city} soil type clay content foundation"` — soil/slab data
- `"{city} freeze risk pipe burst history"` — freeze patterns
- `"{city} backflow prevention program cross connection"` — backflow requirements

### HVAC
- `"{city} average heating cooling degree days"` — energy demand data
- `"{city} {state} HVAC efficiency requirements SEER"` — efficiency standards
- `"{city} common HVAC brands installed homes"` — local brand prevalence

### Electrical
- `"{city} {state} electrical code NEC adoption"` — code version
- `"{city} power grid reliability outage data"` — grid reliability
- `"{city} solar panel permit requirements"` — solar requirements (if applicable)

### Cleaning
- `"{city} water hardness mineral content"` — affects cleaning products
- `"{city} common home sizes types age"` — housing stock
- `"{city} seasonal cleaning challenges pollen dust"` — seasonal factors

### Dental
- `"{state} dental board AHPRA regulations advertising"` — advertising restrictions
- `"{city} common dental insurance plans accepted"` — insurance landscape
- `"{city} emergency dentist availability hours"` — emergency demand

### Roofing
- `"{city} {state} roofing permit requirements"` — permits
- `"{city} common roof types materials"` — local roofing materials
- `"{city} hail wind storm history damage"` — weather damage patterns
- `"{city} HOA roofing requirements restrictions"` — HOA rules

---

## Research Output Format

After running WebSearches, compile findings into this structure for use in content generation:

```
CITY RESEARCH: {City}, {State}
================================
Population: {number}
Region: {region_name}
Key neighborhoods: {list}
Zip codes: {list}

CLIMATE/ENVIRONMENT:
- {factor_1}: {detail}
- {factor_2}: {detail}

NICHE-SPECIFIC FINDINGS:
- {finding_1}: {detail with stats}
- {finding_2}: {detail with stats}

CODES/COMPLIANCE (if applicable):
- Code adopted: {code_name} {year}
- Licensing body: {name} ({url})
- Permit requirements: {summary}

LOCAL ISSUES:
- {issue_1}: {why it matters}
- {issue_2}: {why it matters}
```
