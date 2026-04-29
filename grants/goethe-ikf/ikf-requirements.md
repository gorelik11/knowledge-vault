# IKF Research Notes — Tone, Style & Requirements

## Compiled 2026-03-26 from Goethe website and funded project examples

---

## Application Format

The application is an **online form** at portal.gap.goethe.de, NOT a single uploaded document.

### Text fields (typed into portal):
- Short description EN (~150 words)
- Short description DE (~150 words)
- Detailed project description (max 1500 words)
- Artistic profiles (max 300 words each coproduction partner)
- List of participants (name, role, country)
- Schedule (3 phases)
- Expenses/Income summary table
- Links (max 12)

### PDF uploads (attachments):
- Confirmation form from local Goethe-Institut
- Itemized finance plan (Excel template provided)
- 2x travel cost quotes
- Letters of confirmation from coproduction partners
- Letters of intent from venues/festivals
- Detailed project description (optional, as separate file)
- Other supporting documents

---

## Project Description Guideline (from guideline_project-description.pdf)

### ARTISTIC CONCEPT

**Introduction / Background:**
- How did the initial idea originate? What was the motivating question?
- Why is international cooperation essential for the artistic idea?
- Explain the methodology proposed as part of the intercultural working process

**Development / Proceeding:**
- Which performing arts will be represented?
- What is the artistic value?
- Specify objectives and planned activities

### TEAM
- How did the collaboration idea develop? Present partners, their role and contribution
- Who else is participating?
- Any experience with intercultural artistic work?

### RELEVANCE OF THE TOPIC AND IMPACT
- Artistic and social relevance of the topic
- How could the project improve artistic landscape in applicant's region?
- How does it support cultural artistic exchange?
- Added value for current activities of applicant and partners

---

## Key Eligibility Requirements (from application-guidelines.pdf)

1. Applicant lives/works **outside Germany** (at least 3 years, established in local scene)
2. Project developed in **dialogue-oriented partnership** with co-producers
3. All co-producers **artistically involved**, joint creative process
4. IKF covers **max 75%** of total costs; min 25% own resources/third-party
5. At least **one performance outside Germany** (performance in Germany optional)
6. Max project duration: **15 months** from approval
7. Funding: **EUR 15,000–30,000**
8. **Must contact local Goethe-Institut** before applying (obligatory)
9. Application in **English only**
10. Projects already started are NOT eligible (unless "early start" approved via email)

### NOT eligible:
- Commercial projects, commissioned works
- Guest performances or tours
- Residency-based projects
- Pure music recordings
- Film or exhibition without performative element
- Ongoing operational costs

### At project end:
- 5-minute film documentation required (extra EUR 1,000 lump sum)

---

## Funded Project Examples — Tone & Framing

### "Narrow Backroads" (Spain/Germany, Music, Round 14/2024)
> "A musical composition that employs a hybrid approach, seamlessly blending spatial audio, 360-degree video, 3D modeling, dynamic lighting and visual effects to deliver a real-time performative experience. Guided by a poetic narrative, the score explores the interplay between travel, geography, expanding consciousness and the impacts of globalization."

### "Amphi" (Israel/Germany, Performance)
> "Trace the foundations of performance in public space, forms of movement and the architecture serving it, while addressing the present time, with its forms of ritual, mourning, celebration, and the contemporary performance of collectivity and politics."

### Key patterns in successful IKF projects:
1. **Dialogue between cultures** — not just touring, but genuine artistic exchange
2. **Language of artistic research** — "explores", "traces", "examines", not "we perform concerts"
3. **Interdisciplinary framing** valued — music + visual + digital elements
4. **Equal partnership** between German and non-German artists stressed
5. **Concrete venues and dates** already named
6. **Social/political relevance** — projects address identity, displacement, belonging, memory
7. Most funded projects are **theatre/dance/performance hybrids** — pure music projects are rarer, so framing as "live programme creation" (not album) is critical

### 2024 Round 14 — Music projects funded:
- Sonic diary (Australia) — Music
- Symbiophilia (Brazil) — Music
- Wilding AI (Canada) — Music
- Francesco Cavalli: La Doriclea (Finland) — Music
- Effusive Boundaries (Great Britain) — Music
- Dancehall to Gengetone (Kenya) — Music
- Narrow Backroads (Spain) — Music, Poetry
- Drifting To The Rhythms (Thailand) — Music, Dance

### 2024 funded: 29 projects total, ~8 music projects = ~28% music

---

## IKF Contact
- Email: koproduktionsfonds@goethe.de
- Phone: +49 89 15921 563
- Address: Goethe-Institut e.V. Zentrale, Oskar-von-Miller Ring 18, 80333 München
- Website: www.goethe.de/ikf
- Funded projects archive: https://www.goethe.de/en/kul/foe/int/ikf.html
- Previous projects: https://www.goethe.de/en/kul/foe/int/ikf/bis.html

---

## Technical Setup Notes

- `pypdf` (pip3) reads all Goethe PDF guidelines — no poppler needed
- Finance plan template: `template_finance-plan_2026.xlsx`
- DOCX creation: Office-Word-MCP-Server on 2nd computer
- Letters of intent → DOCX with logo → PDF
